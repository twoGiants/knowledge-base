# Golang

## PR Readiness Checklist

- Tests pass
- Static check has 0 errors (see below)

## Study Resources

- Good one from Mark: [Go Code Review Comments](https://go.dev/wiki/CodeReviewComments)
- official but a outdated and maybe frozen: [Effective Go](https://go.dev/doc/effective_go)
- article: [Best Practices for a New Go Developer](https://www.cloudbees.com/blog/best-practices-for-a-new-go-developer)
- [Go wiki](https://go.dev/wiki)
- [Learning Go, 2nd Edition](https://learning.oreilly.com/library/view/learning-go-2nd/9781098139285)
- [Go in Action](https://learning.oreilly.com/library/view/go-in-action/9781617291784)
- [Go in Practice](https://learning.oreilly.com/library/view/go-in-practice/9781633430075/)

## Rune

A rune literal in Go is a character enclosed in single quotes, representing a single Unicode code point. For example, `'a'` or `'😊'`. It is of type `rune`, which is an alias for `int32`.

## Slices

- portion of slice syntax does not include the number of the last used index:
```go
nums := []int{1,2,3,4}
portion := nums[0:2]
fmt.Println(portion) 
// prints: [1,2], number at index 2 which is "3" is not included
```
## Format

[Docs](https://pkg.go.dev/fmt).

## Tooling

- Coverage with browser output: [link](https://go.dev/blog/cover), 
```bash
go tool cover -html=coverage.out
```
- static code check
```bash
go run honnef.co/go/tools/cmd/staticcheck@latest -f stylish -checks 'all,-ST1000' ./...
```
## Interfaces

- A more typical pattern in Go is to return concrete structs, and use interfaces for parameter types received by functions.
- Interfaces are typically used for return types only where different implementation structs might be returned.

## Errors

Learning Go, 2nd Edition, Ch [9. Errors](https://learning.oreilly.com/library/view/learning-go-2nd/9781098139285/ch09.html#id109)

### Basics

- use `error` interface type as function return types
- use `nil` for the error return if none happened
- never return custom errors

### Sentinel Errors

- use Sentinel errors sparingly and write them starting `ErrSomeName`
- use `errors.As` instead of type assertion
- used in std packages and libraries, e.g. `os.ErrNotExist`

### Wrapping Errors

- *error tree* is a series of wrapped errors
- wrap errors using `fmt.Errorf` and `%w`, e.g. `fmt.Errorf("in fileChecker: %w", err)`
- instead of `errors.Unwrap` use `errors.Is` and `errors.As`
- implement `Unwrap` to wrap errors with your custom error
- if you want to create a new error that contains the message from another error, but don't want to wrap it use `%v`, e.g. 

```go
err := internalFunction()
if err != nil {
    return fmt.Errorf("internal failure: %v", err)
}
```

### Wrapping Multiple Errors

- for e.g. validation when you need to return an error for each field use `errors.Join`

```go
type Person struct {
    FirstName string
    LastName  string
    Age       int
}

func ValidatePerson(p Person) error {
    var errs []error
    if len(p.FirstName) == 0 {
        errs = append(errs, errors.New("field FirstName cannot be empty"))
    }
    if len(p.LastName) == 0 {
        errs = append(errs, errors.New("field LastName cannot be empty"))
    }
    if p.Age < 0 {
        errs = append(errs, errors.New("field Age cannot be negative"))
    }
    if len(errs) > 0 {
        return errors.Join(errs...)
    }
    return nil
}
```
- another way to merge errors is using multiple `%w`

```go
err1 := errors.New("first error")
err2 := errors.New("second error")
err3 := errors.New("third error")
err := fmt.Errorf("first: %w, second: %w, third: %w", err1, err2, err3)
```

### Is and As

- use `errors.Is` to check for sentinel errors in the error tree, it uses `==` internally

```go
func fileChecker(name string) error {
    f, err := os.Open(name)
    if err != nil {
        return fmt.Errorf("in fileChecker: %w", err)
    }
    f.Close()
    return nil
}

func main() {
    err := fileChecker("not_here.txt")
    if err != nil {
        if errors.Is(err, os.ErrNotExist) {
            fmt.Println("That file doesn't exist")
        }
    }
}
```
- for non comparable types implement the `Is` method
