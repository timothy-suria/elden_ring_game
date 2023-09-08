# elden_ring_game
Made by: Timothy Suria, Charlene Tan , Argya Daffa Hari Diputra
this is a 2d inspired game from elden ring that has enemies, dungeons, spawn-rates, etc. 
We created an EnemyManager class to deal with creating new enemies. This follows the
Single Responsibility Principle (SRP) as the method to create new enemies is not also in the
types of Ground.
We also made a SpawnCapable interface to show which Grounds could spawn enemies,
and a CardinalDirection enumeration to show which side of the map some types of Ground
are on, as REQ 5 has different enemies ‘spawn’ on the same type of ground on different
sides of the map. Although not specified, we have decided to implement it in requirement 1
as well, just in case it is needed for future implementations.
One alternative to the CardinalDirection and SpawnCapable methods for spawning enemies
is to have some form of SpawnMap. It would be a one-to-one size wise with the game’s
map, and each location would just show what enemy could spawn there. One possible issue
with this would be if the same enemy could have different spawn rates at the same kind of
Ground.
The actor class is implemented by all the enemies, player, and trader. All actors are given a
list of sub actions from the action class such as AttackAction instead of implementing it over
and over again for a new actor/character which adheres to the Do not Repeat Yourself
principle (DRY).
We made some interfaces such as BonePileCapable and SlamAttackCapable for certain
abilities and attacks that are only available on some enemies. Kale has an association with
WeaponItem as he has a list of weapons that he can sell. Rather than have a new attribute
for each weapon, it just has one list. This follows the Reduced Dependency Principle (ReD)
as it has less concrete weapon classes.
We made a ModifyRuneCapable interface to show which classes were capable of modifying
the amount of runes the Player has. We made a Trader interface to show which classes had
the ability to trade with the Player. We made an Interactable interface to show which classes
can be interacted with by the Player. Interactable and Trader are different interfaces to follow
the Interface Segregation Principle (ISP). Some interactable things in the game may not be
Traders, such as the SiteOfLostGrace, which is a type of Ground.
We made a RunesManager class which represents the number of runes that the Player
currently has , meaning that the Player class itself does not need to handle the runes which
follow the Single Responsibility Principle (SRP). RunesManager being its own class instead
of being an attribute of the Player class will also allow us to extend any future uses using it
more easily.
At first, we considered having runes to be just a variable but that would be harder to extend
in the future and it will not follow Single Responsibility Principle (SRP).
Enemies have a dependency with RandomNumberGenerator as, when they are killed by the
Player, they drop runes within a certain range. These runes are added to the Player’s rune
count by calling a method from Runes, adhering to the Single Responsibility Principle (SRP).
DroppedRunes inherits from Item so that it can be shown on the ground. It cannot, however,
be added to the Player’s inventory, so it has a unique PickUpAction to pick it up called
PickUpRunesAction.
Some classes (such as the classes for the enemies, the Player, and the Flask) implement
the Resettable interface as they are affected whenever the game resets.
We made a base PlayerClass that all classes (Samurai, Bandit, Wretch) inherit from. This
helps with future enhancements and prevents having to manually make changes to each
class. This adheres to the Do not Repeat Yourself principle (DRY).
PlayerDeathAction and SiteOfLostGrace have a dependency with ResetManager as the
ResetManager’s method is called when the game resets, which happens when using a Site
of Lost Grace or when the Player dies. PlayerDeathAction also has a dependency on
DroppedRunes as it creates DroppedRunes on a Ground when the Player dies.
