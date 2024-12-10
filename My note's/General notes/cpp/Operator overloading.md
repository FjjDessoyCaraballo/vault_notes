
To overload an operator means to specify what exactly that operator will do. In a way, it customizes what it does. In our case here, we are simply giving it the value of whatever is given at `getRawBits()`, which only returns the private variable `_fpn` for internal use.

The second overload operation is taking care of the output `<<`, therefore the return value is `std::ostream&`. After we insert this overload method in our class, we get to use the output in main().

```cpp
Fixed &Fixed::operator=(const Fixed &other)
{
	if (this != &other)
	{
		_fpn = other.getRawBits();
	}
	return (*this);
}

std::ostream &operator<<(std::ostream &other, Fixed const &fix)
{
	other << fix.toFloat();
	return (other);
}```

#### What does it do in main()?

For our output operator, we enable our operator to output floats automatically:

```cpp
int main(void)
{
	Fixed myFixed;
	std::cout << myFixed << std::endl;
}
```

And the result of this will be outputted in the console like:

```shell
%> ./fix
5.0
```


