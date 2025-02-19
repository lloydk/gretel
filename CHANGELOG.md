# Changelog

## Unreleased

## Version 4.5.0
* Use `link` element for link item in semantic markup instead of `meta` element (via #36, thanks @tkawa)
* Add `link_data` option to set data attributes for link item (via #38, thanks @SpaYco)

## Version 4.4.0
* Support Bootstrap 5. See the `:style` option in the readme for more info (via #30, thanks @tochi)
* Support Rails 7.0
* Link class is now customizable with `<%= breadcrumbs link_class: "some-class" %>`. (via #10)

## Version 4.3.0
* Support generating `aria-current` attribute. It's disabled by default. See the readme for more info

## Version 4.2.0
* Support generating JSON-LD structured data. See the readme for more info (via #26, thanks @dkniffin)

## Version 4.1.0
* Depends only `railties` and `actionview`, not `rails` (via #7)
* Include `Gretel::ViewHelpers` module in `ActiveSupport.on_load(:action_view)` block
* Fix ruby 2.7 keywords warning (via #24, thanks @aki77)
* Fix multithreaded environment issue (via #13)
  * `breadcrumbs.rb` is now evaluated in a instance of `Gretel::Crumbs::Builder`. If you want to call methods from `breadcrumbs.rb` other than `crumb`, `crumbs` and `crumb_defined?`, you need to call it via full reference like `Gretel::Crumbs.xxxx`

## Version 4.0.2
* The return value of `breadcrumbs` is `html_safe` now (via #22)
  * For the slim template engine users: You don't need to use `==` instead of `=` for `breadcrumbs`

## Version 4.0.1
* Replaces data-vocabulary markup as google doesn't support it and now uses schema.org markup (via #17)

## Version 4.0.0
* Support Bootstrap 4. See the `:style` option in the readme for more info
* CSS class for fragment link or span is now customizable. See the `:fragment_class` option in the readme for more info
* Drop support Ruby < 2.5
* Drop support Rails < 5.1
* Deprecated codes have been removed:
  * `breadcrumbs` is no longer accept block, use `tap` instead
  * `breadcrumbs` is no longer accept `style: :default`, use `style: :inline` instead
  * `breadcrumbs` is no longer accept `:show_root_alone` option, use `:display_single_fragment` option instead

## Version 3.0.9
* Adds breadcrumbs option `link_current_to_request_path` to link the current breadcrumb to the request path(#28 via #29)
* Fixes semantic breadcrumbs when the last item has no link (via #55)
* Downgrades Rails dependency to 3.1 (via #56)
* Fixes jRuby issue with `Rails::Application` constant (via #50)
* Fixes deprecation warnings for `alias_method_chain` (via #66)
* Updated coprights (via #63)

## Version 3.0.8
* Parent breadcrumbs can now also be inferred from models responding to `model_name`.

## Version 3.0.7
* Pretext and posttext classes are now customizable with `<%= breadcrumbs pretext_class: "some-class" %>` and `<%= breadcrumbs posttext_class: "some-other-class" %>`.

## Version 3.0.6
* Pretext and posttext are now enclosed in spans with `<span class="pretext">` and `<span class="posttext">`.
* Semantic breadcrumbs are now rendered in spans instead of divs to enable easier styling.

## Version 3.0.3
* Breadcrumbs can now be rendered for use in the [Foundation 5](http://foundation.zurb.com/) framework. Use `breadcrumbs style: :foundation5`.
* Breadcrumbs are now automatically loaded from any engines' `config/breadcrumbs.rb` and `config/breadcrumbs/**/*.rb`. See the readme for details.
* You can now pass options to links to be used when you render manually. See the readme for details.
* Breadcrumb configuration files can now be put in the `app/views/breadcrumbs/` folder. This is an experimental feature that may replace loading breadcrumbs from the `config` folder in the future.

## Version 3.0.2
* Inferring breadcrumbs is now supported on all instances of objects that respond to `model_name`.

## Version 3.0.1
* Breadcrumbs can now be inferred if you pass in an ActiveRecord model instance. E.g. `breadcrumb @product` is short for `breadcrumb :product, @product`.

## Version 3.0
* Support for defining breadcrumbs using `Gretel::Crumbs.layout do ... end` in an initializer has been removed. See the readme for details on how to upgrade.
* Breadcrumbs rendering is now done in a separate class to unclutter the view with helpers. The public API is still the same.
* Support for rendering the breadcrumbs in different styles like ul- and ol lists, and for use with [Twitter Bootstrap](http://getbootstrap.com/). See the `:style` option in the readme for more info.
* The `:show_root_alone` option is now called `:display_single_fragment` and can be used to display the breadcrumbs only when there are more than one link, also if it is not the root breadcrumb.
* Links yielded from `<%= breadcrumbs do |links| %>` now have a `current?` helper that returns true if the link is the last in the trail.
* New view helper: `parent_breadcrumb` returns the parent breadcrumb link (with `#key`, `#text`, and `#url`). This can for example be used to create a dynamic back link. You can supply options like `:autoroot` etc.
  If you supply a block, it will yield the parent breadcrumb if it is present.

## Version 2.1
* Breadcrumbs are now configured in `config/breadcrumbs.rb` and `config/breadcrumbs/**/*.rb` and reloaded when changed in the development environment instead of the initializer that required restart when configuration changed.

## Version 2.0

* Totally rewritten for better structure.
* `options[:autoroot]` is now `true` by default which means it will automatically link to the `:root` breadcrumb if no parent is specified.
* Now accepts `options[:class]` for specifying the CSS class for the breadcrumbs container. Default: `"breadcrumbs"`.
* Now accepts `options[:current_class]` for specifying the CSS class for the current link / span. Default: `"current"`.
* `options[:link_last]` was deprecated in a previous version and is now removed. Use `options[:link_current]` instead.
* The `link` method in `crumb :xx do ... end` no longer takes HTML options. The method for this is now by building the breadcrumbs manually (see the readme).
* No longer supports procs for link text or URL as this is unnecessary when you can pass arguments to the block anyway.
* It now accepts multiple arguments for `crumb` and `parent` (see the readme).
* Breadcrumbs are now rendered with `<%= breadcrumbs %>`, although you can still use the old `<%= breadcrumb %>` (without *s*).
* You can now access view helpers from inside `Gretel::Crumbs.layout do .. end`.
