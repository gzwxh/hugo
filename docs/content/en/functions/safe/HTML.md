---
title: safe.HTML
linkTitle: safeHTML
description: Declares a provided string as a "safe" HTML document to avoid escaping by Go templates.
categories: [functions]
keywords: []
menu:
  docs:
    parent: functions
function:
  aliases: [safeHTML]
  returnType: template.HTML
  signatures: [safe.HTML INPUT]
relatedFunctions:
  - safe.CSS
  - safe.HTML
  - safe.HTMLAttr
  - safe.JS
  - safe.JSStr
  - safe.URL
aliases: [/functions/safehtml]
---

It should not be used for HTML from a third-party, or HTML with unclosed tags or comments.

Given a site-wide [`hugo.toml`][config] with the following `copyright` value:

{{< code-toggle file="hugo" >}}
copyright = "© 2015 Jane Doe.  <a href=\"https://creativecommons.org/licenses/by/4.0/\">Some rights reserved</a>."
{{< /code-toggle >}}

`{{ .Site.Copyright | safeHTML }}` in a template would then output:

```html
© 2015 Jane Doe.  <a href="https://creativecommons.org/licenses/by/4.0/">Some rights reserved</a>.
```

However, without the `safeHTML` function, html/template assumes `.Site.Copyright` to be unsafe and therefore escapes all HTML tags and renders the whole string as plain text:

```html
<p>© 2015 Jane Doe.  &lt;a href=&#34;https://creativecommons.org/licenses by/4.0/&#34;&gt;Some rights reserved&lt;/a&gt;.</p>
```

[config]: /getting-started/configuration/