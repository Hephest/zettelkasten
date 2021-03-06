Link: [[202008112334 Design Patterns]]

# Abstract Factory
Use a generic function with specific factories.

## Description
> ***TL;DR** Provides a way to encapsulate a group of individual factories.

Abstract Factory Pattern serves to provide an interface for creating related/dependent objects without need to specify their actual class.

The idea is to abstract the creation of objects depending on business
logic, platform choice, etc.

In Python, the interface we use is simply a callable, which is "builtin" interface.

in Python, and in normal circumstances we can simply use the class itself as
that callable, because classes are first class objects in Python.

## Example
```python
import random


class PetShop:

    """A pet shop"""

    def __init__(self, animal_factory=None):
        """pet_factory is our abstract factory.  We can set it at will."""

        self.pet_factory = animal_factory

    def show_pet(self):
        """Creates and shows a pet using the abstract factory"""

        pet = self.pet_factory()
        print("We have a lovely {}".format(pet))
        print("It says {}".format(pet.speak()))


class Dog:
    def speak(self):
        return "woof"

    def __str__(self):
        return "Dog"


class Cat:
    def speak(self):
        return "meow"

    def __str__(self):
        return "Cat"


# Additional factories:

# Create a random animal
def random_animal():
    """Let's be dynamic!"""
    return random.choice([Dog, Cat])()


# Show pets with various factories
def main():
    """
    # A Shop that sells only cats
    >>> cat_shop = PetShop(Cat)
    >>> cat_shop.show_pet()
    We have a lovely Cat
    It says meow
    # A shop that sells random animals
    >>> shop = PetShop(random_animal)
    >>> for i in range(3):
    ...    shop.show_pet()
    ...    print("=" * 20)
    We have a lovely Cat
    It says meow
    ====================
    We have a lovely Dog
    It says woof
    ====================
    We have a lovely Dog
    It says woof
    ====================
    """


if __name__ == "__main__":
    random.seed(1234)  # for deterministic doctest outputs
    import doctest

    doctest.testmod()
```