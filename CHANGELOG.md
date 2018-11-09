# Change Log

## 2.2.2 (2018-11-21)

### Enhancements

- Add extensions for audios (SoundCloud, Netease Cloud Music), videos (YouTube, TED, bilibili) and slide(SlideShare)
- Add sharing (AddToAny)

## 2.2.1 (2018-10-02)

### Enhancements

- Update screenshots
- landing Layout `data.sections` item's `image` add `full_width` setting
- Remove `header.type` and add `header.background` setting
- page layout sidebar use document scroll when viewport width < 1024px, this enhance the user experience on a phone or a pad
- Telegram social icon (@WangQiru)
- Search panel use dark background

## 2.2.0 (2018-09-16)

### Enhancements

- `article_header` config for Page Layout
- Articles Layout
- New grid system
- Image, card, item and hero components
- Tag additional style
- chart.js update to 2.7.2, mathjax update to 2.7.4 and mermaid update to 8.0.0-rc.8

### Bug Fixes

- replace Lenna example image

## 2.1.0 (2018-08-26)

### Enhancements

- Search panel (Click search icon in the header or press `s` or `/` key to search)
- Npm social icon (@WangQiru)

### Bug Fixes

- Google analytics may not work, use gtag.js

## 2.0.2 (2018-07-29)

### Enhancements

- Highlight theme
- Articles whit `sidebar.toc` support section navigator (previous and next navigator)
- Aside Toc show immediately after page get ready (no more delay)

### Bug Fixes

- Aside Toc may display error when scroll to bottom

## 2.0.1 (2018-07-07)

> “All elements that respond to press should have a visual feedback when touched.”
>
> —TouchableWithoutFeedback in *React Native Docs*

### Enhancements

- Some interaction details optimize: button and link add feedback when clicked, cancel button of input in archive layout, button focus style, etc

### Bug Fixes

- `mathjax` and `mermaid` config may not work

## 2.0.0 (2018-07-01)

Breaking changes, please check [Update form 1.x to 2.x](https://tianqi.name/jekyll-TeXt-theme/docs/en/update-form-1-to-2) for details

### Enhancements

- Authors
- License
- New layouts (page, article, landing, etc)

## 1.5.0 (2018-03-18)

### Enhancements

- `text_color_theme` config
- Long pagination
- Additional styles (Alert, Image)
- Mathjax autoNumber config (@liao961120)
- Article heading anchor
- Previous and next post
- Search

## 1.4.3 (2018-01-13)

### Enhancements

- New TOC style
- Gitalk support (@WangQiru)
- Mermaid support
- `site.paths` & `site.nav_lists` support absolute URL

## 1.4.2 (2017-12-10)

### Enhancements

- Use new liquid syntax `{%-` `-%}` to avoid unnecessary output whitespace
- Add paths.base config

## 1.4.1 (2017-12-05)

### Enhancements

- New color themes(Chocolate, Orange)

### Bug Fixes

- Issues 9: the _posts file can't recorded by git

## 1.4.0 (2017-11-19)

### Enhancements

- Multi-language support

### Bug Fixes

- Table overflow-x smooth on iOS

## 1.3.0 (2017-11-11)

### Enhancements

- Article tag supports special characters
- Excerpts type (HTML | TEXT)
- Titles on the phone become smaller
- Styles change (table, code, blockquote)

## 1.2.2 (2017-11-04)

### Enhancements

- MathJax Support
- Add “Read more” link at the end of article excerpt
- 404 page

### Bug Fixes

- Fix Email link URL error
- Fix Site Title link URL error
- Fix table responsive style error

## 1.2.1 (2017-10-27)

### Enhancements

- Optimize Article TOC

### Bug Fixes

- Issues 4: View count display error when the post key include `-` (@yuxianda)
- Email url error

## 1.2.0 (2017-10-22)

### Enhancements

- Article excerpt no more than 200 words
- If `leancloud` is not set, 0 view won't display

### Bug Fixes

- Fix article TOC ’s display error at proper situation
- Fix footer social buttons not in the center bug

## 1.1.0 (2017-10-19)

### Enhancements

- Color variables
- More color themes (dark, forest, ocean)

## 1.0.0 (2017-10-17)

### Enhancements

- Better article directories
- Dark color theme