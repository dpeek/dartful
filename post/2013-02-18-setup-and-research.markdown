---
title: Setup and Research
date: 2013-02-18 21:39
---

The [installation instructions][install] on the Dart website are great, and 
since I didn't have any issues I don't have much to add. In no time at all I 
was skimming through tutorials, playing with futures from dart:async and 
writing my first HelloWorld HttpServer with Rikulo. Rikulo introduced the idea 
of a project `build.dart` where I could define build tasks, A good place to 
start roughing out the pieces of the blog engine.

--

The build script is executed when files in your project change, and can also 
be configured using the option parsing library from the Dart Team. This should 
allow me to define some tasks for creating pages and posts, previewing and 
publishing the site. Initially I'll focus on publishing.

Here's what publishing needs to do (pseudo code):

```dart
class Post {
  // post model
}

void main() {
  var files = getMarkdownFiles();
  var posts = paths.map(readPost);
  writeIndex(posts);
  posts.forEach(writePost);
}

List<File> getMarkdownFiles() {
  // get markdown files
}

Post readPost(File file) {
  // read file
  // parse haml
  return post;
}

void writeIndex(List<Post> posts) {
  // markdown to html
  // write file
}

void writePost(Post post) {
  // markdown to html
  // write file
}
```

## Markdown

Most of the work involved parsing Markdown and converting it to HTML. Dartdoc, 
a documentation tool that ships with the SDK, includes an approachable parser 
and HTML renderer. Unfortunately, using it outside of Dartdoc took some work.

I found another project using the parser on GitHub where it was referenced 
using a `sdk:dartdoc` pubspec dependency. This no longer works as Dartdoc has 
been moved from `dart-sdk/pkg` to `dark-sdk/lib/_internal`. I eventually found 
a workaround by copying `_private` to my project. I've asked for a better 
solution on the [mailing list][mailing].

I can now parse Markdown like a boss:

```dart
import '_internal/dartdoc/lib/markdown.dart';

void main() {
  print(markdownToHtml("Hello *World*"));
}
```

## YAML

The [YAML][yaml] library used to parse pubspec files does what is says on the 
box, parsing a document into a stream of key/value pairs. In this case it will 
be easier to create a lookup:

```dart
void main() {
  var values = new Map();
  loadYaml('foo: 10').forEach((k, v) => values[k] = v);
  print(values[foo]);
}
```

## Templates

It seems like the Dart team has [plans for templates][template-thread]. I did 
investigate the [template library][template] in the bleeding edge branch, but 
it seems to have fallen behind changes to the core libraries and language. I 
also checked out [hart][hart] but it seems like the wrong solution for what 
should be fairly simple page templates. For now I'll stick with hard coded 
templates until the basics are finished.

[install]: http://www.dartlang.org/downloads.html
[yaml]: http://pub.dartlang.org/packages/yaml
[template-thread]: https://groups.google.com/a/dartlang.org/forum/?fromgroups=#!topic/misc/o8SWaMrjDgA
[template]: http://blog.sethladd.com/2012/03/first-look-at-darts-html-template.html
[hart]: http://pub.dartlang.org/packages/hart