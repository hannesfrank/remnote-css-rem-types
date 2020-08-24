# RemNote Card Type Styles

A Custom CSS for [RemNote](https://www.remnote.io/) to change how flashcard generating rems look.

![default_style](./default_style.png) ![custom_style](./custom_style.png)

**Features:**

- Color code rem types (plain, multi-line, list, set) and card types (concept, descriptor, question [and slot]).
- Visually indicate backward practice direction.

**Note:** This is only a proof of concept. See [Current Problems](#current-problems).

## Installation

1. Open the `Custom CSS` page in RemNote.
2. Create a new blank template block.
3. Paste the layout:
   1. If you want future updates and are ok with the defaults, just paste this:
      ```
      @import URL('https://cdn.jsdelivr.net/gh/hannesfrank/remnote-css-rem-types@master/card-types.css');
      ```
   2. If you want to tweak some stuff copy the style directly [from here](https://github.com/hannesfrank/remnote-css-rem-types/blob/master/card-types.css).

## Contributing

I am not a designer. This is just a proof of concept.
If you have a good design, feel free to open an Issue to discuss. You can also try Discord, but it might get lost there.

If you can improve something — e.g. fix a [Problem](#current-problems) — a Pull Request is very welcome!

## Current Problems

Right now the styling is not stable. The RemNote's markup is pretty dynamic due to heavy optimization. There are elements created and deleted whenever you hover over a Rem or focus to edit. I might have missed some cases.

There are also some difficulties with the current markup which might get fixed later:

- **Dynamic markup!** I tried to work around a bit, but for example if you hover over rems fast sometimes the hover markup sticks and there are duplicated icons.
- Concepts, descriptors and Questions have an extra tag `span.*_rem_type` with a zero-width-non-breakable space (`&#65279;`) between name and `..`. This might be a bug though. Currently it generates extra icons.
  - Btw: Slots don't.
- Card types are handled differently: For Multiline, Set and List the `:::` is virtual - you can't select it.
- Slots are handled differently than Concept, descriptor and Question. With slots the `::` marker is just text, with the other types, it has its own tag.
- Some things break if you make part of the name of a concept bold.
  - Note to self: This splits the name into multiple tags. This might be the cause why some names in my backup are lists of strings.
  - Those things still get the `.bold` tag which was fixed in [Remnote#58](https://github.com/remnoteio/remnote-issues/issues/58).
  - Styling works when not hovered. When hovered, it is removed.
- Concept etc. get removed when selecting plain, slots don't. I think plain should not remove the card status and just reset List, Set, Multiline.

### WIP: Wishlist for RemNote Team

- [ ] Remove `&#65279;` tag.
- [ ] Add class to indicate hover, unfocused.
  - There is `.rem-container-focused` for edit
  - E.g. to remove styling when hovered to make `::` editable.
- Design decision: How to handle `::` marker. Is this visual only and changable in menu or with shortcut or should it be editable as text.
  - [ ] Fix Slot handling.
  - [ ] Fix plain.

* [ ] Add a setting to disable Uppercase/lowercase convention for Concept/descriptor and `?` for Question and rely on shortcut/menu to change type.
