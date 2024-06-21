#include <iostream>
#include <vector>
#include <string>

// Base class for all entities in the meadow
class Entity {
public:
    Entity(const std::string &name) : name(name) {}
    virtual void interact() = 0;

    std::string getName() const {
        return name;
    }

protected:
    std::string name;
};

// Player class
class Player : public Entity {
public:
    Player(const std::string &name) : Entity(name) {}

    void interact() override {
        std::cout << "Player " << name << " is exploring the meadow." << std::endl;
    }

    void collectItem(const std::string &item) {
        inventory.push_back(item);
        std::cout << "Collected: " << item << std::endl;
    }

    void showInventory() const {
        std::cout << "Inventory: ";
        for (const auto &item : inventory) {
            std::cout << item << " ";
        }
        std::cout << std::endl;
    }

private:
    std::vector<std::string> inventory;
};

// Creature class
class Creature : public Entity {
public:
    Creature(const std::string &name) : Entity(name) {}

    void interact() override {
        std::cout << "Creature " << name << " is frolicking in the meadow." << std::endl;
    }
};

// EnchantedMeadow class
class EnchantedMeadow {
public:
    void addEntity(Entity *entity) {
        entities.push_back(entity);
    }

    void explore() const {
        for (const auto &entity : entities) {
            entity->interact();
        }
    }

private:
    std::vector<Entity *> entities;
};

int main() {
    // Create the enchanted meadow
    EnchantedMeadow meadow;

    // Create a player and some creatures
    Player player("Arthur");
    Creature creature1("Bunny");
    Creature creature2("Fairy");

    // Add entities to the meadow
    meadow.addEntity(&player);
    meadow.addEntity(&creature1);
    meadow.addEntity(&creature2);

    // Simulate exploring the meadow
    meadow.explore();

    // Player collects some items
    player.collectItem("Magic Flower");
    player.collectItem("Golden Acorn");

    // Show player's inventory
    player.showInventory();

    return 0;
}
