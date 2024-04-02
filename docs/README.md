## What it does

This project generates cards for spells, items, or monsters for RPG games. The generator is web-based and runs in your browser, there is no need to install any software. The cards are packed on an A4 page such that you can print it double sided and get cards with a front and back. Here's an example of what you can create:

<div align="center">
    <img src="images/front.png" alt="front">
    <img src="images/back.png" alt="back">
</div>

You can define the content of the cards yourself using simple JSON data. The above example was generated from the data shown below. Don't worry if you don't want to edit the raw data - there is a simple user interface for creating the cards.

```json
{
    "count": 1,
    "color": "maroon",
    "title": "Burning Hands",
    "icon": "book-cover",
    "contents": [
        "subtitle | 1st level evocation",
        "rule",
        "property | Casting time | 1 action",
        "property | Range | Self (15ft cone)",
        "property | Components | V, S",
        "rule",
        "fill | 1",
        "text | Each creature in a 15-foot cone takes 3d6 fire damage.",
        "text | The fire ignites any flammable objects in the area.",
        "fill | 3",
        "section | At higher levels",
        "text | +1d6 damage for each slot above 1st"
    ]
}
```

## Live demo

[Try it out yourself.](https://dungeons-and-pi.github.io/rpg-cards/) Press "Load sample" in the menu, then press "Generate" and have a look at the newly opened window/tab that contains all the generated cards.

# Documentation

This is not a complete documentation, but some information that should help you get started.

## Card JSON data

* `count` The number of times this card is repeated. Useful for consumable items that you hand out multiple times.
* `color` Name of the card color. You can use all [CSS color names](http://www.w3schools.com/cssref/css_colornames.asp).
* `icon` Name of the card icon. You can use most icons from [game-icons.net](http://game-icons.net/). For example, the file name of [this dagger](http://game-icons.net/lorc/originals/plain-dagger.html) is "plain-dagger.png", so you would use "plain-dagger" as the icon name. Additional custom icon names are defined in `css/custom-icons.css`.
* `icon_back` Optional. Name of the big icon on the card back. If not specified, the icon from the "icon" property is used.
* `background_image` Optional. URL of a backgound image for the card back. If specified, replaces the back icon.
* `title` The title of the card.
* `contents` An array of strings, specifying all card elements, in top to bottom order (see below).

### Card elements

Each card element is a string of the following format:

```txt
"element | param1 | param2 | ..."
```

HTML code is supported.

The following elements are available:

* `subtitle` Slightly larger italic text.
  * *Param1* - the subtitle text.
  * *Param2* - right aligned additional content.
* `rule` A horizontal rule.
* `property` A property line. The property description is indented if it spans more than one line.
  * *Param1* - the property name (in bold).
  * *Param2* - the property description.
* `description` Same as property, but text is not indented.
* `text` A simple paragraph of text.
  * *Param1* - the text.
* `section` A subsection header, with a horizontal rule below the subsection name.
  * *Param1* - the subsection name.
  * *Param2* - right aligned additional content.
* `boxes` A line full of empty boxes. Useful for items with charges and actions with limited use.
  * *Param1* - number of boxes.
  * *Param2* - size of a box (in "em" css unit, where 1.0 is the size of the letter 'e').
  * *Param3* - text.
* `dndstats` A Dungeons&Dragons stat block.
  * *Param1* - Strength score.
  * *Param2* - Dexterity score.
  * *Param3* - Constitution score.
  * *Param4* - Intelligence score.
  * *Param5* - Wisdom score.
  * *Param6* - Charisma score.
* `swstats` A Savage Worlds stat block.
  * *Param1* - Agility dice.
  * *Param2* - Smarts dice.
  * *Param3* - Spirit dice.
  * *Param4* - Strength dice.
  * *Param5* - Vigor dice.
  * *Param6* - Pace score.
  * *Param7* - Parry score.
  * *Param8* - Toughness score.
  * *Param9* - Loot value.
* `fill` A dynamically resized empty element that takes up a portion of unused space on the card. You can use this to vertically center text by adding one of these before and after the text you want to center.
  * *Param1* - the number of units of empty space to use.
* `bullet` A bulleted text line.
  * *Param1* - the text.
* `picture` An inline picture.
  * *Param1* - URL of the picture.
  * *Param2* - Height in pixels.

### Pathfinder 2nd Edition Card Elements

#### Custom icons

Custom icons for Actions have been added. You may use them as "Icons" (front of the card) and "Back icon" (back of the card).

* `p2e-1-action`
* `p2e-2-actions`
* `p2e-3-actions`
* `p2e-free-action`
* `p2e-reaction`

#### Attributes, Saving Throws, Armor Class and Hit Points

It shows this information in a similar way you can find Monsters and Creatures in the books.

* `p2e_stats` A Pathfinder 2nd Edition stat block, similar to the ones you find in the books.
  * *Param1* - Strength score.
  * *Param2* - Dexterity score.
  * *Param3* - Constitution score.
  * *Param4* - Intelligence score.
  * *Param5* - Wisdom score.
  * *Param6* - Charisma score.
  * *Param7* - Armor Class score.
  * *Param8* - Fortitude score.
  * *Param9* - Reflex score.
  * *Param10* - Will score.
  * *Param11* - Hit Points score.

#### Activities

Displayed in a similar way to the "Property" card element, except it accepts one more parameter for the amount of actions you need to perform the activity.

* `p2e_activity` A Pathfinder 2nd Edition stat block, similar to the ones you find in the books.
  * *Param1* - Action name.
  * *Param2* - Amount of actions needed (0, 1, 2, 3, R).
  * *Param3* - Action Description.

#### Traits

You can have "trait" badges in in your cards.

* `p2e_start_trait_section` - Start of traits section. Required when you want to have traits in your cards.
* `p2e_trait` - Shows a trait.
  * *Param1* - Trait rarity (common, uncommon, size, alignment).
  * *Param2* - Trait text.
* `p2e_end_trait_section` - End of traits section. Required when you want to have traits in your cards.

#### Other Pathfinder 2nd Edition Card Elements

Some other card elements you may find useful while creating Pathfinder 2nd Edition themed cards.

* `ruler` - Creates a single, thin black line for content separation.

### Special tags

You can use special non-standard HTML tags created especially for this card editor:

<tag param1="" param2="" ...>\
The following special HTML tags are available:

* `icon` Prints a Game Icon using the [gameicons-font](https://github.com/seiyria/gameicons-font).
  * *name* - the name of the icon.
  * *size* - size of the icon (in "pt" css unit).

## FAQ

### Can I change the layout of the cards?

You'll need to edit the CSS and Javascript files to change the layout at this point. I might add some customization options later on.
