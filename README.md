# console-theme

[![Gem Version](https://badge.fury.io/rb/console-theme.svg)](https://badge.fury.io/rb/console-theme)

For a demo, please [click here](http://jaehee0113.github.io/console).

![alt tag](http://jaehee0113.github.io/console/screenshot.png)

This is a simple yet powerful theme that will make your website look really stylish. This theme is especially suitable for users who would want to focus on writing blogs instead of working on front-end stuffs.

The primary features of this theme are:
* Gulp
* Post search functionality
* svg symbol functionality (plugin)
* string original type check functionality (plugin)
* Rake to create a post
* txtpen integration
* Disqus integration (with each post having its unique identifier)
* Color customization functionality
* Categorization (data-driven)
* Offcanvas menu
* Pagination functionality (utilises jekyll-paginate as well as jquery paginator)
* Internationalization (uses jekyll-polyglot)
* SEO (uses jekyll-seo-tag)

There are more features to come. Stay tuned!

# Table of Contents

* [Installation](#installation)
  * [Gulp Settings](#gulp-settings)
  * [Using a BrowserSync instead of Jekyll generated local server](#why-browsersync)
* [Usage](#usage)
  * [Creating a post](#create-post)
  * [Integrating Disqus with your website](#integrate-disqus)
  * [Integrating txtpen with your website](#integrate-txtpen)
  * [Using svg symbol](#use-svg-symbol)
  * [Adding more languages](#add-languages)
* [Categorization](#categorization)
* [Layouts and Blocks](#layout-block)
* [Stylesheets](#stylesheets)
* [Why some pages need to use folder structure](#why-use-folder-structure)
* [Contributing](#contributing)
* [Development](#development)
* [License](#license)

## Installation
<div id='installation'></div>

Add this line to your Jekyll site's Gemfile:

```ruby
gem "console-theme"
```

And add this line to your Jekyll site's `_config.yml`:

```yaml
theme: console-theme
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install console-theme

## Gulp settings
<div id='gulp-settings'></div>

To be able to use Gulp, you will need to install Node.js as well as its package manager (i.e. npm). Once you have installed npm. Go to the folder where the package.json is located and run `npm install` and it will install all the dependencies including Gulp.

    $ npm install

When running `gulp` command, it will run the default gulp task. Make sure to run the following command when you are in the folder that has `gulpfile.js`.

    $ gulp

This task would run several other tasks defined in `gulpfile.js.` To run individual tasks, please type `gulp [task name]`. For example:

    $ gulp minify-css

### Using a BrowserSync instead of Jekyll generated local server.
<div id='why-browsersync'></div>

When running Jekyll serve, it is possible to run a server. However, I chose to use BrowserSync instead of that for few reasons:

* BrowserSync is a de-facto standard nowadays.
* It is used with Gulp and Gulp provides bundling as well as minifying, which based on my knowledge is not possible with Jekyll generated server.

Therefore, please do use gulp!

## Usage
<div id='usage'></div>

### Creating a post
<div id='create-post'></div>

Please use `rake` command to create a post. Using this command would automatically generate Jekyll front matter with a unique Disqus identifier. The syntax for rake command is [assuming that you are in the root folder]:

```ruby
rake post title="Title" [date="2017-01-13"] [category="category"]
```

[] are optionals.

### Integrating Disqus with your website.
<div id='integrate-disqus'></div>

You will need to first have Disqus account. Once the account is ready, please modify `config.yml` file by adding your shortname for disqus like below:

```yaml
disqus_shortname: [your short name. Remove the bracket!]
```

By doing this, every disqus script would use that information and disqus identifier to fetch relevant data.

### Integrating txtpen with your website.
<div id='integrate-txtpen'></div>

You will need to first have txtpen account. Once the account is ready, please modify `config.yml` file by adding your sitename for txtpen like below:

```yaml
txtpen_sitename: [your site name. Remove the bracket!]
```

### Using svg symbol
<div id='use-svg-symbol'></div>

Using svg symbol is a good practice. By doing this, we can organize svgs better while not losing the caching functionality. Make sure you change your svg file to the file that conforms to the svg symbol style:

```html
<svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
  <symbol id="beaker" viewBox="214.7 0 182.6 792">
    <circle cx="344.8" cy="20.2" r="20.2"/>
    <circle cx="344.8" cy="92.9" r="20.2"/>
    <circle cx="320.5" cy="169.7" r="24.2"/>
    <circle cx="243" cy="141.4" r="24.2"/>
    <circle cx="284.2" cy="56.6" r="36.4"/>
  </symbol>
</svg>
```

If we would like to use this, we use svgicon tag by:

```liquid
{% svgicon beaker %}
```

This would display beaker on the screen! Examples are available.

This external svg file is located in: `assets/css/images/graphics/svg-symbols.svg`

### Adding more languages
<div id='add-languages'></div>

This theme uses `jekyll-polyglot` plugin with the plugin I developed. I have already initiated the internationalization work. The partially translated languages are: English, German and Korean. To add languages, simply add the language acronym (e.g. German is de ('Deutsch') but really you can define your own acronym) to languages variable in `_config.yml` (e.g. `languages: ["en", "de", "ko"]`). To add more languages, you would need to do the following:

1. **`localization.json`**: this is a nested json object file. The key represents the id for each translation and the value would have another key-value object with its key repesenting language acronym and the value being the translated word.

2. **`search.js`**: this may later be integrated with `localization.json` file but at the moment it is separate. In this js file, you will see `populateJSON()` function. The translation json in this function will be used in search.html. To add more languages, you need to modify this function.

The above files will then be used by the plugin called **Localization** (i.e. `_plugins/localize.rb`) and to use this simply:

```liquid
{% localize [key_id] %}
```

Explore the files and you will see plenty of examples. The plugin will automatically detect the language currently being used and then translate the word according to the one defined in `localization.json`.

## Categorization
<div id='categorization'></div>

This theme uses data-driven categorization, which makes the construction of categoization simple and succinct. The json file for category is located in _data/categories.json. Each category has three attributes: title, href and id (used to uniquely identify them). Please view the sample file to get a sense of it.

To create the category pages, you need to create a 'category' folder and subfolders would be the name of categories. They can be further nested (i.e. sub categories). Each folder would have index.md (as we will be using folder structure for creating the page for category.) You can reference my website or refer to the examples provided.

## Layouts and Blocks
<div id='layout-block'></div>

This theme values simplicity. As such, every layout would look extremely analogous with each other. However, for extensibility there are about 7 layouts:

* category
* default
* main
* page
* post
* search
* home

These layouts share same blocks, which are defined in _includes folder. There are about 10 blocks:

* **category**: the block that displays the available categories.
* **comment**: the comment block, which would be visible if comment: true in the front matter for posts.
* **footer**: the footer area.
* **global**: the global menu area.
* **head**: corresponds to the head tag in html.
* **header**: the header area. This area usually shows the location of particular page.
* **home**: corresponds the index.html
* **navigation**: the block for the menu.
* **not_found**: for 404 page.
* **search**: the block for search.

## Stylesheets
<div id='stylesheets'></div>

Jekyll uses sass, which is a scripting language that would be interpreted into css files. They are largely divided into three usages:

* **blocks**: the rest. The files are well separated. ( I think. )
* **configurations**: color settings and foundation styling will be here.
* **mixins**: self-explanatory. The breakpoint would be set here for responsive web design.

Based on your needs, you may modify these files.

## Why some pages need to use folder structure
<div id='why-use-folder-structure'></div>

To create a page, there are few ways to achieve it. One of the solutions would be to use folder structure. For example, if we were to create a page called 'archive', then you can create the folder called 'archive' and then include index.html.  For pages that use jekyll-paginate functionality, it is mandatory to use this. Otherwise, the functionality would not work. Please do not use .md extension. Use `.html` only as it would not work if this extension is not used.

## Contributing
<div id='contributing'></div>

Bug reports and pull requests are welcome on GitHub at https://github.com/jaehee0113/console. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## Development
<div id='development'></div>

To set up your environment to develop this theme, run `bundle install`.

Your theme is setup just like a normal Jekyll site! To test your theme, run `bundle exec jekyll serve` and open your browser at `http://localhost:4000`. This starts a Jekyll server using your theme. Add pages, documents, data, etc. like normal to test your theme's contents. As you make modifications to your theme and to your content, your site will regenerate and you should see the changes in the browser after a refresh, just like normal.

When your theme is released, only the files in `_layouts`, `_includes`, and `_sass` tracked with Git will be released.

## License
<div id='license'></div>

The theme is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
