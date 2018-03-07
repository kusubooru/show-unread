# \<show-unread\>

A web component displaying the number of unread private messages of a user in a
notification badge.

![show-unread](doc/show-unread.png)

## Disclaimer

This web component sends an AJAX request to one of our internal services. It is
not a reusable web component. But it is simple and if you are new to web
components, you could use it as an example.

## Development

Install the [Polymer CLI](https://www.npmjs.com/package/polymer-cli).

### Serve locally

```
$ polymer serve
```

### Testing

```
$ polymer test
```

### Building

We found building to be very non-trivial. Our current application is written in
PHP and it is not "web component aware". There are many questions:

* How do we make a web component work in an existing application?
* What dependencies do we need to include to make the web component work?
* How do we "package" a web component and its dependencies?
* How to make the web component work across browsers?

Currently our procedure involves creating a dummy Polymer project, which only
includes \<show-unread\>. We build the project with `polymer build` using a
configuration similiar to
[es5-bundled](https://www.polymer-project.org/2.0/toolbox/build-for-production#build-presets).

The build produces an `index.html` file and a `bower_components` folder. The
head tag of the produced `index.html` contains the polyfills and scripts
required for the component's dependencies and making it work across browsers.
We copy the `bower_components` to the server and we extract all the scripts
from the head tag of the produced `index.html` to the head tag of our existing
application.

This procedure works but it is delicate and kinda ugly. There has to be a
better way. We have hopes that Polymer 3.0 will make it easier to include a web
component in any other project regardless of the technology used.
