---
layout: post
title: "On linked data surveys, rewards and data ownership"
author: joep
permalink: /blog/linked-data-surveys/
---

In this article, we'll discuss how linked data can make surveys more easy to manage, increase response rates using rewards, create new benefits for users and more.

- Why it's important to improve survey interoperability
- How we could increase interoperability using linked data
- How we can use rewards to increase respondent rates for surveys

## Why we need Survey interoperability

Surveys are a pretty interesting and complex type of data model.
You can think of a Survey as describing three concepts at once:

1. a data schema / model (datatypes, required fields, etc.)
1. a UI (the questions show to the user)
1. and a customer journey (the sequence of questions, sometimes with conditional paths).

Due to this complexity, it should not be a big surprise that there are many approaches to creating a Survey, and this has contributed to the low degree of interoperability of surveys.

That's a shame, because having interoperable Surveys would be _really cool_!

- It would be easier for researchers to **standardize how questions are asked**. For example, many medical surveys are highly standardized, up to how specific words can be used. You can probably imagine how a small change in phrasing a question or answer could have a serious impact on average results. If we standardize surveys and their questions on a data level, researchers could simply import an existing survey, instead of going through the time consuming process of manually creating every single field in their survey software.
- Respondents could have more **freedom in chooing a UI**. Not all user interfaces are easily accessible, pretty, or fun to use. People can have vastly different preferences regarding how a survey should be filled in. If we standardize how Survey Data is structured, we can let respondents pick their own front-end, similar to how you can open a webpage in any webbrowser that you like.
- We could **auto-fill** data from a personal source, which makes entering data less tedious. Browsers already do this for addresses and credit cards, but we can extend this _way_ further by using links! We'll get to that later
- We can **improve insights in ourselves** by storing and then analyzing data that we filled in in a survey. For example, filling in a survey about how your shortness of breath linked to air pollution has been today could be used in a different app to make a graph that visualizes how your shortness of breath has progressed over the months for personal insight.

Achieving these last two steps requires a high degree of standardization in both the surveys and the responses. The survey and its questions should provide information about:

- The **question** itself. This is required in all survey questions, of course.
- The **required datatype** of the response, such as 'string', or 'datetime' or some 'enumeration'.
- A (link to a) **semantic definition** of the property being described. This is a bit more obscure: all pieces of linked data use links, instead of keys, to describe the relation between some resource and its property. For example, a normal resource might have a 'birthdate', while in linked data, we'd use 'https://schema.org/birthDate'. This semantic definition makes things easier to share, because it prevents misinterpretation. Links remove ambiguity.
- A **query description**. This is even more obscure, but perhaps the most interesting. A query description means describing how a piece of information can be retrieved. Perhaps a question in a survey will want to know what your payment pointer is. If a piece of software wants to auto-fill this field, it needs to know where it can find your payment pointer.

## Making surveys interoperable

A good place to start standardizing, is to use _links_ everywhere. Use links for Properties, use links as identifiers for Surveys, for Responses, for Questions...
Links are great, because they can be _opened_.
Read my article on [Linked Data](https://ontola.io/what-is-linked-data) if this is new to you.

Okay, so we standardize the Questions, Surveys and Responses using links. But which links? And how?
At Ontola, we've been building dynamic RDF based forms for our [Argu.co](https://argu.co) e-democracy application.
We started out by using the [W3C SHACL specification](https://www.w3.org/TR/shacl/), which is a linked data standard for describing data models.
It turned out to be a great first step, as it ticked the first box of concepts in surveys: it describes the _schema_.
But we still have two concepts left to define: the _UI_ and the _Journey_.
For example, the SHACL spec does not provide UI concepts for describing whether to use a _radio select_ or a _dropdown_, or how to render a _helper text_.
And the _Journey_ should include conditional paths, which is also not possible.
These conditions are also important when the _rights_ of a user determines whether that user can edit a certain field.
We could either calculate all the form fields dynamically, or we could let the front-end use conditional fields to determine which fields are shown.
We opted for the latter, as this resulted in better performance.

So we're currently working on a Form ontology which adds things like `Pages`, `Groups`, `helper text` and `Conditions`.
As this is still prone to changes and under-specified, we'd rather not share it in its current form, but we do aim to do this in the near future.
An open-source implementation of our Survey software can be found on [Gitlab](https://gitlab.com/ontola/linked-surveys).

## Rewarding responses

Filling in a survey isn't the most fun thing to do, so getting people to fill in a survey can be a challenge.
That's why it's pretty common these days to see surveys that promise a chance to win rewards like nice gadgets (iPads, mostly) or coupons.
The first problem with this approach is that the one filling in the survey doesn't have a clear estimate of what their chances of winning are, which makes the deal a bit less attractive.
The second problem is that it requires the respondent to provide privacy sensitive details, such as address.
A third problem is that not everybody wants an iPad - money is often a bit more attractive.
Ideally, we'd provide a clear and transparent reward, and do so in an anonymous fashion.

A couple of months ago, we discovered the Grant for the Web, a grant that aims to change how we do payments on the internet.
We submitted a proposal to implement a solution for the problems stated above: we wanted to build a service that sends a payment to people who completed a survey.
Because we wanted to provide a high degree of privacy, we wanted our own services to be completely unaware of the payment address of the receiver.
We also wanted to make this project re-usable for other usages (other survey tools, or totally different things).
We therefore up building an open source service, called [**cashlink**](https://gitlab.com/ontola/cashlink).
It works like this:

- Create unique links (hence _cashlink_) which encode the value of the link. These can be used only once.
- Share this unique URL in some application, such as at the end of a survey.
- When the user opens this URL, they can submit their own _Payment Pointer_, which is an open specification for payment addresses built for the web.
- After submitting this, the payment is sent by the cashlink service.

## In conclusion

- Having a higher degree of standardization can offer various benefits: more standardized research, auto fill forms, UI freedom, and get more insights in our own personal data
- Linked Data can be used to facilitate this standardization process, but we need more (well-documented) standards to do this.
- Payments can be an effective tool for getting more people to fill in surveys.
