# It's my Go !

## go run:
if there is a go's source file named *hello.go*,you can do this:
```
go run hello.go // compile + run
---
go build hello.go // make a compiled file named hello 
./hello // run the hello

```
## go writing
tips : It's not necessary but OK to wright ; after a line of code(no ; was preferred)

- import:
```
import "fmt"
import "time"
```
this is OK but we can also type by this way
```
import(
    "fmt"
    "time"
)
```
==the laster was preferred==

### key point:
```
func main(){

}
```
correct
```
func main()
{

}
```
==completely wrong!== The compiler can not understand
