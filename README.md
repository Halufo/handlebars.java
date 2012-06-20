handlebars.java - Logic-less and semantic templates with Java
===============

## Basic Usage
```java
Handlebars handlebars = new Handlebars();

Template template = handlebars.compile("Hello {{.}}!");

// will print: Hello Handlebars.java!
System.out.println(template.apply("Handlebars.java"));
```

## JavaBean Usage
```java
Blog blog = new Blog("My First Post", "edgar");
blog.setBody("...");

Handlebars handlebars = new Handlebars();

Template template = handlebars.compile("{{title}} by {{author}}\n{{body}}");

// will print:
//My First Post by edgar
//...
System.out.println(template.apply(blog));
```

## Map Usage
```java
Map blog = new HashMap();
blog.put("title", "My First Post");
blog.put("author", "edgar");
blog.put("body", "...");

Handlebars handlebars = new Handlebars();

Template template = handlebars.compile("{{title}} by {{author}}\n{{body}}");

// will print:
//My First Post by edgar
//...
System.out.println(template.apply(blog));
```

## Helper Usage
```java

Map<String, String> nav1 = new HashMap<String, String>();
nav1.put("url", "http://www.yehudakatz.com");
nav1.put("title", "Katz Got Your Tongue");

Map<String, String> nav2 = new HashMap<String, String>();
nav2.put("url", "http://www.sproutcore.com/block");
nav2.put("title", "SproutCore Blog");

Map<String, Object> navs = new HashMap<String, Object>();
navs.put("nav", Arrays.asList(nav1, nav2));

Handlebars handlebars = new Handlebars();
handlebars.registerHelper("list", new Helper<List<Map<String, String>>>() {
  public CharSequence apply(List<Map<String, String>> context, Options options) {
    String ret = "<ul>";
    
    for(Map<String, String> nav: context) {
      ret += "<li>" + options.fn(nav) + "</li>";
    }
    
    return ret + "</ul>";
  }
});

Template template = handlebars.compile("{{#list nav}}<a href="{{url}}">{{title}}</a>{{/list}}");

// will print:
//<ul>
//<li><a href="http://www.yehudakatz.com">Katz Got Your Tongue</a></li>
//<li><a href="http://www.sproutcore.com/block">SproutCore Blog</a></li>
//</ul>
System.out.println(template.apply(navs));
```

## Status
### Mustache Spec
 * Passes 123 of 127 tests from the [Mustache Spec](https://github.com/mustache/spec).
 * The 4 tests are: "Standalone Line Endings", "Standalone Without Previous Line", "Standalone Without Newline", "Standalone Indentation" all them from partials.yml.
 * In short, partials works 100% if you ignore white spaces indentation.

### Maven Central
 * There isn't a public release yet.

## Design
 * Handlebars.java do the best to follows the JavaScript API with some minors exceptions due to the nature of the Java Language.
 * The parser is built on top of [Parboiled] (https://github.com/sirthias/parboiled).
 * Data is provided as primitive types (int, boolean, double, etc.), strings, maps, list or JavaBeans objects.
 * Handlebars.java is thread-safe.

## Helpers
 * Handlebars.java includes the built-in helpers: 'if', 'unless', 'with', 'each', 'noop' and 'log'.
 * Handlebars.java also includes two built-in helpers: 'block' and 'partial' for doing [Template Inheritance](http://thejohnfreeman.com/blog/2012/03/23/template-inheritance-for-handlebars.html)

## FAQ

## License
[Apache License 2](http://www.apache.org/licenses/LICENSE-2.0.html)