# NAME

Mojolicious::Plugin::TemplatePerlish - Template::Perlish renderer plugin for
Mojolicious

# VERSION

This document describes Mojolicious::Plugin::TemplatePerlish version {{\[ version \]}}.

# SYNOPSIS

    # Mojolicious
    $app->plugin('TemplatePerlish');
    $app->plugin(TemplatePerlish => {name => 'tpt'});
    $app->plugin(TemplatePerlish => {template_perlish => {start => '<%', stop => '%>'}});

    # Mojolicious::Lite
    plugin 'TemplatePerlish';
    plugin TemplatePerlish => {name => 'tpt'};
    plugin TemplatePerlish => {template_perlish => {start => '<%', stop => '%>'}});

    # Set as default handler, default name is 'tp'
    $app->renderer->default_handler('tp');

    # Render without setting as default handler
    $c->render(template => 'foo', handler => 'tp');

# DESCRIPTION

[Mojolicious::Plugin::TemplatePerlish](https://metacpan.org/pod/Mojolicious::Plugin::TemplatePerlish) is a renderer for [Template::Perlish](https://metacpan.org/pod/Template::Perlish)
templates. See [Template::Perlish](https://metacpan.org/pod/Template::Perlish) for details on the template format and
available opitons, and [Mojolicious::Guides::Rendering](https://metacpan.org/pod/Mojolicious::Guides::Rendering) for general
information on rendering in [Mojolicious](https://metacpan.org/pod/Mojolicious).

[Mojolicious](https://metacpan.org/pod/Mojolicious) helpers and stash values will be exposed directly as variables
in the templates, and the current controller object will be available as `c`
or `self`, similar to [Mojolicious::Plugin::EPRenderer](https://metacpan.org/pod/Mojolicious::Plugin::EPRenderer). See
[Mojolicious::Plugin::DefaultHelpers](https://metacpan.org/pod/Mojolicious::Plugin::DefaultHelpers) and [Mojolicious::Plugin::TagHelpers](https://metacpan.org/pod/Mojolicious::Plugin::TagHelpers)
for a list of all built-in helpers.

    $c->stash(description => 'template engine');
    $c->stash(engines => [qw(Template::Perlish Template::Toolkit)]);

    [% for my $engine (A 'engines') { %]
       [% engine %] is a [% description %].
    [% } %]

    [%= V('link_to')->('Perl', 'http://www.perl.org') %]

Along with standard template files, inline and data section templates can be
rendered in the standard way. Template files and data sections will be
retrieved using [Mojolicious::Renderer](https://metacpan.org/pod/Mojolicious::Renderer), so you should set
["paths" in Mojolicious::Renderer](https://metacpan.org/pod/Mojolicious::Renderer#paths) to the appropriate paths towards the templates.

# OPTIONS

The following options are supported.

## **cache**

    # Mojolicious::Lite
    plugin TemplatePerlish => {cache => 0};

By default this plugin caches templates to avoid recompiling the over and over.
If you plan to have a long running job, or a lot of templates, you can disable
caching passing a false value (like in the example above). A true value enables
caching. If you pass a hash reference, it will be used as cache (so you can
e.g. pre-populate it with subroutines, see
["compile\_as\_sub" in Template::Perlish](https://metacpan.org/pod/Template::Perlish#compile_as_sub)).

## **name**

    # Mojolicious::Lite
    plugin TemplatePerlish => {name => 'foo'};

Handler name, defaults to `tp`.

## **read\_binmode**

    # Mojolicious::Lite
    plugin TemplatePerlish => {read_binmode => ':raw'};

When a template is loaded from a file, this is the `binmode` that is applied
upon opening the file. Defaults to the string `:encoding(UTF-8)`.

## **template\_perlish**

    # Mojolicious::Lite
    plugin TemplatePerlish => {
       template_perlish => {
          start => '<%', # default is '[%'
          stop  => '%>', # default is '%]'
          variables => {foo => bar}, # default is {}
       }
    };

Options for [Template::Perlish constructor](https://metacpan.org/pod/Template::Perlish#new).

# METHODS

## **register**

    $plugin->register(Mojolicious->new());
    $plugin->register(Mojolicious->new(), {name => 'foo'});

Register renderer in [Mojolicious](https://metacpan.org/pod/Mojolicious) application.

# BUGS AND LIMITATIONS

Report bugs either through RT or GitHub (patches welcome).

# SEE ALSO

[Mojolicious](https://metacpan.org/pod/Mojolicious). Most of the documentation and tests is copied from
[Mojolicious::Plugin::TemplateToolkit](https://metacpan.org/pod/Mojolicious::Plugin::TemplateToolkit).

# AUTHOR

Flavio Poletti <polettix@cpan.org>

# COPYRIGHT AND LICENSE

Copyright (C) 2016 by Flavio Poletti <polettix@cpan.org>

This module is free software. You can redistribute it and/or modify it
under the terms of the Artistic License 2.0.

This program is distributed in the hope that it will be useful, but
without any warranty; without even the implied warranty of
merchantability or fitness for a particular purpose.
