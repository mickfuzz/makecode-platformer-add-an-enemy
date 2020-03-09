### @activities true

# Making a Platformer Game - Adding an Enemy

## Adding an Enemy 
### Getting Started @unplugged

This tutorial series we start with a template of a simple platformer game that you will start with and add to.
In this particular tutorial we will add a static enemy. 

If you want to understand more about how the starting code works then you can follow [this tutorial](https://arcade.makecode.com/beta#tutorial:https://github.com/mickfuzz/makecode-platformer-101)
  to create the game step by step.

If you want to add more features later you can do so with tutorials like the following:

* Adding a Moving Enemy
* Create more Levels
* Add instructions and between level comments
* Jump on Enemies to Zap them


```template
### @activities true

# Making a Platformer Game - Adding an Enemy

## Adding an Enemy 
### Getting Started @unplugged

This tutorial series we start with a template of a simple platformer game that you will start with and add to.
In this particular tutorial we will add a static enemy. 

If you want to understand more about how the starting code works then you can follow [this tutorial](https://arcade.makecode.com/beta#tutorial:https://github.com/mickfuzz/makecode-platformer-101)
  to create the game step by step.

If you want to add more features later you can do so with tutorials like the following:

* Adding a Moving Enemy
* Create more Levels
* Add instructions and between level comments
* Jump on Enemies to Zap them


```template
namespace SpriteKind {
    export const Door = SpriteKind.create()
}
namespace myTiles {
    //% blockIdentity=images._tile
    export const tile0 = img`
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
    `
    //% blockIdentity=images._tile
    export const tile1 = img`
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
    `
    //% blockIdentity=images._tile
    export const tile2 = img`
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
    `
}
function chooseLevel () {
    if (level == 0) {
        tiles.setTilemap(tiles.createTilemap(
            hex`1400080000000000000000000000000000000000000000000400030000000000000000000000000000000000010101030000000000000000000000000000000000000101000000000000000000000000000000000000000000000000000000000000000000000000000000000000000101010100000000000000000000000000000001010000000300000000030000000101010101010101010101010101010101010101`,
            img`
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . . . . . .
                2 2 2 . . . . . . . . . . . . . . . . .
                . . 2 2 . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . . 2 2 2 2 . . . . . . . . .
                . . . . . . 2 2 . . . . . . . . . . . .
                2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
            `,
            [myTiles.tile0,sprites.castle.tileGrass2,sprites.builtin.forestTiles0,myTiles.tile1,myTiles.tile2],
            TileScale.Sixteen
        ))
    }
    if (level == 1) {
        tiles.setTilemap(tiles.createTilemap(
            hex`1400080000000000000000000000000000000000000000000400000000000000000000000000000000000000010101030000000000000000000000000000000000000101000000000000000000000000000000000000000000000300000000000000000000000000000000000001010000000000000000000000000000000000000000000000000000000000000000000101010101010101010101010101010101010101`,
            img`
                . . . . . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . . . . . .
                2 2 2 . . . . . . . . . . . . . . . . .
                . . 2 2 . . . . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . . . . . .
                . . . . . 2 2 . . . . . . . . . . . . .
                . . . . . . . . . . . . . . . . . . . .
                2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
            `,
            [myTiles.tile0,sprites.castle.tileGrass2,sprites.builtin.forestTiles0,myTiles.tile1,myTiles.tile2],
            TileScale.Sixteen
        ))
    }
    if (level == 2) {
        game.over(true)
    }
}
sprites.onOverlap(SpriteKind.Player, SpriteKind.Door, function (sprite, otherSprite) {
    if (sprites.allOfKind(SpriteKind.Food).length == 0) {
        level += 1
        mySprite.setPosition(10, 100)
        createLevels()
    }
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    otherSprite.destroy()
})
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (mySprite.isHittingTile(CollisionDirection.Bottom)) {
        mySprite.vy = -175
    }
})
function createLevels () {
    chooseLevel()
    for (let value of tiles.getTilesByType(myTiles.tile1)) {
        strawberry = sprites.create(img`
            . . . . . . . 6 . . . . . . . .
            . . . . . . 8 6 6 . . . 6 8 . .
            . . . e e e 8 8 6 6 . 6 7 8 . .
            . . e 2 2 2 2 e 8 6 6 7 6 . . .
            . e 2 2 4 4 2 7 7 7 7 7 8 6 . .
            . e 2 4 4 2 6 7 7 7 6 7 6 8 8 .
            e 2 4 5 2 2 6 7 7 6 2 7 7 6 . .
            e 2 4 4 2 2 6 7 6 2 2 6 7 7 6 .
            e 2 4 2 2 2 6 6 2 2 2 e 7 7 6 .
            e 2 4 2 2 4 2 2 2 4 2 2 e 7 6 .
            e 2 4 2 2 2 2 2 2 2 2 2 e c 6 .
            e 2 2 2 2 2 2 2 4 e 2 e e c . .
            e e 2 e 2 2 4 2 2 e e e c . . .
            e e e e 2 e 2 2 e e e c . . . .
            e e e 2 e e c e c c c . . . . .
            . c c c c c c c . . . . . . . .
        `, SpriteKind.Food)
        tiles.placeOnTile(strawberry, value)
        tiles.setTileAt(value, myTiles.tile0)
    }
    for (let value2 of tiles.getTilesByType(myTiles.tile2)) {
        chest = sprites.create(img`
            . . b b b b b b b b b b b b . .
            . b e 4 4 4 4 4 4 4 4 4 4 e b .
            b e 4 4 4 4 4 4 4 4 4 4 4 4 e b
            b e 4 4 4 4 4 4 4 4 4 4 4 4 e b
            b e 4 4 4 4 4 4 4 4 4 4 4 4 e b
            b e e 4 4 4 4 4 4 4 4 4 4 e e b
            b e e e e e e e e e e e e e e b
            b e e e e e e e e e e e e e e b
            b b b b b b b d d b b b b b b b
            c b b b b b b c c b b b b b b c
            c c c c c c b c c b c c c c c c
            b e e e e e c b b c e e e e e b
            b e e e e e e e e e e e e e e b
            b c e e e e e e e e e e e e c b
            b b b b b b b b b b b b b b b b
            . b b . . . . . . . . . . b b .
        `, SpriteKind.Door)
        tiles.placeOnTile(chest, value2)
        tiles.setTileAt(value2, myTiles.tile0)
    }
}
let chest: Sprite = null
let strawberry: Sprite = null
let level = 0
let mySprite: Sprite = null
mySprite = sprites.create(img`
    . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . .
    . . . . . . . . . b 5 5 b . . .
    . . . . . . b b b b b b . . . .
    . . . . . b b 5 5 5 5 5 b . . .
    . b b b b b 5 5 5 5 5 5 5 b . .
    . b d 5 b 5 5 5 5 5 5 5 5 b . .
    . . b 5 5 b 5 d 1 f 5 d 4 f . .
    . . b d 5 5 b 1 f f 5 4 4 c . .
    b b d b 5 5 5 d f b 4 4 4 4 b .
    b d d c d 5 5 b 5 4 4 4 4 4 4 b
    c d d d c c b 5 5 5 5 5 5 5 b .
    c b d d d d d 5 5 5 5 5 5 5 b .
    . c d d d d d d 5 5 5 5 5 d b .
    . . c b d d d d d 5 5 5 b b . .
    . . . c c c c c c c c b b . . .
`, SpriteKind.Player)
controller.moveSprite(mySprite, 100, 0)
mySprite.ay = 350
mySprite.setPosition(10, 100)
scene.cameraFollowSprite(mySprite)
scene.setBackgroundColor(9)
level = 0
createLevels()

```

## Understanding the existing patterns 

### We add enemies like we add food. @fullscreen

We add enemies to the game the same way we add the strawberry food. 
**We use a loop** (to save time) that turns all the yellow squares in a tile map into a sprite of kind Food. 
Find the following loop in the code. 
```block 

namespace myTiles {
    //% blockIdentity=images._tile
    export const tile0 = img`
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
    `
    //% blockIdentity=images._tile
    export const tile1 = img`
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
    `
    //% blockIdentity=images._tile
    export const tile2 = img`
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
    `
}
let strawberry: Sprite = null
for (let value of tiles.getTilesByType(myTiles.tile1)) {
    strawberry = sprites.create(img`
        . . . . . . . 6 . . . . . . . .
        . . . . . . 8 6 6 . . . 6 8 . .
        . . . e e e 8 8 6 6 . 6 7 8 . .
        . . e 2 2 2 2 e 8 6 6 7 6 . . .
        . e 2 2 4 4 2 7 7 7 7 7 8 6 . .
        . e 2 4 4 2 6 7 7 7 6 7 6 8 8 .
        e 2 4 5 2 2 6 7 7 6 2 7 7 6 . .
        e 2 4 4 2 2 6 7 6 2 2 6 7 7 6 .
        e 2 4 2 2 2 6 6 2 2 2 e 7 7 6 .
        e 2 4 2 2 4 2 2 2 4 2 2 e 7 6 .
        e 2 4 2 2 2 2 2 2 2 2 2 e c 6 .
        e 2 2 2 2 2 2 2 4 e 2 e e c . .
        e e 2 e 2 2 4 2 2 e e e c . . .
        e e e e 2 e 2 2 e e e c . . . .
        e e e 2 e e c e c c c . . . . .
        . c c c c c c c . . . . . . . .
    `, SpriteKind.Food)
    tiles.placeOnTile(strawberry, value)
    tiles.setTileAt(value, myTiles.tile0)
}

```


### We add enemies like we add food. @fullscreen
For first line here reads ``||loops:for element value of array of all...||``
it contains a value and a list. The loop keeps running until it runs out of a values in the list. 
This means it will create one item of Food for every yellow block. 
Duplicate this code block. Drop the copied loop back into the function after the original one. 

![Duplicate loop ](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-add-an-enemy/master/images/duplicate_loop_ae_1.png)

```

## Understanding the existing patterns 

### We add enemies like we add food. @fullscreen

We add enemies to the game the same way we add the strawberry food. 
**We use a loop** (to save time) that turns all the yellow squares in a tile map into a sprite of kind Food. 
Find the following loop in the code. 
```block 

namespace myTiles {
    //% blockIdentity=images._tile
    export const tile0 = img`
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
        . . . . . . . . . . . . . . . .
    `
    //% blockIdentity=images._tile
    export const tile1 = img`
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
        5 5 5 5 5 5 5 5 5 5 5 5 5 5 5 5
    `
    //% blockIdentity=images._tile
    export const tile2 = img`
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
        4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4
    `
}
let strawberry: Sprite = null
for (let value of tiles.getTilesByType(myTiles.tile1)) {
    strawberry = sprites.create(img`
        . . . . . . . 6 . . . . . . . .
        . . . . . . 8 6 6 . . . 6 8 . .
        . . . e e e 8 8 6 6 . 6 7 8 . .
        . . e 2 2 2 2 e 8 6 6 7 6 . . .
        . e 2 2 4 4 2 7 7 7 7 7 8 6 . .
        . e 2 4 4 2 6 7 7 7 6 7 6 8 8 .
        e 2 4 5 2 2 6 7 7 6 2 7 7 6 . .
        e 2 4 4 2 2 6 7 6 2 2 6 7 7 6 .
        e 2 4 2 2 2 6 6 2 2 2 e 7 7 6 .
        e 2 4 2 2 4 2 2 2 4 2 2 e 7 6 .
        e 2 4 2 2 2 2 2 2 2 2 2 e c 6 .
        e 2 2 2 2 2 2 2 4 e 2 e e c . .
        e e 2 e 2 2 4 2 2 e e e c . . .
        e e e e 2 e 2 2 e e e c . . . .
        e e e 2 e e c e c c c . . . . .
        . c c c c c c c . . . . . . . .
    `, SpriteKind.Food)
    tiles.placeOnTile(strawberry, value)
    tiles.setTileAt(value, myTiles.tile0)
}

```


### We add enemies like we add food. @fullscreen
For first line here reads ``||loops:for element value of array of all...||``
it contains a value and a list. The loop keeps running until it runs out of a values in the list. 
This means it will create one item of Food for every yellow block. 
Duplicate this code block. Drop the copied loop back into the function after the original one. 

![Duplicate loop ](https://raw.githubusercontent.com/mickfuzz/makecode-platformer-add-an-enemy/master/images/duplicate_loop_ae_1.png)