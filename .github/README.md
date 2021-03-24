# Includes Picture
[heading__top]:
  #includes-picture
  "&#x2B06; Builds `picture` element from FrontMatter and includes"


Builds `picture` element from FrontMatter and includes


## [![Byte size of Includes Picture][badge__main__includes_picture__source_code]][includes_picture__main__source_code] [![Open Issues][badge__issues__includes_picture]][issues__includes_picture] [![Open Pull Requests][badge__pull_requests__includes_picture]][pull_requests__includes_picture] [![Latest commits][badge__commits__includes_picture__main]][commits__includes_picture__main] [![includes-picture Demos][badge__gh_pages__includes_picture]][gh_pages__includes_picture]


---


- [:arrow_up: Top of Document][heading__top]

- [:building_construction: Requirements][heading__requirements]

- [:zap: Quick Start][heading__quick_start]
  - [:memo: Edit Your ReadMe File][heading__your_readme_file]
  - [:floppy_disk: Commit and Push][heading__commit_and_push]

- [&#x1F9F0; Usage][heading__usage]

- [:symbols: API][heading__api]

  - [`url`][heading__url]
    - [`base`][heading__urlbase]
    - [`filter`][heading__urlfilter]

  - [`img`][heading__img]
    - [`src`][heading__imgsrc]
    - [`alt`][heading__imgalt]
    - [`height`][heading__imgheight]
    - [`width`][heading__imgwidth]
    - [`loading`][heading__imgloading]
    - [`decoding`][heading__imgdecoding]

  - [`sources`][heading__sources]
    - [`srcset`][heading__sources0srcset]
    - [`media`][heading__sources0media]

- [&#x1F5D2; Notes][heading__notes]

- [:chart_with_upwards_trend: Contributing][heading__contributing]
  - [:trident: Forking][heading__forking]
  - [:currency_exchange: Sponsor][heading__sponsor]

- [:card_index: Attribution][heading__attribution]

- [:balance_scale: Licensing][heading__license]


---



## Requirements
[heading__requirements]:
  #requirements
  "&#x1F3D7; Prerequisites and/or dependencies that this project needs to function properly"


This repository depends upon [Jekyll][jekyll_rb__home] which is supported by [GitHub Pages][github_docs__github_pages__jekyll], further details about setup can be found from [documentation][jekyll_rb__github_pages] published by the Jekyll maintainers regarding GitHub Pages.


______


## Quick Start
[heading__quick_start]:
  #quick-start
  "&#9889; Perhaps as easy as one, 2.0,..."


This repository encourages the use of Git Submodules to track dependencies


**Bash Variables**


```Bash
_module_name='includes-picture'
_module_https_url="https://github.com/liquid-utilities/includes-picture.git"
_module_base_dir='_includes/modules'
_module_path="${_module_base_dir}/${_module_name}"
```


**Bash Submodule Commands**


```Bash
cd "<your-git-project-path>"


git checkout gh-pages

mkdir -vp "${_module_base_dir}"


git submodule add -b main\
                  --name "${_module_name}"\
                  "${_module_https_url}"\
                  "${_module_path}"
```


---


### Your ReadMe File
[heading__your_readme_file]:
  #your-readme-file
  "&#x1F4DD; Suggested additions for your ReadMe.md file so everyone has a good time with submodules"


Suggested additions for your _`ReadMe.md`_ file so everyone has a good time with submodules


```MarkDown
Clone with the following to avoid incomplete downloads


    git clone --recurse-submodules <url-for-your-project>


Update/upgrade submodules via


    git submodule update --init --merge --recursive
```


---


### Commit and Push
[heading__commit_and_push]:
  #commit-and-push
  "&#x1F4BE; It may be just this easy..."


```Bash
git add .gitmodules
git add "${_module_path}"


## Add any changed files too


git commit -F- <<'EOF'
:heavy_plus_sign: Adds `liquid-utilities/includes-picture#1` submodule



**Additions**


- `.gitmodules`, tracks submodules AKA Git within Git _fanciness_

- `README.md`, updates installation and updating guidance

- `_includes/modules/includes-picture`, Builds `picture` element from FrontMatter and includes
EOF


git push origin gh-pages
```


**:tada: Excellent :tada:** your project is now ready to begin unitizing code from this repository!


______


## Usage
[heading__usage]:
  #usage
  "&#x1F9F0; How to utilize this repository"


**`2021-03-24-example-picture-includes.md` (FrontMatter Snip)**


```YAML
pictures:
  funny_cat:
    url:
      base: assets/images/funny_cat/
      filter: absolute_url

    img:
      alt: Picture of a funny cat playing with yarn ball
      src: playful-yarn.jpeg
      width: 300
      height: 200
      loading: lazy
      decoding: async

    sources:
      - srcset: playful-yarn.png

      - srcset:
        - playful-yarn-480.webp
        - playful-yarn-480-2x.webp 2x
        media: '(min-width: 600px)'
```


**`2021-03-24-example-picture-includes.md` (Content Snip)**


```liquid
{% include modules/includes-picture/picture.html name='funny_cat' %}
```


> Note, the `name` parameter corresponds to the FrontMatter key under `picture` hash-map.


**`2021/03/24/example-picture-includes.html` (HTML Snip)**


```HTML
<picture>
  <source type="image/png"
          srcset="/includes-picture/assets/images/funny_cat/playful-yarn.png"
  />

  <source type="image/webp"
          srcset="/includes-picture/assets/images/funny_cat/playful-yarn-480.webp,
                  /includes-picture/assets/images/funny_cat/playful-yarn-480-2x.webp 2x"
          media="(min-width: 600px)"
  />

  <img src="/includes-picture/assets/images/funny_cat/playful-yarn.jpeg"
       height="300"
       width="200"
       alt="Picture of a funny cat playing with yarn ball"
       loading="lazy"
       decoding="async"
  />
</picture>
```


> Note, `type` is automatically parsed from first listed `srcset` path from each of listed `sources`
>
> And `height`/`width` generally should only be defined if **all** picture variants are of the same dimensions


______


## API
[heading__api]:
  #api
  "&#x1F523; Parameter documentation"


Including the `picture.html` code requires that `name` parameter be defined, and point to a name within the `pictures` name-space for either the page/post or layout, eg...


```liquid
{% include modules/includes-picture/picture.html name='left-side-bar' %}

{% include modules/includes-picture/picture.html name='right-side-bar' %}
```


... each of above refer to a `left-side-bar` and `right-side-bar` FrontMatter configuration within a `pictures` name-space, eg...


```YAML
pictures:
  left-side-bar:
    url: ...
    img: ...
    sources: ...

  right-side-bar:
    url: ...
    img: ...
    sources: ...
```


---


### `url`
[heading__url]: #url


Type: **Hash**


Optional, if defined modifies `src` and `srcset` paths


#### `url.base`
[heading__urlbase]: #urlbase


Type: **string**


Optional, if defined `url.base` will prepend each `src` and `srcset` path


> Note, **no** path dividing slash (`/`) is inserted between `url.base` and paths


#### `url.filter`
[heading__urlfilter]: #urlfilter


Type: **absolute_url** | **relative_url**


Optional, if defined each `src` and `srcset` path will be piped through the defined Liquid filter


---


### `img`
[heading__img]: #img


Type: **Hash**


Required, fallback/default for browsers that do not support `source` elements and/or when no `source` element is picked by the browser


#### `img.src`
[heading__imgsrc]: #imgsrc


Type: **string**


Required, path or URL of image file


#### `img.alt`
[heading__imgalt]: #imgalt


Type: **string**


Optional but recommend, text that describes `picture` element recommend for accessibility and SEO (Search Engine Optimization)


#### `img.height`
[heading__imgheight]: #imgheight


Type: **number**


Optional, defines height for **all** elements within named `picture` element


#### `img.width`
[heading__imgwidth]: #imgwidth


Type: **number**


Optional, defines width for **all** elements within named `picture` element


#### `img.loading`
[heading__imgloading]: #imgloading


Type: **eager** | **lazy**


Optional and requires browser has JavaScript enabled, defines priority for downloading image


#### `img.decoding`
[heading__imgdecoding]: #imgdecoding


Type: **sync** | **async** | **auto**


Optional and requires browser has JavaScript enabled, generally `async` is recommended for most use cases, default is `auto`


---


### `sources`
[heading__sources]: #sources


Type: **Array<Hash>**


Optional, define list of alternate image sources and/or formats for browser to choose


#### `sources[0].srcset`
[heading__sources0srcset]: #sources0srcset


Type: **string** | **Array<string>**


Required, list of paths or URLs (comma separated) for browser to choose for a given file type


#### `sources[0].media`
[heading__sources0media]: #sources0media


Type: **string**


Optional, CSS media query that provides further hints for browser to use for deciding when to load an image


______


## Notes
[heading__notes]:
  #notes
  "&#x1F5D2; Additional things to keep in mind when developing"


This repository may not be feature complete and/or fully functional, Pull Requests that add features or fix bugs are certainly welcomed.


______


## Contributing
[heading__contributing]:
  #contributing
  "&#x1F4C8; Options for contributing to includes-picture and liquid-utilities"


Options for contributing to includes-picture and liquid-utilities


---


### Forking
[heading__forking]:
  #forking
  "&#x1F531; Tips for forking includes-picture"


Start making a [Fork][includes_picture__fork_it] of this repository to an account that you have write permissions for.


- Add remote for fork URL. The URL syntax is _`git@github.com:<NAME>/<REPO>.git`_...


```Bash
cd ~/git/hub/liquid-utilities/includes-picture

git remote add fork git@github.com:<NAME>/includes-picture.git
```


- Commit your changes and push to your fork, eg. to fix an issue...


```Bash
cd ~/git/hub/liquid-utilities/includes-picture


git commit -F- <<'EOF'
:bug: Fixes #42 Issue


**Edits**


- `<SCRIPT-NAME>` script, fixes some bug reported in issue
EOF


git push fork main
```


> Note, the `-u` option may be used to set `fork` as the default remote, eg. _`git push -u fork main`_ however, this will also default the `fork` remote for pulling from too! Meaning that pulling updates from `origin` must be done explicitly, eg. _`git pull origin main`_


- Then on GitHub submit a Pull Request through the Web-UI, the URL syntax is _`https://github.com/<NAME>/<REPO>/pull/new/<BRANCH>`_


> Note; to decrease the chances of your Pull Request needing modifications before being accepted, please check the [dot-github](https://github.com/liquid-utilities/.github) repository for detailed contributing guidelines.


---


### Sponsor
  [heading__sponsor]:
  #sponsor
  "&#x1F4B1; Methods for financially supporting liquid-utilities that maintains includes-picture"


Thanks for even considering it!


Via Liberapay you may <sub>[![sponsor__shields_io__liberapay]][sponsor__link__liberapay]</sub> on a repeating basis.


Regardless of if you're able to financially support projects such as includes-picture that liquid-utilities maintains, please consider sharing projects that are useful with others, because one of the goals of maintaining Open Source repositories is to provide value to the community.


______


## Attribution
[heading__attribution]:
  #attribution
  "&#x1F4C7; Resources that where helpful in building this project so far."


- [GitHub -- `github-utilities/make-readme`](https://github.com/github-utilities/make-readme)

- [MDN -- HTML Element -- `picture`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture)

- [MDN -- HTML Element -- `img`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)

- [MDN -- Image file type and format guide](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Image_types)

- [MDN --MIME types (IANA media types)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types)

- [StackOverflow -- check if variable is type of string or array in liquid](https://stackoverflow.com/questions/38917552/)


______


## License
[heading__license]:
  #license
  "&#x2696; Legal side of Open Source"


```
Builds `picture` element from FrontMatter and includes
Copyright (C) 2021 S0AndS0

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published
by the Free Software Foundation, version 3 of the License.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
```


For further details review full length version of [AGPL-3.0][branch__current__license] License.



[branch__current__license]:
  /LICENSE
  "&#x2696; Full length version of AGPL-3.0 License"


[badge__commits__includes_picture__main]:
  https://img.shields.io/github/last-commit/liquid-utilities/includes-picture/main.svg

[commits__includes_picture__main]:
  https://github.com/liquid-utilities/includes-picture/commits/main
  "&#x1F4DD; History of changes on this branch"


[includes_picture__community]:
  https://github.com/liquid-utilities/includes-picture/community
  "&#x1F331; Dedicated to functioning code"

[includes_picture__gh_pages]:
  https://github.com/liquid-utilities/includes-picture/tree/
  "Source code examples hosted thanks to GitHub Pages!"

[badge__gh_pages__includes_picture]:
  https://img.shields.io/website/https/liquid-utilities.github.io/includes-picture/index.html.svg?down_color=darkorange&down_message=Offline&label=Demo&logo=Demo%20Site&up_color=success&up_message=Online

[gh_pages__includes_picture]:
  https://liquid-utilities.github.io/includes-picture/index.html
  "&#x1F52C; Check the example collection tests"

[issues__includes_picture]:
  https://github.com/liquid-utilities/includes-picture/issues
  "&#x2622; Search for and _bump_ existing issues or open new issues for project maintainer to address."

[includes_picture__fork_it]:
  https://github.com/liquid-utilities/includes-picture/
  "&#x1F531; Fork it!"

[pull_requests__includes_picture]:
  https://github.com/liquid-utilities/includes-picture/pulls
  "&#x1F3D7; Pull Request friendly, though please check the Community guidelines"

[includes_picture__main__source_code]:
  https://github.com/liquid-utilities/includes-picture/
  "&#x2328; Project source!"

[badge__issues__includes_picture]:
  https://img.shields.io/github/issues/liquid-utilities/includes-picture.svg

[badge__pull_requests__includes_picture]:
  https://img.shields.io/github/issues-pr/liquid-utilities/includes-picture.svg

[badge__main__includes_picture__source_code]:
  https://img.shields.io/github/repo-size/liquid-utilities/includes-picture


[jekyll_rb__home]:
  https://jekyllrb.com/
  "Jekyll home page"

[jekyll_rb__github_pages]:
  https://jekyllrb.com/docs/github-pages/
  "Jekyll documentation for GitHub Pages setup"

[github_docs__github_pages__jekyll]:
  https://docs.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll
  "GitHub Pages documentation on Jekyll setup"


[sponsor__shields_io__liberapay]:
  https://img.shields.io/static/v1?logo=liberapay&label=Sponsor&message=liquid-utilities

[sponsor__link__liberapay]:
  https://liberapay.com/liquid-utilities
  "&#x1F4B1; Sponsor developments and projects that liquid-utilities maintains via Liberapay"

