
1. Getters and setters
```cpp
/* Getters and setters */
std::string	get_fname(void) const;
std::string	get_lname(void) const;
std::string	get_nick(void) const;
std::string	get_phone_num(void) const;
std::string	get_secret(void) const;

void	set_fname(std::string str);
void	set_lname(std::string str);
void	set_nick(std::string str);
void	set_phone_num(std::string str);
void	set_secret(std::string str);```

These are **getters** and **setters**:

- **Getters** (like `get_fname()`) are used to retrieve the value of a private member.
- **Setters** (like `set_fname()`) allow you to set the value of a private member.

This approach respects **encapsulation**, as you don't directly access the private variables, but you can still interact with them using these controlled methods.

#### Understanding the syntax:

- The `const` keyword at the end of each getter (e.g., `std::string get_fname(void) const;`) indicates that this function doesn't modify the object. It guarantees that calling `get_fname()` won’t alter the `Contact` object’s state.
- The setters (like `set_fname(std::string str)`) take a `std::string` as a parameter and assign that to the corresponding private member.

This helps keep your data safe and avoids accidental changes by external code.
