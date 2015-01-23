# scss-animated-radios-mixin
Provides a mixin for pretty scss radios to replace your old clunky ones.
built specifically to work with drupal form output, but is not specific

USAGE

The html structure required is as follows:

    <div class="parent-element">
        <label>Animated Radios </label>
        <div>
            <div>
                <input type="radio" id="input-id-must-match-label-for-0" name="name_attribute_must_match_other_input" />
                <label for="input-id-must-match-label-for-0"><span>OFF</span> </label>
            </div>
            <div>
                <input type="radio" id="input-id-must-match-label-for-1" name="name_attribute_must_match_other_input" checked="checked" />
                <label for="input-id-must-match-label-for-1"><span>ON</span> </label>
            </div>
        </div>
    </div>

    This is also just general good radio structure. matched input ids/label names allow you to click on the label to select the name


in scss, include our mixin
@import "mixin";

then, call mixin inside any section similar to class parent-element above (.form-type-radios in drupal).

.parent-element {
  @include animated-radio();
}

If you don't already have it, you will need to include the following compass library:

@import "compass/css3";     // Use one CSS3 mixin instead of multiple vendor prefixes.

OPTIONS

Available options and defaults are as follows:

  @include animated-radio(
    $transition-time: 1s,
    $width: 41,
    $labelwidth: 100,
    $border-radius: 10px,
    $leftbackground: #ffffff,
    $rightbackground: #248cf4,
    $leftcolor: #000000,
    $rightcolor: #ffffff
  );

  If you need more customizeability, you may as well alter the mixin to suite your needs.


HOW IT WORKS:

This mixin hides the input elements, which are provided by the OS's graphics and can therefore vary.
It instead relies on the next-sibling selector (+) and the input's :checked pseudoclass to tell which side is active.
The slider is an :after pseudoelement, and there is a complimentary :before pseudoelement with a z-index that varies based on its input's checked status.
Because a click on either pseudoelement is a click on the label (which is a click on the input if html is set correctly),
clicking anywhere on the radio will change the state -- the non-selected pseudoelements are always on top.
beyond that, css transitions apply the effect.

TODO: Adjust invisible layer to not move but just sit on top when necessary
TODO: check on other browsers
TODO: possibly include additional types of JS-free animated form items.