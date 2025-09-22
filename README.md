# Shift - A Simple and Easy Spritesheet Animation Library!

In my attempts to make a simple animation script for spritesheets I came up with Shift.


## Steps

1.  Declare a ShiftData object.
2.  Set the delay of the animation using the double `ShiftData::delay`. (Default is 0.15)
3.  Push back a rectangle `<left, top, width, height>` into the vector `ShiftData::rect`.
4.  Repeat step 3 for as many frame rects as needed.
5.  To access the animating rectangle frames, simply call the function `Shift(ShiftData &shift)` to receive the current rect.

## Suggestions

Modification to this library might prove beneficial in terms of ease if you change the used rect type to the type of your choosing. If, for example, you are using SFML, it would be simpler to change the `ShiftRect` type to `sf::IntRect` so that `sf::Sprite` can take the rects like so: `sprite.setTextureRect(Shift(shift));`. Since there is no single standard for rectangle data types, replacing the rect with the type needed might be necessary.

## Example Code

```cpp
// Shift library modified to use SFML's sf::IntRect instead of ShiftRect

int main()
{
    sf::Texture texture;
    texture.loadFromFile("spritesheet.png");
    sf::Sprite sprite;
    sprite.setTexture(texture);

    ShiftData shift;
    shift.delay = 0.15;
    shift.rect.push_back({237,437,120,102});
    shift.rect.push_back({127,1237,110,123});
    shift.rect.push_back({360,1237,119,124});
    shift.rect.push_back({335,342,124,95});
    shift.rect.push_back({324,761,99,116});
    shift.rect.push_back({230,877,106,117});

    sf::RenderWindow window(sf::VideoMode(960, 540), "");

    while (window.isOpen())
    {
        sf::Event event;
        while (window.pollEvent(event))
        {
            if (event.type == sf::Event::Closed)
                window.close();
        }

        window.clear();
        sprite.setTextureRect(Shift(shift));
        window.draw(sprite);
        window.display();
    }
}
