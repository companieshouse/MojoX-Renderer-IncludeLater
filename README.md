# NAME

MojoX::Renderer::IncludeLater - A post processor to defer partial template rendering

# DESCRIPTION

[MojoX::Renderer::IncludeLater](https://metacpan.org/pod/MojoX::Renderer::IncludeLater) is a [Mojolicious](https://metacpan.org/pod/Mojolicious) plugin which adds support for
deferring rendering of partial templates until the parent template rendering is complete.

For example, this makes it possible to build up data during rendering (e.g. which
input fields are rendered) and then use that data to render an earlier part of a template.

This should work with any [Mojolicious](https://metacpan.org/pod/Mojolicious) renderer, including [Mojolicious::Renderer](https://metacpan.org/pod/Mojolicious::Renderer) and
[Mojolicious::Renderer::Xslate](https://metacpan.org/pod/Mojolicious::Renderer::Xslate).

# SYNOPSIS

Example 'test' template:

    % stash('my_var') // 'my_var has not been set'

Example page template:

    <h3>Include later</h3>
    <p>Include a template immediately</p>
    % include "test" # will render 'my_var has not been set'

    <p>Include a template later</p>
    % include_later "test" # will render 'foo'

    <p>Set a value the included template expects</p>
    % stash('test' => 'foo')

Which will generate the following output:

    <h3>Include later</h3>
    <p>Include a template immediately</p>
    my_var has not been set

    <p>Include a template later</p>
    foo

    <p>Set a value the included template expects</p>

# HELPERS

This plugin creates the following [Mojolicious](https://metacpan.org/pod/Mojolicious) helpers:

## include\_later

Is identical to `include` but template inclusion happens after
the rest of the template has been rendered.

# HOOKS

This plugin hooks into `after_render` to perform deferred template inclusion.

# SEE ALSO

[Mojolicious](https://metacpan.org/pod/Mojolicious)
