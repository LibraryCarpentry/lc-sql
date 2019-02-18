# Library Carpentry

The Library Carpentry lesson module [SQL for Librarians](https://librarycarpentry.org/lc-sql/) is maintained by [Kristin Lee](https://github.com/kristindawn), [Chris Erdmann](https://github.com/libcce), *[Jordan Pedersen](https://github.com/JordanPedersen)*, [Elaine Wong](https://github.com/elainewong) and [Janice Chan](https://github.com/icecjan).

## Background

Library Carpentry is a software and data skills training programme for people working in library- and information-related roles. It builds on the work of [Software Carpentry](http://software-carpentry.org/) and [Data Carpentry](http://www.datacarpentry.org/). Library Carpentry is an official Lesson Program of [The Carpentries](https://carpentries.org/).

Library Carpentry is in the commons and for the commons. It is not tied to any institution of person. For more information on Library Carpentry, see our website [librarycarpentry.org](https://librarycarpentry.org).

## Contribution

There are many ways of contributing to Library Carpentry:

- Join our [Gitter discussion forum](https://gitter.im/LibraryCarpentry/).
- Follow updates on [Twitter](https://twitter.com/LibCarpentry).
- Make a suggestion or correct an error by [raising an Issue](https://github.com/data-lessons/library-sql/issues).

See the additional ways you can connect with the community by visiting the Library Carpentry [Contact Us](https://librarycarpentry.org/contact/) page.

## Code of Conduct

All participants should agree to abide by The Carpentries [Code of Conduct](https://docs.carpentries.org/topic_folders/policies/code-of-conduct.html).

## Authors

Library Carpentry is authored and maintained by the [community](https://github.com/LibraryCarpentry/lc-sql/network/members).

## Citation

Please cite as:

Library Carpentry. SQL for Librarians. June 2016. https://librarycarpentry.org/lc-sql/.

1. Installation instructions for core lessons are included in the [workshop template's home page][template],
   so that they are all in one place.
   The `setup.md` files of core lessons link to the appropriate sections of the [workshop template page][template].

2. Other lessons' `setup.md` include full installation instructions organized by OS
   (following the model of the workshop template home page).


## Contributing

If you want to set up Jekyll
so that you can preview changes on your own machine before pushing them to GitHub,
you must install the software described below.
(Note: Julian Thilo has written instructions for [installing Jekyll on Windows](http://jekyll-windows.juthilo.com/).)

1.  **Ruby**.
    This is included with Linux and Mac OS X;
    the simplest option on Windows is to use [RubyInstaller](http://rubyinstaller.org/).
    You can test your installation by running `ruby --version`.
    For more information,
    see [the Ruby installation guidelines](https://www.ruby-lang.org/en/downloads/).

2.  **[RubyGems](https://rubygems.org/pages/download)**
    (the package manager for Ruby).
    You can test your installation by running `gem --version`.

3.  **[Jekyll](https://jekyllrb.com/)**.
    You can install this by running `gem install jekyll`.

[template]: {{ site.workshop_repo }}
