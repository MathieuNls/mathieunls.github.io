---
layout: post
title: Citations.js&#58; A JQuery plugin to ease citations in html documents
tags:
- javascript
description: Citations.js&#58; A JQuery plugin to ease citations in html documents
---

I always liked LaTeX for how easy it is to manage references. Indeed a simple `\cite{citation-key}` coupled with a `\thebibliography{your-bibtex}` will automatically generate a citation and a reference table in your paper.
However, when you write html/mardown content, managing references could be obnoxious.
I trust that there is some Wordpress plugins  or node module to achieve just that through elegant drag and drop, but I wanted a solution that I can use here, on my Jekyll Github-page powered blog.

<!--more-->

That's why I've created [citations.js](https://github.com/MathieuNls/citations.jquery.js), A simple JQuery plugin to ease citations in html documents. You can see a live example [here](https://math.co.de/resume.html).

For now, citations. is only supports the `\citeAll` command of LaTeX that includes references for all the entries of a given JSON file.
In other words, it'll *only* generate the reference table.
However, you can already do some fancy manipulations on your reference table such as grouping, filtering, ordering, dynamic search and more.

Why JSON instead of the *regular* bibtex format you might ask. Well, did you ever write bibtex entry by hand ? I mean :

{% highlight bib %}
@inproceedings{Giger2011,
address = {New York, New York, USA},
author = {Giger, Emanuel and Pinzger, Martin and Gall, Harald C.},
booktitle = {Proceeding of the 8th working conference on Mining software repositories - MSR '11},
doi = {10.1145/1985441.1985456},
isbn = {9781450305747},
keywords = {code churn,nonlinear regression,prediction models,software bugs,source code changes},
month = {may},
pages = {83},
publisher = {ACM Press},
title = {{Comparing fine-grained source code changes and code churn for bug prediction}},
url = {http://dl.acm.org/citation.cfm?id=1985441.1985456},
year = {2011}
}
{% endhighlight %}

Seriously?! Personally, I use [mendeley](https://www.mendeley.com/) and the export and its export bibliography feature for LaTeX-based content.

JSON is easy to read/write and it's supported by jquery and bare javascript both which speed up the development of this plugin.

In the near future, I'd like to add the following to citations.js:

- Tests
- Highlight search results
- The current `cite` function is more like a LateX `\citeAll`, I would like to have both `\cite` and `\citeAll` behaviour.
- Support bibtex/build a bib to json converter
- Display a list of co-author with numbers of papers associated and allow searching by co-author
- Same for years
- Same for students (In case a Pr wants to highlights students of his)
- Support official citation style (APA, Harvard,...)

Let's get to it and see how to use citations.js.

## How to install

Download the [latest version of the plugin](https://github.com/MathieuNls/citations.jquery.js/releases/latest).

{% highlight html %}
<script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/underscore.js/1.8.3/underscore-min.js"></script>
<script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/jquery/2.2.1/jquery.min.js">
</script>
<script type="text/javascript" src="path/to/citations.jquery.js"></script>
{% endhighlight %}

## How to use

Given a `publications.json` file looking like:

{% highlight json %}
[
 {"authors":
   [
     {"lastname": "Nayrolles", "firstname": "Mathieu"},
     {"lastname": "Palma", "firstname": "Francis"},
     {"lastname": "Moha", "firstname": "Naouel"}
   ],
   "title":"SOA Antipatterns : An Approach for their Specification and Detection",
   "venue": "International Journal of Cooperative Information Systems",
   "volume":22,
   "issue":4,
   "year":2013,
   "type": "journal",
   "pages": "1-40"
 },...
 ...,
]
{% endhighlight %}

The following will populate the `#papers` element with a `<ul><li>` structure.

{% highlight js %}
$("#papers").cite({
  file : "/json/publications.json"
});
{% endhighlight %}
In this example, it'll generate

{% highlight html %}
<div id="papers">
  <ul>
    <li>Nayrolles, M. , Palma, F. &amp; Moha, N. (2013). SOA Antipatterns : An Approach for their Specification and Detection. International Journal of Cooperative Information Systems. (pp. 1-40).</li>
    <li>...</li>
    <li>...</li>
  </ul>
</div>
{% endhighlight %}

A more advanced example with sorting, grouping, and more:

{% highlight js %}
$("#papers").cite({
  file : "json/publications.json",
  sortBy : "year",
  orderType : "desc",
  groupBy: "type",
  myLastName : "Nayrolles",
  myFirstName : "Mathieu",
  classul: "resume-item-list",
  preGroup: "<div class='resume-item'><h3 class='resume-item-title'>{title}</h3>",
  postGroup:'</div>',
  groupTitle : {
    journal: "Peer Reviewed Journals"
  },
  searchBar: "#filter"
});
{% endhighlight %}
will generate :

{% highlight html %}
<div id="papers">
  <div class='resume-item'><h3 class='resume-item-title'>Peer Reviewed Journals</h3>
  <ul class="resume-item-list">
    <li><u>Nayrolles, M.</u> , Palma, F. &amp; Moha, N. (2013). SOA Antipatterns : An Approach for their Specification and Detection. International Journal of Cooperative Information Systems. (pp. 1-40).</li>
    <li>...</li>
    <li>...</li>
  </ul>
</div>
{% endhighlight %}
## Options

 * file: url to your publication json file
 * classul: optional class to add for ul
 * classli: optional class to add for each li
 * sortBy: optional field on which publications shall be sorted
 * orderType: optional, default = "asc".
 * filterBy: optional, field on which remove publication
 * filterValue: optional, field value on which remove publication
 * myLastName: optional, your last name to underline it
 * myFirstName: optional, your first name to underline it
 * debug: optional, default false.
 * groupBy:optional, a field on which group your publications
 * preGroup:optional, if you group your citation, you might want to add something before each group. You can use the `{title}` key in preGroup to replace it with the group key value
 * postGroup: optional, see preGroup
 * groupTitle: optional, the group key value might not be the title you want for your group. You can provide an associative array `groupKey value : Title`
 * searchBar:optional, provide a selector to an input field. Only publications matching the input value will be shown.
