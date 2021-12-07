# Discord RPC + Buttons

This is a fork of the [discord/discord-rpc](https://github.com/discord/discord-rpc) repository. I just modified a few bits to support buttons with rich presence.

You can use up to 2 buttons: I added the variables `button1_label`, `button1_url`, `button2_label` and `button2_url` to the `DiscordRichPresence` struct, declared in include/discord_rpc.h. As I didn't found much documentation on how to implement it, I looked at the one used in the [hipvpitsme/discord-rpc-with-buttons](https://github.com/hipvpitsme/discord-rpc-with-buttons) repo, and based off that, I modified the original C++ code. I needed a C++ implementation for my purposes.

Either of each pair of fields can be used to add one button, or both at the same time for 2, of course. Be sure to provide both the label and the url for a button, as otherwise it won't be shown.
The url provided for a button also needs to be "valid". I tested that if you provide a label for a button and the url is just "hello" for example, the presence update will be completely ignored. I did add some checks so this won't happen when you don't provide the fields for the buttons properly as explained before, so it just doesn't show the button(s), but I didn't for the validity of a link.

In short, just check the provided urls to be valid, or the presence won't be updated. But if you mess up with providing some empty fields for the button(s), they just won't be shown.

The reason to not add a check for the links, so it just won't show the buttons in case an invalid link is provided, it's simply I don't know how Discord figures out how a link is valid or not. Though, I may or may not add a check myself in the future, but it might exclude some links that Discord would've thought were valid.

For more information about the rest of the repo, you can just check out the original.

For compilation, I've been using the cmake instructions originally provided. I'll keep them below for reference.

### Compilation from repo

First-eth, you'll want `CMake`. There's a few different ways to install it on your system, and you should refer to [their website](https://cmake.org/install/). Many package managers provide ways of installing CMake as well.

To make sure it's installed correctly, type `cmake --version` into your flavor of terminal/cmd. If you get a response with a version number, you're good to go!

There's a [CMake](https://cmake.org/download/) file that should be able to generate the lib for you; Sometimes I use it like this:

```sh
    cd <path to discord-rpc>
    mkdir build
    cd build
    cmake .. -DCMAKE_INSTALL_PREFIX=<path to install discord-rpc to>
    cmake --build . --config Release --target install
```
