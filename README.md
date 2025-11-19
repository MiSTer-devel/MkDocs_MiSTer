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

In the root folder of this repo, create a [virtual environment](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/), activate it, and update pip:

```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install --upgrade pip
```

We can now install our requirements in the new virtual environment:
```
python3 -m pip install -r requirements.txt
```
Run a local server from the root folder:
```
mkdocs serve
```
The server can also detect changes and refresh the pages as you edit them:
```
mkdocs serve --watch docs
```
And it should give you a weburl in the terminal to go to --> http://127.0.0.1:8000

Note: video files are stored in a separate branch named `videos`. This is to make it easier to clone quickly with the command `git clone --depth 1 https://github.com/MiSTer-devel/MkDocs_MiSTer.git`. Thanks to @agg23 for the suggestion.

## Credits

Huge thanks to [@tofukazoo](https://github.com/tofukazoo) (Jorge González) for helping me with the initial GitHub automation, lots of conceptual brainstorming, important early-stage debating, and finally the motivation and encouragement to get this project going!

Thanks to [@Kitrinx](https://github.com/Kitrinx/), [@sentientsix](https://github.com/sentientsix), [@alanswx](https://github.com/alanswx/), [@MiSTerAddons](https://github.com/misteraddons), [@Tonurics](https://github.com/tonurics/), [@theypsilon](https://github.com/theypsilon/), and many more for so much help and advice with the content written and with the initial layout!

Thanks to [@hewhoisred](https://github.com/hewhoisred) for supplying art and giving expert UI design and aesthetics advice!

Thanks to Conrad Fenech for the logo design!

Thanks to [@sorgelig](https://github.com/sorgelig/) (Alexey Melnikov) for all of his amazing hard work on the MiSTer FPGA project that we all are so happy to enjoy!
