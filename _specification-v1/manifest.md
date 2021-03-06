---
title: Origami.json Manifest Specification
description: A specification which describes the required structure of an Origami.json manifest file.
cta: Read the manifest spec

# Redirect from legacy URLs
redirect_from:
  - /docs/syntax/origamijson/

# Navigation config
nav_display: true
nav_label: Manifest
nav_order: 25
---

# {{page.title}}

`origami.json` is a <a href="https://www.json.org/" class="o-typography-link--external"><abbr title="JavaScript Object Notation">JSON</abbr></a> format file that is responsible for describing various aspects of an Origami component.

## Properties

### description

<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>String</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>true</code></td>
	</tr>
</table>

**Should** be a concise description of the purpose of the component.
<pre><code class="o-syntax-highlight--json">{
	"description": "Branded tables"
}</code></pre>

### origamiType

<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>String</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>true</code></td>
	</tr>
</table>

Defines the type of Origami component that the manifest belongs to. **Must** be set to one of:
- `module`
- `imageset`
- `service`

<aside>
	The <code>type</code> of <code>"module"</code> is a hangover from when client-side Origami components were named "modules". It's likely to change in a later version of the spec.
</aside>

<pre><code class="o-syntax-highlight--json">{
	"origamiType": "module"
}</code></pre>

### origamiVersion

<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>Integer</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>true</code></td>
	</tr>
</table>

**Must** be set to `1`. It is the version of Origami to which the component conforms.
<pre><code class="o-syntax-highlight--json">{
	"origamiVersion": 1
}</code></pre>

### keywords

<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>Array</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>true</code></td>
	</tr>
</table>

Expects keywords related to the component to help discover it in the registry. These **should** be stored as an array.

<pre><code class="o-syntax-highlight--json">{
	"keywords": ["table", "rows", "columns"]
}</code></pre>

### origamiCategory

<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>String</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>true</code></td>
	</tr>
</table>

Describes the organisational category the component belongs to. **Must** be one of:
- `components`
- `primitives`
- `utilities`
- `layouts`

<pre><code class="o-syntax-highlight--json">{
	"origamiCategory": "components"
}</code></pre>

### support
<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>String</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>true</code></td>
	</tr>
</table>
Describes where a user can go for support on this component. **Should** be the URL of the component's GitHub issues.

<pre><code class="o-syntax-highlight--json">{
	"support": "https://github.com/Financial-Times/o-table/issues"
}</code></pre>

### supportStatus

<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>String</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>true</code></td>
	</tr>
</table>

Describes the support status of the component's major version. **Must** be one of:
- `active`: feature development ongoing, bug reports will be gratefully received and acted upon promptly
- `maintained`: not actively developed but reproducible bugs will be fixed promptly and work done where necessary to maintain compatibility with browsers and other components
- `deprecated`: not actively developed, not recommended for new projects, only the most disabling bugs will be addressed and only when time allows, but existing implementations may still work
- `dead`: decommissioned entirely, will receive no support
- `experimental`: the component is not ready for production use

<pre><code class="o-syntax-highlight--json">{
	"supportStatus": "active"
}</code></pre>

### supportContact

<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>Object</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>false</code></td>
	</tr>
</table>

Describes contact details a user can choose from to find support for this component. The owner(s) identified in the support options commit to:
- reviewing code prior to release
- signing off on deployments
- publishing and maintaining up to date releases and documentation
- decommissioning the component when appropriate
- provide support to the users of the component

The object **requires** two properties:
- `email`: type `String`. Is an email address that users can request support from. This email **must** be group or role based, not a named individual
- `slack`: type `String`. Is a slack channel that users can go to for support. This **must** be in the format: organisation/channel-name

<pre><code class="o-syntax-highlight--json">{
	"supportContact": {
		"email": "origami.support@ft.com",
		"slack": "financialtimes/ft-origami"
	}
}</code></pre>


### ci
<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>Object</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>false</code></td>
	</tr>
</table>
_This object is no longer used in the Origami manifest. It is documented here for the purpose of reference in case a component does still use it_. Describes a set of one or more URLs where build information can be found.
<pre><code class="o-syntax-highlight--json">{
	"ci": {
		"circle": "https://circleci.com/api/v1/project/owner/repo",
		"travis": "https://api.travis-ci.org/repos/owner/repo/builds.json",
		"jenkins": "https://jenkins.example.com/job/"
	}
}</code></pre>

circle:	A CircleCI build status URL (https://circleci.com/api/v1/project/owner/repo)

### browserFeatures

<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>Object</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>false</code></td>
	</tr>
</table>

Applies to `{ "origamiType": "module" }` only. Outlines the browser features required for the component's functionality.
The object accepts two properties:
- `required`: type `Array`. A list of <a href="https://polyfill.io" class="o-typography-link--external">Polyfill Service</a> features or <a href="https://modernizr.com/docs/" class="o-typography-link--external">Modernizr</a> tests, which the component assumes exists. If these features do not exist, the component may error.
- `optional`: type `Array`. A list of <a href="https://polyfill.io" class="o-typography-link--external">Polyfill Service</a> features or <a href="https://modernizr.com/docs/" class="o-typography-link--external">Modernizr</a> tests, which the component  will use if they are available in the browser. If not the component may offer different or reduced functionality, but with graceful degradation.

<pre><code class="o-syntax-highlight--json">{
	"origamiType": "module",
	"browserFeatures": {
		"required": [
		"customEvent"
		],
		"optional": [
			"IntersectionObserver",
			"IntersectionObserverEntry"
		]
	}
}</code></pre>

### serviceUrl

<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>String</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>true</code>*</td>
	</tr>
</table>

*Applies to `{ "origamiType": "service" }` only.

Is the URL on which the service is provided.

<pre><code class="o-syntax-highlight--json">{
	"origamiType": "service",
	"serviceUrl": "https://www.ft.com/__origami/service/build/"
}</code></pre>

### demosDefaults
<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>Object</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>false</code></td>
	</tr>
</table>

Describes default options to be applied to all demos.
The object accepts the following properties:

**required** (when setting demo defaults):
- `template`: type `String`. Describes the path to the mustache template to render

**optional**
- `sass`: type `String`. Describes the path to the Sass file to compile.
- `js`: type `String`. Describes the JS file to build.
- `data`: type `Object`. Describes data to populate to the mustache template with.
- `documentClasses`: type `Object`. Names CSS classes to set on the `html` tag.
- `dependencies`: type `Array`. Is a list of other components that are only needed for demos, which will be loaded via the <a href="https://www.ft.com/__origami/service/build" class="o-typography-link--external">Build Service</a>

<pre><code class="o-syntax-highlight--json">{
	"demosDefaults": {
		"template": "demos/src/demo.mustache"
		"sass": "demos/src/demo.scss",
		"js": "demos/src/demo.js"
		"data": {
			"striped-rows": true
		},
		"documentClasses": "demo-container",
		"dependencies": ["o-normalise"]
	}
}</code></pre>

### demos
<table class="o-manifest__table o-table o-table--compact o-table--row-headings o-table--vertical-lines o-table--horizontal-lines" data-o-component="o-table">
	<tr>
		<th scope="row" role="rowheader">Type</th>
		<td><code>Array</code></td>
	</tr>
	<tr>
		<th scope="row" role="rowheader">Required</th>
		<td><code>false</code></td>
	</tr>
</table>

It accepts an array. Is a list of configuration objects for individual demos.
Each object in the list accepts the following properties:

**required**:
- `name`: type `String`. Demo name which will be used as the name of the outputted html file
- `title`: type `String`. A title for the demo which will appear when listed in the Registry
- `description`: type `String`. An explanation of the purpose of the demo
- `template`: type `String`. Describes the path to the demo-specific mustache template to render

**optional**:
- `sass`: type `String`. Describes the path to the demo-specific Sass file to compile.
- `js`: type `String`. Describes the path to the demo-specific JS file to build.
- `data`: type `Object`. Describes to populate to the component-specific mustache template with
- `documentClasses`: type `Object`. Names CSS classes to set on the component-specific `html` tag
- `dependencies`: type `Array`. Is a list of other components that are only needed a this specific demo, which will be loaded via the <a href="https://www.ft.com/__origami/service/build" class="o-typography-link--external">Build Service</a>
- `hidden`: type `Boolean`. Whether the demo should be hidden in the Registry
- `display_html`: type `Boolean`. Whether the demo should have a HTML tab in the Registry (defaults to true)

<pre><code class="o-syntax-highlight--json">{
	"demos": [
		{
			"name": "Basic table",
			"description": "Basic table implementation",
			"template": "demos/src/basic-component.mustache"
		},
		{
			"name": "Striped table",
			"description": "Striped table implementation",
			"template": "demos/src/striped-table.mustache",
			"sass": "demos/src/striped-table.scss",
			"documentClasses": "demo-striped-table-container"
		},
		{
			"name": "pa11y",
			"description": "Hidden test for pa11y",
			"hidden": true,
			"template": "demos/src/pa11y.mustache"
		}
	]
}</code></pre>

## Example

This example joins all of the property snippets outlined above:

<pre><code class="o-syntax-highlight--json">{
	"description": "Branded tables",
	"origamiType": "module",
	"origamiVersion": 1,
	"keywords": ["table", "rows", "columns"],
	"origamiCategory": "components",
	"support": "https://github.com/Financial-Times/o-table/issues",
	"supportStatus": "active",
	"supportContact": {
			"email": "origami.support@ft.com",
			"slack": "financialtimes/ft-origami"
		}
	"browserFeatures": {
		"required": [
		"customEvent"
		],
		"optional": [
			"IntersectionObserver",
			"IntersectionObserverEntry"
		]
	},
	"demosDefaults": {
		"template": "demos/src/demo.mustache"
		"sass": "demos/src/demo.scss",
		"js": "demos/src/demo.js"
		"data": {
			"striped-rows": true
		},
		"documentClasses": "demo-container",
		"dependencies": ["o-normalise"]
	},
	"demos": [
		{
			"name": "Basic table",
			"description": "Basic table implementation",
			"template": "demos/src/basic-component.mustache"
		},
		{
			"name": "Striped table",
			"description": "Striped table implementation",
			"template": "demos/src/striped-table.mustache",
			"sass": "demos/src/striped-table.scss",
			"documentClasses": "demo-striped-table-container"
		},
		{
			"name": "pa11y",
			"description": "Hidden test for pa11y",
			"hidden": true,
			"template": "demos/src/pa11y.mustache"
		}
	]
}</code></pre>
