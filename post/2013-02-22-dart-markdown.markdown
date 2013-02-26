---
title: Dart Markdown
date: 2013-02-22 23:53
---

Minor detour. My questions on the [dart mailing list][list] have lead to my 
first library on [pub.dartlang.org][pub]. I can't take credit for the code (I 
think [Bob Nystrom][munificent] write most of it), but I'm happy to make 
myself useful by maintaining and building on it.

Extracting the library from Dartdoc meant removing support for Dart syntax 
highlighting. Fortunately, with some pointers from the list, I've written a 
new Dart classifier based on [analyzer_experimental][analyzer]. HTML/CSS 
classifiers are also [in the works][classifiers].

The project is [located here][project], and there is a editor demo running 
on [GitHub pages][demo]. Pull requests, feedback and issues welcome.

[list]: https://groups.google.com/a/dartlang.org/forum/#!topic/misc/q79EMVtD2Xg
[munificent]: https://github.com/munificent
[pub]: http://pub.dartlang.org/packages/markdown
[analyzer]: http://pub.dartlang.org/packages/analyzer_experimental
[project]: http://github.com/dpeek/dart-markdown
[demo]: http://dpeek.github.com/dart-markdown
[classifiers]: https://github.com/dpeek/dart-markdown/tree/feature/classify-html