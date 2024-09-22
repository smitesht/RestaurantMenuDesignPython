# Restaurant Menu Design using Composite Design Pattern

![image](https://github.com/user-attachments/assets/a9f917ef-63da-4dda-b2fb-1b396b5a70c5)


## What is Composite Pattern
The Composite Design Pattern is a structural pattern that allows you to compose objects into tree-like structures to represent part-whole hierarchies. This pattern allows clients to treat individual objects and compositions of objects uniformly, which simplifies code and enhances flexibility.

## Key ELements of the pattern
- **Component**: An abstract class or interface that defines the common interface for all objects in the composition (both leaf and composite). **MenuComponent** is the abstract class.
- **Leaf**: A class that implements the component interface and represents individual objects in the composition. Leaf nodes do not have children. **MenuItem** is the leaf class.
- **Composite**: A class that also implements the component interface and contains child components. It can add, remove, and manage its children. **MenuCategory and ComboMenuCategory** are the composite classes.

## When to use
- **Hierarchical Structures**: When you need to represent a tree-like structure (e.g., file systems, organization charts, menus).
- **Uniform Treatment of Objects**: When clients should be able to treat individual objects and compositions uniformly without worrying about their specific types. In this example, MenuItem, MenuCategory, and ComboMenuCategory objects are treated uniformly in the main method.

![image](https://github.com/user-attachments/assets/a451994e-9059-4244-b068-b9aec3d49882)


## Code Snippet

```python

from abc import ABC, abstractmethod

class MenuComponent(ABC):
    @abstractmethod
    def print(self):
        pass
    
class MenuItem(MenuComponent):
    def __init__(self, name, price ):
        self.itemName = name
        self.itemPrice = price
        
    def print(self):
        print(f"{self.itemName}.................${self.itemPrice:.2f}")
        
class MenuCategory(MenuComponent):
    def __init__(self, categoryName):
        self.categoryName = categoryName
        self.menuItems = []
        
    def addItem(self, menuItem):
        self.menuItems.append(menuItem)
        
    def removeItem(self, menuItem):
        self.menuItems.remove(menuItem)
        
    def print(self):
        print(f"\n{self.categoryName}")
        for menuItem in self.menuItems:
            menuItem.print()
            

class ComboMenuCategory(MenuComponent):
    def __init__(self, comboName, comboPrice):
        self.comboName = comboName
        self.comboPrice = comboPrice
        self.menuItems = []
        
    def addItem(self, menuItem):
        self.menuItems.append(menuItem)
        
    def removeItem(self, menuItem):
        self.menuItems.remove(menuItem)
        
    def print(self):
        print(f"\n{self.comboName}............${self.comboPrice}")
        for menuItem in self.menuItems:
            print(f"{menuItem.itemName}")
            


if __name__ == "__main__":
    vegPizza  = MenuItem("Vegi. Pizza", 20.00)
    chickenPizza = MenuItem("Chicken Pizza", 25.50)
    
    garlicBread = MenuItem("Garlic Bread", 5.00)
    chickenNugget = MenuItem("Chicken Nugget",6.50)
    
    coke = MenuItem("Coke",1.50)
    pepsi = MenuItem('Pepsi',1.50)
    
    
    pizzaCategory = MenuCategory("Pizza")
    pizzaCategory.addItem(vegPizza)
    pizzaCategory.addItem(chickenPizza)
    
    sideDish = MenuCategory("Side Dishes")
    sideDish.addItem(garlicBread)
    sideDish.addItem(chickenNugget)
    
    beverages = MenuCategory("Beverages")
    beverages.addItem(coke)
    beverages.addItem(pepsi)
    
    vegMealCombo = ComboMenuCategory("Veg. Meal Combo",25.00)
    vegMealCombo.addItem(vegPizza)
    vegMealCombo.addItem(garlicBread)
    vegMealCombo.addItem(coke)
    
    chickenMealCombo = ComboMenuCategory("Chicken Meal Combo",31.00)
    chickenMealCombo.addItem(chickenPizza)
    chickenMealCombo.addItem(chickenNugget)
    chickenMealCombo.addItem(pepsi)
    
    restaurantMenu = MenuCategory("Awesome Pizza Restaurant")
    restaurantMenu.addItem(pizzaCategory)
    restaurantMenu.addItem(sideDish)
    restaurantMenu.addItem(beverages)
    restaurantMenu.addItem(vegMealCombo)
    restaurantMenu.addItem(chickenMealCombo)
    
    restaurantMenu.print()

```
