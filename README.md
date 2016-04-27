# Contentful Widget SDK Developer Preview

The UI Extensions API allows you to extend the [Contentful](https://www.contentful.com)
Web Application's entry editor, so that you can build plugins that meet your
specific content editing or content management needs. It operates on top of any
of our current field types, and gives you the power to manipulate its data
through an iframe where you can embed custom functionality, styling,
integrations or workflows.

The UI Extensions API is stable but remains under active development so please reach out to us if you intend to use it for business critical operations. The purpose of making it available early is to provide early access to upcoming features and make our roadmap more transparent to users, as well as to collect early feedback before releasing, and commiting to support, a brand new API. 

Every Contentful user has access to this feature, it is enabled by default, and all requirements to start using it are simply to follow the instructions contained here.

This SDK overview introduces you to the concept of custom widgets and lists concrete
usage examples. The actual [widget API documentation][api-ref]
on the other hand gives you a more abstract and technical overview.

## Widgets taxonomy and example use cases

Conceptually, there are two main categories of custom widgets, for content
editing and content management. Editing widgets reside on the main body of the
entry editor and operate on top of a particular field or set of fields, while
the management widgets perform actions on the entire entry.

### Content editing widgets
Content editing widgets can operate on either single fields, or multiple fields.

#### Single field widgets
Content editing widgets applied to single fields are great for circumstances
where you just want to customize how you edit a particular field type. Examples
of single field widgets are:

* Integration with external digital asset management system (i.e. flickr) to
  insert external assets
* Specific data manipulation, like removing an element ID for a social media
  link
* Integration with a translation API service to programmatically translate the
  field's content
* Creation or integration with custom text editing interface

#### Multiple field widgets
If you need more than a single field, you can try multi-field level widgets.
Currently we have two approaches for this:

##### Using JSON objects
The first is a simple approach is to use a JSON object field type and construct
any complex field type that is not provided out of the box by Contentful, along
with its UI and logic. However, there is a tradeoff when using this approach.
Data inside of a JSON field cannot be used to query or filter entries in our
APIs.

##### Using relationships between multiple fields
This approach involves creating a single field custom widget that can use our
CMA to perform operations on other fields within the entry.
Examples of multi-field-level widgets are:

* Automatic asset metadata creation: When inserting an asset on a media field I
  want the long-text field below it to query our copyright database and fill-in
  the details for the asset above
* Custom recipes: When selecting an item from a dropdown menu I want the content
  of a short-text field type to change

### Content management widgets

Content management widgets reside on the sidebar and allow for actions that
include every element in the entry. These are better suited for tasks related to
workflows, data-management, integrations, etc.
Examples of entry-level widgets are:

* Custom webhooks/notifications
* Integration with a preview environment
* Moving entries across different spaces

## Getting Started

The most convenient way to upload and manage widgets through our API is via the
[`contentful-widget`][cf-widget-cli] command line tool. You can install it with

```bash
npm install -g contentful-widget-cli
```

To work with the widget sdk library and the examples, clone this repo and
install the dependencies:

```bash
git clone git@github.com:contentful/widget-sdk.git
cd widget-sdk
npm install
```

Including the compiled version of the widget client library is as simple as
adding the following line to your application.

```html
<script src="https://contentful.github.io/widget-sdk/cf-widget-api.js"></script>
```

If you want to learn how to write your own widgets and see them in
action, checkout the documentation for the
[Rating Dropdown Widget](./examples/rating-dropdown). To get an overview over
the API have a look at the [reference documentation][api-ref]

[cf-widget-cli]: https://github.com/contentful/contentful-widget-cli
[api-ref]: doc/widget-api-frontend.md


## Using Contentful Styles

As widgets are rendered inside an iframe, you will need to include the
`cf-widget-api.css` library within your custom widget in order to use any of
Contentful's styles.

Download the CSS library [here](https://contentful.github.io/widget-sdk/cf-widget-api.css) and include it in your widget

```html
<link rel="stylesheet" type="text/css" href="cf-widget-api.css">
```

Futher information can be found in the
[styleguide](http://contentful.github.io/widget-sdk/styleguide).


## Examples

This repo includes the following example widget implementations. Before you can
use them, you need to run `npm install` in the repository root.

#### [Basic Rating Dropdown](examples/rating-dropdown)

Basic widget that helps you *get started* with developing. Uses a dropdown to
change the value of a number field and makes some CMA requests.

#### [Chessboard](examples/chessboard)

![Chessboard Widget in action](http://contentful.github.io/widget-sdk/assets/chessboard.gif)

This widget displays a chessboard and stores the board position as a JSON
object. You can drag pieces on the chessboard and the position data will be
updated automatically. The widget also supports *collaborative editing*. If two
editors open the same entry moves will be synced between them.

#### [Slug Generator](examples/slug)

This widget will automatically generate its values from an entries title field.
For example typing “Hello World” into the title field will set the widgets input
field to “hello-world”. It will also check the uniquness of the slug across a
customizable list of content types.

This examples highlights how the widget API can be used to *inspect any value*
of an entry and *react to changes*.

#### [Rich Text Editor](examples/alloy-editor)

This example integrates the [Alloy rich text editor](http://alloyeditor.com/) to
edit “Text” fields.

#### [JSON Editor](examples/json-editor)
This widget provides a JSON formatter and validator based on the [Codemirror](http://codemirror.net) library.

It should be used with fields with the type “Object”.

#### [JSON Form Editor](examples/json-form-editor)
This widget integrates the [JSON Editor](https://github.com/jdorn/json-editor)
library to display an edit form based on a predefined [JSON Schema](https://json-schema.org/).
Form input gets stored as a JSON object.

#### [Translator](examples/translate)
This widget translates text from the default locale to other locales in a space using the Yandex translation API.

#### [Wistia Videos](examples/wistia)
The wistia widget loads videos from a [project](http://wistia.com/doc/projects) on [wistia](http://wistia.com/) into the Contentful UI. A video can be easily previewed, selected and then stored as part of your content. In this example widget we store the video embed URL in Contentful so the video can be embedded easily. 

![Screenshot of Wistia widget](http://contentful.github.io/widget-sdk/assets/wistia.gif) 


## Providing Feedback

Technical feedback can be provided directly through the Github repo. This has
several advantages, including a closer communication between developers and a
single point of information. Answers provided to one participant may also be
relevant to others, and we can use this space for a healthy and open
communication channel. However, if at any point some confidential or business
sensitive information needs to be discussed, then the conversation would
temporarily be handled via Zendesk.

We are mostly interested in technical details (custom widgets management, SDK,
API, specific functionality details) and use cases (concert examples of problems
that your organization could solve using custom widgets).


## End of Developer Preview Program

The final release of the UI Extensions API is scheduled for end of Q2 2016.
