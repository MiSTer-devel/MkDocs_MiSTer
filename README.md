# MkDocs_MiSTer

https://MiSTer-devel.github.io/MkDocs_MiSTer/

MiSTer FPGA Documentation built in Material for MkDocs.

## Useful resources

* https://www.markdownguide.org/tools/mkdocs/ - Good guide on how to use markdown in mkdocs.
* https://www.mkdocs.org/user-guide/writing-your-docs/ - MkDocs reference

## Software used

* https://squidfunk.github.io/mkdocs-material/ - The static site generator used for this documentation site. (MIT License)
* https://github.com/byrnereese/mkdocs-minify-plugin - Minify plugin used. (MIT License)
* https://github.com/datarobot/mkdocs-redirects - Redirects plugin used. (MIT License)
* https://github.com/soulless-viewer/mkdocs-video - Embedded video plugin used. (MIT License)
* https://github.com/timvink/mkdocs-git-revision-date-localized-plugin - Git revision date plugin used. (MIT License)
* https://github.com/Guts/mkdocs-rss-plugin - RSS plugin used. (GPL 3.0 License)

## Instructions for deploying a local environment

Prerequisites:
* Python 3
* Pip

Make sure you update [python 3](https://www.python.org/downloads/) and [update pip](https://pip.pypa.io/en/stable/installation/). Then, `cd` into the root folder of this repo and install these modules:
```
pip install mkdocs mkdocs-material mkdocs-minify-plugin mkdocs-redirects mkdocs-video mkdocs-git-revision-date-localized-plugin mkdocs-rss-plugin
```
Deploy to local server from that root folder:
```
mkdocs serve
```
And it should give you a weburl in the terminal to go to --> http://127.0.0.1:8000

## Credits

Huge thanks to [@tofukazoo](https://github.com/tofukazoo) (Jorge González) for helping me with the initial GitHub automation, lots of conceptual brainstorming, important early-stage debating, and finally the motivation and encouragement to get this project going!

Thanks to [@Kitrinx](https://github.com/Kitrinx/), [@sentientsix](https://github.com/sentientsix), [@alanswx](https://github.com/alanswx/), [@MiSTerAddons](https://github.com/misteraddons), [@Tonurics](https://github.com/tonurics/), [@theypsilon](https://github.com/theypsilon/), and many more for so much help and advice with the content written and with the initial layout!

Thanks to [@hewhoisred](https://github.com/hewhoisred) for supplying art and giving expert UI design and aesthetics advice!

Thanks to [@sorgelig](https://github.com/sorgelig/) (Alexey Melnikov) for all of his amazing hard work on the MiSTer FPGA project that we all are so happy to enjoy!
