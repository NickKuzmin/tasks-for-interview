- `IRequest<T>` - the request returns a value.
- `IRequest` - the request does not return a value.
- 
- `IRequestHandler<T, U>` - implement this and return Task<U>
- `RequestHandler<T, U>` - inherit this and return U

```
/ Command
public class CreateCustomerCommand : IRequest<Customer>
{
    public Customer Customer { get; set; }
}


// Command Handler
public class CreateCustomerCommandHandler : IRequestHandler<CreateCustomerCommand, Customer>
{
    private readonly IRepository<Customer> _repository;

    public CreateCustomerCommandHandler(IRepository<Customer> repository)
    {
        _repository = repository;
    }

    public async Task<Customer> Handle(CreateCustomerCommand request, CancellationToken cancellationToken)
    {
        return await _repository.AddAsync(request.Customer);
    }
}
```

```
// Query
public class GetCustomerByIdQuery : IRequest<Customer>
{
    public Guid Id { get; set; }
}

// Query Handler
public class GetCustomerByIdQueryHandler : IRequestHandler<GetCustomerByIdQuery, Customer>
{
    private readonly IRepository<Customer> _repository;

    public GetCustomerByIdQueryHandler(IRepository<Customer> repository)
    {
        _repository = repository;
    }

    public async Task<Customer> Handle(GetCustomerByIdQuery request, CancellationToken cancellationToken)
    {
        return _repository.GetAll().FirstOrDefault(x => x.Id == request.Id);
    }
}
```

```
public class CustomerController : ControllerBase
{
    private readonly IMediator _mediator;

    public CustomerController(IMediator mediator)
    {
        _mediator = mediator;
    }

    [HttpGet("all")]
    public async Task<IActionResult> GetAll()
    {
        var result = await _mediator.Send(new GetCustomersQuery());

        return Ok(result);
    }

    [HttpGet("{id}")]
    public async Task<IActionResult> Get([FromRoute] Guid id)
    {
        var result = await _mediator.Send(new GetCustomerByIdQuery
        {
            Id = id
        });

        return Ok(result);
    }

    [HttpPost("add")]
    public async Task<IActionResult> Add([FromBody] CreateCustomerModel createCustomerModel)
    {
        //TODO: Use AutoMapper for mappings

        var customer = new Customer()
        {
            FirstName = createCustomerModel.FirstName,
            LastName = createCustomerModel.LastName,
            Birthday = createCustomerModel.Birthday,
            Age = createCustomerModel.Age,
            Phone = createCustomerModel.Phone,
        };

        var result = await _mediator.Send(new CreateCustomerCommand
        {
            Customer = customer
        });

        return Ok(result);
    }

    [HttpPut("update")]
    public async Task<IActionResult> Update([FromBody] UpdateCustomerModel updateCustomerModel)
    {
        //TODO: Use AutoMapper for mappings

        var existCustomer = await _mediator.Send(new GetCustomerByIdQuery
        {
            Id = updateCustomerModel.Id
        });

        if (existCustomer == null)
        {
            return BadRequest($"No customer found with the id {updateCustomerModel.Id}");
        }

        var customer = new Customer()
        {
            Id = updateCustomerModel.Id,
            FirstName = updateCustomerModel.FirstName,
            LastName = updateCustomerModel.LastName,
            Birthday = updateCustomerModel.Birthday,
            Age = updateCustomerModel.Age,
            Phone = updateCustomerModel.Phone,
        };

        var result = await _mediator.Send(new UpdateCustomerCommand
        {
            Customer = customer
        });

        return Ok(result);
    }
}
```
