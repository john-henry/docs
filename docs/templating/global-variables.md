# Global Variables

Every single template is going to get loaded with the following variables:

## `craft`

A [craft\web\twig\variables\CraftVariable](https://docs.craftcms.com/api/v3/craft-web-twig-variables-craftvariable.html) object, which provides access points to various helper functions and objects for templates.

### `craft.app`

A reference to the main [craft\web\Application](https://docs.craftcms.com/api/v3/craft-web-application.html) instance (the thing you get when you type `Craft::$app` in PHP code) is also available to templates via `craft.app`.

::: danger
Accessing things via `craft.app` is considered highly advanced. There are more security implications than other Twig-specific variables and functions, and your templates will be more susceptible to breaking changes during major Craft version bumps.
:::

```twig
{% if craft.app.config.general.devMode %}
    <p>This site is running in Dev Mode.</p>
{% endif %}
```  

## `currentSite`

The requested site, represented by a [craft\models\Site](https://docs.craftcms.com/api/v3/craft-models-site.html) object.

```twig
{{ currentSite.name }}
```

You can access all of the sites in the same group as the current site via `currentSite.group.sites`:

```twig
<nav>
    <ul>
        {% for site in currentSite.group.sites %}
            <li><a href="{{ alias(site.baseUrl) }}">{{ site.name }}</a></li> 
        {% endfor %}
    </ul>
</nav>
```

## `currentUser`

The currently-logged-in user, represented by a [craft\elements\User](https://docs.craftcms.com/api/v3/craft-elements-user.html) object, or `null` if no one is logged in.

```twig
{% if currentUser %}
    Welcome, {{ currentUser.friendlyName }}!
{% endif %}
```

## `loginUrl`

The URL to your site’s login page, based on the [loginPath](https://docs.craftcms.com/api/v3/craft-config-generalconfig.html#$loginPath-detail) config setting.

```twig
{% if not currentUser %}
    <a href="{{ loginUrl }}">Login</a>
{% endif %}
```

## `logoutUrl`

The URL Craft uses to log users out, based on the [logoutPath](https://docs.craftcms.com/api/v3/craft-config-generalconfig.html#$logoutPath-detail) config setting. Note that Craft will automatically redirect users to your homepage after going here; there’s no such thing as a “logout _page_”.

```twig
{% if currentUser %}
    <a href="{{ logoutUrl }}">Logout</a>
{% endif %}
```

## `now`

A [DateTime](http://php.net/manual/en/class.datetime.php) object set to the current date and time.

```twig
Today is {{ now|date('M j, Y') }}.
```

## `POS_BEGIN`

Twig-facing copy of the [craft\web\View::POS_BEGIN](https://docs.craftcms.com/api/v3/craft-web-view.html#constants) constant.

## `POS_END`

Twig-facing copy of the [craft\web\View::POS_END](https://docs.craftcms.com/api/v3/craft-web-view.html#constants) constant.

## `POS_HEAD`

Twig-facing copy of the [craft\web\View::POS_HEAD](https://docs.craftcms.com/api/v3/craft-web-view.html#constants) constant.

## `POS_LOAD`

Twig-facing copy of the [craft\web\View::POS_LOAD](https://docs.craftcms.com/api/v3/craft-web-view.html#constants) constant.

## `POS_READY`

Twig-facing copy of the [craft\web\View::POS_READY](https://docs.craftcms.com/api/v3/craft-web-view.html#constants) constant.

## `siteName`

The name of your site, as defined in Settings → Sites.

```twig
<h1>{{ siteName }}</h1>
```

## `siteUrl`

The URL of your site

```twig
<link rel="home" href="{{ siteUrl }}">
```

## `SORT_ASC`

Twig-facing copy of the `SORT_ASC` PHP constant.

## `SORT_DESC`

Twig-facing copy of the `SORT_DESC` PHP constant.

## `SORT_FLAG_CASE`

Twig-facing copy of the `SORT_FLAG_CASE` PHP constant.

## `SORT_LOCALE_STRING`

Twig-facing copy of the `SORT_LOCALE_STRING` PHP constant.

## `SORT_NATURAL`

Twig-facing copy of the `SORT_NATURAL` PHP constant.

## `SORT_NUMERIC`

Twig-facing copy of the `SORT_NUMERIC` PHP constant.

## `SORT_REGULAR`

Twig-facing copy of the `SORT_REGULAR` PHP constant.

## `SORT_STRING`

Twig-facing copy of the `SORT_STRING` PHP constant.

## `systemName`

The System Name, as defined in Settings → General.

## `view`

A reference to the [craft\web\View](https://docs.craftcms.com/api/v3/craft-web-view.html) instance that is driving the template.

## Global Set Variables

Each of your site’s [global sets](../globals.md) will be available to your template as global variables, named after their handle.

They will be represented as [craft\elements\GlobalSet](https://docs.craftcms.com/api/v3/craft-elements-globalset.html) objects.

```twig
<p>{{ companyInfo.companyName }} was established in {{ companyInfo.yearEstablished }}.</p>
```
