要解析URL中的查询参数，需要用[FromQuery]注释控制器方法参数，例如：
```
[Route("api/[controller]")]
public class PersonController : Controller
{
    //api/Person/GetById?id=123
    [HttpGet("[action]")]
    public string GetById([FromQuery]int id)
    {

    }
    //api/Person/GetByName?firstName=zhangsan&lastName=wang
    [HttpGet("[action]")]
    public string GetByName([FromQuery]string firstName, [FromQuery]string lastName)
    {

    }
    //api/Person/GetByNameAndAddress?firstName=zhangsan&lastName=wang&address=
    [HttpGet("[action]")]
    public string GetByNameAndAddress([FromQuery]string firstName, [FromQuery]string lastName, [FromQuery]string address)
    {
        
    }
}
```
