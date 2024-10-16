
### Summary

- **`ClapTrap`** is a base class that defines general behaviors for a robot-like entity (such as attack, take damage, and repair).
- **`ScavTrap`** is a derived class that inherits the basic behavior of `ClapTrap` and adds its own features (like guard mode) or modifies inherited ones.
- Inheritance allows `ScavTrap` to **reuse** and **extend** the functionality of `ClapTrap`, leading to more organized and maintainable code.

In C++, **inheritance** allows one class (the **derived class**) to inherit the attributes and methods of another class (the **base class**). This promotes code reuse and provides a way to create more specialized versions of a generic class.

In this case, the **`ScavTrap` class inherits from `ClapTrap`**, meaning `ScavTrap` will have access to all the public and protected members (data and methods) of `ClapTrap`. The **private members** of `ClapTrap` are still part of each `ScavTrap` object, but they are inaccessible directly within `ScavTrap`—you can only access them through public or protected methods.

### `ClapTrap` Class Overview

```cpp
#ifndef CLAPTRAP_HPP
#define CLAPTRAP_HPP

#include <iostream>

class ClapTrap
{
	private:
		std::string _name;
		u_int32_t _HP;
		u_int32_t _MP;
		u_int32_t _atkDmg;
		std::string _target;
	public:
		// Constructors
		ClapTrap();
		ClapTrap( std::string name );
		// Canonical Orthodox Form
		ClapTrap( const ClapTrap &copy );
		ClapTrap &operator=(const ClapTrap &other);
		// Destructor
		~ClapTrap();
		// Public methods
		void attack( const std::string &target);
		void takeDamage(unsigned int amount);
		void beRepaired(unsigned int amount);
};

#endif
```

The `ClapTrap` class is a generic base class representing a robot-like entity. It has:

- **Private attributes**: `_Name`, `_HP`, `_MP` (Mana Points or Energy Points), `_atkDmg` (attack damage), and `_target`.
- **Constructors**: For initializing `ClapTrap` objects.
- **Destructor**: A special method called when the object is destroyed.
- **Public methods**:
    - `attack`: Makes the `ClapTrap` attack a target.
    - `takeDamage`: Reduces the health points (HP) when taking damage.
    - `beRepaired`: Heals or repairs the `ClapTrap` by increasing its HP.

### `ScavTrap` Class Overview
```cpp
#ifndef SCAVTRAP_HPP
#define SCAVTRAP_HPP

#include "ClapTrap.hpp"

class ScavTrap: public ClapTrap
{
	private:
		std::string _name;
		u_int32_t _HP;
		u_int32_t _MP;
		u_int32_t _atkDmg;
		bool _guard;
		std::string _target;
	public:
		//Constructors
		ScavTrap();
		ScavTrap( std::string name );
		// Canonical Orthodox Form
		ScavTrap( const ScavTrap &copy );
		ScavTrap &operator=( const ScavTrap &other );
		// Destructor
		~ScavTrap();
		// Methods
		void attack( const std::string &target );
		void guardGate();
};

#endif
```

The **`ScavTrap`** class inherits from `ClapTrap` using the syntax:

```cpp
class ScavTrap: public ClapTrap
```

This means:

- **`ScavTrap` will inherit all public and protected members from `ClapTrap`**, including:
    - The `attack`, `takeDamage`, and `beRepaired` methods.
    - Constructors and destructors of `ClapTrap` (though `ScavTrap` can define its own).
- **`ScavTrap` can also extend or override the functionality** of `ClapTrap`.

### Breakdown of `ScavTrap`'s Inheritance

1. **Attributes of ScavTrap:** The `ScavTrap` class introduces some of its own private attributes:
    
    - `_Name`, `_HP`, `_MP`, and `_atkDmg` are **redefined** in `ScavTrap`. This means that `ScavTrap` may use these attributes differently from `ClapTrap` (even though they share similar names).
    - `_guard`: A new boolean flag that likely represents whether `ScavTrap` is in guard mode.
    - `_target`: Seems like it’s a specific target that the `ScavTrap` might attack or defend.
2. **Constructors and Destructor:**
    
    - `ScavTrap()` and `ScavTrap(std::string name)` are constructors specific to `ScavTrap`.
        - These constructors will likely call the base class `ClapTrap` constructor to initialize the inherited parts of the class, and then initialize `ScavTrap`-specific attributes like `_guard`.
    - `ScavTrap(const ScavTrap &copy)` and `ScavTrap &operator=(const ScavTrap &other)` are part of the **Canonical Form** (a set of standard constructors, including copy constructor and assignment operator).
    - `~ScavTrap()` is the destructor specific to `ScavTrap`, called when the object is destroyed.
3. **Public Methods:**
    
    - `attack`: `ScavTrap` may override the `attack` method from `ClapTrap` to add its own behavior, such as a different type of attack.
    - `guardGate`: This is a new method specific to `ScavTrap`, not present in `ClapTrap`. This function might enable `ScavTrap`'s guard mode, setting the `_guard` attribute to `true`.

### Example: How `ScavTrap` Inherits and Extends `ClapTrap`

Here’s an example to illustrate how inheritance works:

```cpp
#include "ScavTrap.hpp"

int main() {
    // Creating a ScavTrap object
    ScavTrap scav("Guardian");

    // ScavTrap can use methods inherited from ClapTrap
    scav.attack("Enemy");
    scav.takeDamage(25);
    scav.beRepaired(15);

    // ScavTrap can also use its own unique method
    scav.guardGate(); // Activates guard mode
}
```

- **Inherited Methods**: The `ScavTrap` object `scav` can call the `attack`, `takeDamage`, and `beRepaired` methods, which are defined in `ClapTrap`, because `ScavTrap` inherits them.
- **Extended Functionality**: The `guardGate()` method is unique to `ScavTrap` and extends the functionality of `ClapTrap`.

### The Role of Constructors in Inheritance

When you create a `ScavTrap` object, its constructor needs to initialize both the inherited members (from `ClapTrap`) and its own members.

For example, a `ScavTrap` constructor might look like this:

```cpp
ScavTrap::ScavTrap(std::string name) : ClapTrap(name), _guard(false) {
    _HP = 100;
    _MP = 50;
    _atkDmg = 20;
    std::cout << "ScavTrap " << _Name << " is created!" << std::endl;
}
```

In this constructor:

- The **base class constructor** `ClapTrap(name)` is called to initialize the `ClapTrap` part of the `ScavTrap` object.
- Then, `ScavTrap`-specific attributes like `_guard`, `_HP`, `_MP`, and `_atkDmg` are initialized.