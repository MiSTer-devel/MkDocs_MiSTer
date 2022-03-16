# MiSTer FPGA MkDocs contribution info
Try your best to follow along with the general structure of folders (categories) and the quality of the articles. Remember, quality over quantity. :)

It's very easy to contribute, just fork this repo, make your changes (such as making a new markdown file or editing one) and follow normal markdown syntax, commit changes to your fork, submit your pull request, and we will review it to see if it's suitable to merge.

https://MiSTer-devel.github.io/MkDocs_MiSTer/editing/

## Style guide
Any internally facing links must be relative links. `./docs` is the implicit root folder, so if you want to link to the assets folder you just need to use `/assets/` and type in the file that you want to link to in there.

Any externally facing links need to use "open link in new tab" by default, so as not to confuse the user and keep them on their setup step, reduce the need to click "back", etc... This is enabled by the `- attr_list` extension. To do this, just add `{target=_blank}` to the end of your link. e.g.:

`[DE10-Nano](http://de10-nano.terasic.com){target=_blank}`

Make images links when it may benefit the user. Here is the syntax:

`[![Download Mr. Fusion](dl-mr-fusion.png)](https://github.com/MiSTer-devel/mr-fusion/releases){target=_blank}`

To embed a video:

`![type:video](videos/downloader.mp4)`

To link to another doc with a specific sub-url:

`[WiFi tutorial](wifi.md#setup-wifi-with-a-script)`
