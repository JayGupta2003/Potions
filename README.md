Potions
============

This module adds several potions which have a variety of effects such as healing, regen, speed increases, and status
ailment cures. This also adds a potion drinking system as well as the ability for other systems to modify the effects.
Moreover, if a potion is durable enough, an empty bottle will be returned following the potion consumption.

The following potions are present in this module:

* All Speed - Combines the effects of all the speed potions.
* Cure All - Cures all status ailments when consumed.
* Cure Poison - Cures poison status when consumed.
* Double Jump - Allows the user to double jump for 15 seconds.
* Heal - Restores 20 HP to the user.
* Health Boost - Increases the user's base max health by 50% for 30 seconds.
* Hemlock Potion - Is a worse poison potion. 
* Item Use Speed - Increases the user's item use speed by 25% for 15 seconds.
* Jump Speed - Doubles the user's jump speed for 10 seconds.
* Poison - Poisons user, dealing 3 damage per second for up to 15 seconds.
* Regen - User regenerates 3 HP per second for 10 seconds.
* Regen II - User regenerates 6 HP per second for 10 seconds ( Like regular Regen X 2 )
* Resist Physical - Temporarily increases user's physical defense by 15 for 20 seconds.
* Resist Poison - Reduces the effects of poison statuses by 2 when consumed for 15 seconds.
* Swim Speed - Doubles the user's swim speed for 10 seconds.
* Walk Speed - Doubles the user's walk speed for 10 seconds.
* Explosive - When the player uses this on an object, it triggers an explosion.
* Invincible - Makes the user invincible for 10 seconds.
* Mega Jump - Doubles all jump stats for 10 seconds
* Giga Jump - Triples all jump stats for 10 seconds
* Ninja - speeds up your running and jumping
* BlindWalk - Turns the player blind for 5 seconds along with speed decrease (Awaiting API integration for the No_Visibility effect to work)
* Battle - It increases your damage withstand limit and helps you regenrate faster.
* Super Heal - Restores a vast amount of HP
* Sacred - Regenerates 3 HP per second for 10 seconds, increases the user's base max health by 25% for 30 seconds, and also cures poison status.
* Ultra Heal - Restores a very vast amount of HP for 2 seconds.

## Contribution

Fork and clone this repository locally.

### Creating a Potion
To create a potion, create a prefab similar to the ones [here](https://github.com/Terasology/Potions/tree/master/assets/prefabs/potion) at `Potions/assets/prefabs/potion/` and add the associated icon to `Potions/assets/textures/potions/`.
For instance, to create a potion called "HealthBoost", the prefab should look like
```
{
    "parent": "engine:iconItem",
    "Item": {
        "icon": "Potions:HealthBoostPotion1Bottle",
        "stackId": "Potions:healthBoostPotion",
        "consumedOnUse": true
    },
    "DisplayName": {
        "name": "Potion of Minor Health Boost",
        "description": "Increases the user's base max health by 50% for 30 seconds."
    },
    "Potion": {
        "hasGenome": false,
        "effects": [
            {
                "effect": "TEMP_MAX_HEALTH_BOOST",
                "magnitude": 50,
                "duration": 30010
            }
        ]
    },
    "ItemHelp": {
        "category": "Potions",
        "paragraphText": [
             "Increases the user's base max health by 50% for 30 seconds."
        ]
    }
}
```
where "HealthBoostPotion1Bottle.png" is the name of the icon file which resides in `Potions/assets/textures/potions/`,  
`DisplayName` and `ItemHelp` carry information relevant to the potion,  
the `effects` field inside Potion contains a list of effects the potion carries.  
All pre-defined potions in this module should have a hasGenome of false because they were not generated by the Herbalism system.  
All potions should have a consumedOnUse set as true so that they exhaust after usage.  
Each effect has an associated `magnitude` and `duration`.  
**Multiple effects** can be used too in this fashion:

```
 "Potion": {
        "hasGenome": false,
        "effects": [
            {
                "effect": "WALK",
                "magnitude": 2,
                "duration": 10100
            },
            {
                "effect": "SWIM",
                "magnitude": 2,
                "duration": 10100
            },
            {
                "effect": "JUMP",
                "magnitude": 2,
                "duration": 10100
            }
        ]
}
```

### Creating a container

Presently we have bottles and vials as containers. To create a similar container, create a prefab similar to [these](https://github.com/Terasology/Potions/tree/master/assets/prefabs) at `Potions/assets/prefabs/`. Also add or use an existing icon from `Potions/assets/textures/`.

For instance, to create a "GlassBottle", the prefab should look like:
```
{
    "parent": "engine:iconItem",
    "Item": {
        "icon": "Potions:EmptyPotionBottle",
        "stackId": "Potions:glassBottle",
        "consumedOnUse": false
    },
    "DisplayName": {
        "name": "Glass Bottle",
        "description": "Used for storing fluids such as potions or water."
    },
    "EmptyPotion": {
    },
    "Durability": {
        "durability": 3,
        "maxDurability": 3
    },
    "FluidContainerItem": {
        "volume": 0.4,
        "maxVolume": 0.4,
        "fluidMinPerc": [0.1875, 0.15625],
        "fluidSizePerc": [0.625, 0.4375],
        "textureWithHole": "Potions:EmptyPotionBottle",
        "emptyTexture": "Potions:EmptyPotionBottle"
    },
    "ItemHelp": {
        "category": "Alchemy",
        "paragraphText": [
            "Used for storing fluids such as potions or water."
        ]
    }
}
```
where "EmptyPotionBottle.png" is the name of the icon file which resides in `Potions/assets/textures/`,  
`DisplayName` and `ItemHelp` carry information relevant to the container,  
`durability` measures the current durability level of the bottle. If durability is <= 0, the item gets destroyed.  
`maxDurability` is the maximum durability allowed with this object.
`FluidContainerItem` specify other related parameters.  
`textureWithHole` specifies the icon when the bottle has fluid in it  
`fluidMinPerc` and `fluidSizePerc` determine how the fluid is drawn in the container  
`volume` measures the current amount of the current fluid that's inside of this fluid container in litres
`maxVolume` is the max amount of fluid that can be stored in this container in litres.

The blank `EmptyPotion` field specifies this prefab as a potion container.

Send in PRs to this repository and feel free to add your name to the authors list in the [module.txt file](https://github.com/Terasology/Potions/blob/master/module.txt). Also add credits to [this README](https://github.com/Terasology/Potions/blob/master/README.md) citing sources for icons and textures.

## Credits for images:

* [Trekmarvel](https://github.com/Trekmarvel) for the base potion bottle graphics.
* http://opengameart.org/content/potion-bottles for the Overdrive Potion bottle image
* InvinciblePotionBottle.png, Regen2PotionBottle.png edited from base by Minege
* MegaJumpBottle.png, GigaJumpBottle.png edited from base by Patrick Wang
* Ninja Potion: https://pixabay.com/en/bottle-vector-water-bottle-1737388/
* BlindWalk Potion: BlindWalkPotionBottle.png edited from base by digitalripperynr
* Battle: https://pixabay.com/en/bottle-clear-glass-close-cork-307980/
* SuperHealPotionBottle.png : https://pixabay.com/en/erlenmeyer-flask-glassware-red-296843/
* HemlockPotion.png : Made by SufurElite.
* Sacred: SacredPotionBottle.png edited from base by smsunarto 
* Ultra Heal: https://pixabay.com/en/erlenmeyer-flask-glassware-red-296843/ (edited)(resized)
