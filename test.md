---
layout: regular
title: Your New Jekyll Site
---

<aside>
    <nav>
        <h1>Documentation</h1>
        <ul>
            <li>
                <a class="active" href="#step-introduction">Introduction: RAML 100 Tutorial</a>
            </li>
            <li>
                <a href="#step-enter-root">Step 1: Enter the Root</a>
            </li>
            <li>
                <a href="#step-enter-resources">Step 2: Enter Resources</a>
            </li>
            <li>
                <a href="#step-enter-methods">Step 3: Enter Methods</a>
            </li>
            <li>
                <a href="#step-enter-uri-params">Step 4: Enter URI Parameters</a>
            </li>
            <li>
                <a href="#step-enter-query-params">Step 5: Enter Query Parameters</a>
            </li>
            <li>
                <a href="#step-enter-responses">Step 6: Enter Responses</a>
            </li>
        </ul>
</aside>
<div class="content">
<h2 id="step-introduction">RAML 100 tutorial</h2>
<div class="tutorial-intro">
    <p><strong>Objective:</strong> Learn the basics of RAML by designing a very basic API for BookMobile.</p>
    <h4><i>Introduction</i></h4>
    <p>This tutorial will guide you through conceptualizing the design of your API and writing it in RAML, the RESTful API Modeling Language.</p>
    <h4><i>Assumptions</i></h4>
    <p>You know the basics of how RESTful APIs operate: how to send requests and responses, and how to specify the components of a RESTful API.</p>
</div>
<h2 id="step-enter-root"><strong>Step 1:</strong> Enter the Root</h2>
                    <p>Let's say you are the API designer for a BookMobile startup. You've worked out a business plan, a scaling plan, and Ashton Kutcher is an angel investor. You know you want developers to capitalize on what you've built, so that you can capitalize on what THEY build. You know having a RESTful API is one way to make that happen. So, let's get started by writing a spec.</p>
                    <p><strong>First, you'll enter some basic information in a text editor. You can save your API's RAML definition as a text file with a recommended extension .raml:</strong></p>
<pre>
                        <code>
<span class="ln">1  </span><span class="l1">#&#37;RAML 0.8</span>
<span class="ln">2  </span><span class="l5">---</span>
<span class="ln">3  </span><span class="def">title:</span> <span class="val">e-BookMobile API</span>
<span class="ln">4  </span><span class="def">baseUri:</span> <span class="val">http://api.e-bookmobile.com/{version}</span>
<span class="ln">5  </span><span class="def">version:</span> <span class="val">v1</span>
                        </code>
                    </pre>
                    <p>Everything you enter in at the <a href="https://github.com/raml-org/raml-spec/blob/master/04_basic_information.md#root-section" target="_blank">root</a> (or top) of the spec applies to the rest of your API. This is going to come in very handy later as you discover patterns in how you build your API. The baseURI you choose will be used with every call made, so make sure it's as clean and concise as can be.</p>
                    <h2 id="step-enter-resources"><strong>Step 2:</strong> Enter Resources</h2>
                    <p>As a thoughtful API designer, it's important to consider how your API consumers will use your API. It's especially important because in many ways, as the API designer YOU control the consumption. For example, consider the functionality of the BookMobile API. You know you want your users to be able to keep track of what they've read and their favorites. Users should also be able to discover new books and look at other titles written by their favorite authors. To do this, you define various _collections_ as your <a href="https://github.com/raml-org/raml-spec/blob/master/05_resources_and_methods.md#resources-and-nested-resources" target="_blank">resources</a>.</p>
                    <p><strong>Recalling how your API consumers will use your API, enter the following three resources under your root:</strong></p>
                    <pre>
                        <code>
<span class="ln">1  </span><span class="l3">/users:</span>
<span class="ln">2  </span><span class="l3">/authors:</span>
<span class="ln">3  </span><span class="l3">/books:</span>
                        </code>
                    </pre>
                    <p>Notice that these resources all begin with a backslash (/). In RAML, this is how you indicate a resource. Any methods and parameters nested under these top level resources belong to and act upon that resource. Now, since each of these resources is a collection of individual objects (specific authors, books, and users), we'll need to define some sub-resources to fill out the collection.</p>
                    <p><strong>Nested resources are useful when you want to call out a particular subset of your resource in order to narrow it. For example:</strong></p>
                    <pre>
                        <code>
<span class="ln">1  </span><span class="l3">/authors:</span>
<span class="ln">2  </span><span class="l3">  /{authorname}:</span>
                        </code>
                    </pre>
                    <p>This lets the API consumer interact with the key resource and its nested resources. For example a GET request to http://api.e-bookmobile.com/authors/Mary_Roach returns details about science writer and humorist Mary Roach. Now, let's think about what we want developers and API consumers to DO.</p>
                    <h2 id="step-enter-methods"><strong>Step 3:</strong> Enter Methods</h2>
                    <p>Here's where it starts to get interesting, as you decide what you want the developer to be able to do with the resources you've made available. <strong>Let's quickly review the 4 most common HTTP verbs:</strong></p>
                    <p><strong>GET</strong> - Retrieve the information defined in the request URI.</p>
                    <p><strong>PUT</strong> - Replace the addressed collection. At the object-level, create or update it.</p>
                    <p><strong>POST</strong> - Create a new entry in the collection. This method is generally not used at the object-level.</p>
                    <p><strong>DELETE</strong> - Delete the information defined in the request URI.</p>
                    <p>You can add as many methods as you like to each resource of your BookMobile API, at any level. However, each HTTP method can only be used once per resource. Do not overload the GET (you know who you are).</p>
                    <p>In this example, you want developers to be able to work at the collection level. For example, your API consumers can retrieve a book from the collection (GET), add a book (POST), or update the entire library (PUT). You do not want them to be able to delete information at the highest level. Let's focus on building out the /books resource.</p>
                    <p><strong>Nest the methods to allow developers to perform these actions under your resources. Note that you must use lower-case for methods in your RAML API definition:</strong></p>
                    <pre>
                        <code>
<span class="ln">1  </span><span class="l3">/books:</span>
<span class="ln">2  </span><span class="l4">  get:</span>
<span class="ln">3  </span><span class="l4">  post:</span>
<span class="ln">4  </span><span class="l4">  put:</span>
                        </code>
                    </pre>
                    <h2 id="step-enter-uri-params"><strong>Step 4:</strong> Enter URI Parameters</h2>
                    <p>The resources that we defined are collections of smaller, relevant objects. You, as the thoughtful API designer, have realized that developers will most likely want to act upon these more granular objects. Remember the example of nested resources above? /authors is made up of individual authors, referenced by {authorName}, for example. This is a URI parameter, denoted by surrounding curly brackets in RAML:</p>
                    <pre>
                        <code>
<span class="ln">1  </span><span class="l3">/books:</span>
<span class="ln">2  </span><span class="l3">  /{bookTitle}:</span>
                        </code>
                    </pre>
                    <p>So, to make a request to this nested resource, the URI for Mary Roach's book, Stiff would look like http://api.e-bookmobile.com/v1/books/Stiff</p>
                    <p><strong>Time to edit your spec to reflect the inherent granular characteristics of your resources:</strong></p>
                    <pre>
                        <code>
<span class="ln">1  </span><span class="l3">/books:</span>
<span class="ln">2  </span><span class="l4">  get:</span>
<span class="ln">3  </span><span class="l4">  put:</span>
<span class="ln">4  </span><span class="l4">  post:</span>
<span class="ln">5  </span><span class="l3">  /{bookTitle}:</span>
<span class="ln">6  </span><span class="l4">    get:</span>
<span class="ln">7  </span><span class="l4">    put:</span>
<span class="ln">8  </span><span class="l4">    delete:</span>
<span class="ln">9  </span><span class="l3">    /author:</span>
<span class="ln">10  </span><span class="l4">     get:</span>
<span class="ln">11  </span><span class="l3">   /publisher:</span>
<span class="ln">12  </span><span class="l4">     get:</span>
                        </code>
                    </pre>
                    <h2 id="step-enter-query-params"><strong>Step 5:</strong> Enter Query Parameters</h2>
                    <p>Great job so far! Now, let's say you want your API to allow even more powerful operations. You already have collections-based resource types that are further defined by object-based URI parameters. But you also want developers to be able perform actions like filtering a collection. Query parameters are a great way to accomplish this.</p>
                    <p><strong>Start by adding some query parameters under the GET method for books. These can be specific characteristics, like the year a book was published:</strong></p>
                    <pre>
                        <code>
<span class="ln">1  </span><span class="l3">/books:</span>
<span class="ln">2  </span><span class="l4">  get:</span>
<span class="ln">3  </span><span class="l5">    queryParameters:</span>
<span class="ln">4  </span><span class="l5">      author:</span>
<span class="ln">5  </span><span class="l5">      publicationYear:</span>
<span class="ln">6  </span><span class="l5">      rating:</span>
<span class="ln">7  </span><span class="l5">      isbn:</span>
<span class="ln">8  </span><span class="l4">  put:</span>
<span class="ln">9  </span><span class="l4">  post:</span>
                        </code>
                    </pre>
                    <p>Query parameters may also be something that the server requires to process the API consumer's request, like an access token. Often, you need security authorization to alter a collection or record. <strong>Nest the access-token query parameter under the PUT method for a specific title:</strong></p>
                    <pre>
                        <code>
<span class="ln">1  </span><span class="l3">/books:</span>
<span class="ln">2  </span><span class="l3">  /{bookTitle}</span>
<span class="ln">3  </span><span class="l4">    get:</span>
<span class="ln">4  </span><span class="l5">      queryParameters:</span>
<span class="ln">5  </span><span class="l5">        author:</span>
<span class="ln">6  </span><span class="l5">        publicationYear:</span>
<span class="ln">7  </span><span class="l5">        rating:</span>
<span class="ln">8  </span><span class="l5">        isbn:</span>
<span class="ln">9  </span><span class="l4">    put:</span>
<span class="ln">10  </span><span class="l5">     queryParameters:</span>
<span class="ln">11  </span><span class="l5">       access_token:</span>
                        </code>
                    </pre>
                    <p>An API's resources and methods often have a number of associated query parameters. Each query parameter may have any number of optional attributes to further define it. The Quick reference guide contains a full listing.</p>
                    <p><strong>Now, specify attributes for each of the query parameters you defined above. As always, be as complete in your documentation as possible:</strong></p>
                    <pre>
                        <code>
<span class="ln">1  </span><span class="l3">/books:</span>
<span class="ln">2  </span><span class="l3">  /{bookTitle}</span>
<span class="ln">3  </span><span class="l4">    get:</span>
<span class="ln">4  </span><span class="l5">      queryParameters:</span>
<span class="ln">5  </span><span class="l5">        author:</span>
<span class="ln">6  </span><span class="l5">          displayName:</span> <span class="val">Author</span>
<span class="ln">7  </span><span class="l5">          type:</span> <span class="val">string</span>
<span class="ln">8  </span><span class="l5">          description:</span> <span class="val">An author's full name</span>
<span class="ln">9  </span><span class="l5">          example:</span> <span class="val">Mary Roach</span>
<span class="ln">10  </span><span class="l5">         required:</span> <span class="val">false</span>
<span class="ln">11  </span><span class="l5">       publicationYear:</span>
<span class="ln">12  </span><span class="l5">         displayName:</span> <span class="val">Pub Year</span>
<span class="ln">13  </span><span class="l5">         type:</span> <span class="val">number</span>
<span class="ln">14  </span><span class="l5">         description:</span> <span class="val">The year released for the first time in the US</span>
<span class="ln">15  </span><span class="l5">         example:</span> <span class="val">1984</span>
<span class="ln">16  </span><span class="l5">         required:</span> <span class="val">false</span>
<span class="ln">17  </span><span class="l5">       rating:</span>
<span class="ln">18  </span><span class="l5">         displayName:</span> <span class="val">Rating</span>
<span class="ln">19  </span><span class="l5">         type: <span class="val">number</span>
<span class="ln">20  </span><span class="l5">         description:</span> <span class="val">Average rating (1-5) submitted by users</span>
<span class="ln">21  </span><span class="l5">         example:</span> <span class="val">3.14</span>
<span class="ln">22  </span><span class="l5">         required:</span> <span class="val">false</span>
<span class="ln">23  </span><span class="l5">       isbn:</span>
<span class="ln">24  </span><span class="l5">         displayName:</span> <span class="val">ISBN</span>
<span class="ln">25  </span><span class="l5">         type:</span> <span class="val">string</span>
<span class="ln">26  </span><span class="l5">         minLength:</span> <span class="val">10</span>
<span class="ln">27  </span><span class="l5">         example:</span> <span class="val">0321736079?</span>
<span class="ln">28  </span><span class="l4">    put:</span>
<span class="ln">29  </span><span class="l5">      queryParameters:</span>
<span class="ln">30  </span><span class="l5">        access_token:</span>
<span class="ln">31  </span><span class="l5">          displayName:</span> <span class="val">Access Token</span>
<span class="ln">32  </span><span class="l5">          type:</span> <span class="val">string</span>
<span class="ln">33  </span><span class="l5">          description:</span> <span class="val">Token giving you permission to make call</span>
<span class="ln">34  </span><span class="l5">          required: <span class="val">true</span>
                        </code>
                    </pre>
                    <p>To make a PUT call, your URI looks like http://api.e-bookmobile.com/books/Stiff?access_token=ACCESS TOKEN</p>
                    <h2 id="step-enter-responses"><strong>Step 6:</strong> Enter Responses</h2>
                    <p>Responses MUST be a map of one or more HTTP status codes, and each response may include descriptions, examples, or schemas. Schemas are more fully explained in the Level 200 tutorial.</p>
                    <pre>
                        <code>
<span class="ln">1  </span><span class="l3">/books:</span>
<span class="ln">2  </span><span class="l3">  /{bookTitle}:</span>
<span class="ln">3  </span><span class="l4">    get:</span>
<span class="ln">4  </span><span class="l5">      description:</span> <span class="val">Retrieve a specific book title</span>
<span class="ln">5  </span><span class="l5">      responses:</span>
<span class="ln">6  </span><span class="l5">        200:</span>
<span class="ln">7  </span><span class="l5">          body:</span>
<span class="ln">8  </span><span class="l5">            application/json:</span>
<span class="ln">9  </span><span class="l5">              example:</span> <span class="l1">|</span>
<span class="ln">10  </span><span class="l1">               {</span>
<span class="ln">11  </span><span class="l1">                 "data": {</span>
<span class="ln">12  </span><span class="l1">                   "id": "SbBGk",</span>
<span class="ln">13  </span><span class="l1">                   "title": "Stiff: The Curious Lives of Human Cadavers",</span>
<span class="ln">14  </span><span class="l1">                   "description": null,</span>
<span class="ln">15  </span><span class="l1">                   "datetime": 1341533193,</span>
<span class="ln">16  </span><span class="l1">                   "genre": "science",</span>
<span class="ln">17  </span><span class="l1">                   "author": "Mary Roach",</span>
<span class="ln">18  </span><span class="l1">                   "link": "http://e-bookmobile.com/books/Stiff",</span>
<span class="ln">19  </span><span class="l1">                 },</span>
<span class="ln">20  </span><span class="l1">                 "success": true,</span>
<span class="ln">21  </span><span class="l1">                 "status": 200</span>
<span class="ln">22  </span><span class="l1">               }</span>
                        </code>
                    </pre>
                    <p><strong>Congratulations! You've just written your first API definition in RAML.</strong></p><br /><br />
                    </div>