---
title: Effective Guide to Write Testable JavaScript
shortdesc: "With the growth in technology, we have earned better options for unit testing JavaScript. Whether we are using Node paired with a test framework like Mocha or Jasmine, in a headless browser, we have a variety of options. However, it does not mean that the code which is tested is as easy on us as our tools are!  "
cmsUserSlug: effective-guide-to-write-testable-javascript
date: 2014-04-21T10:33:56.000Z
banner: /img/citadel.jpg
categories: recent-blog
writer: Philip Bodart
---

<p>With the growth in technology, we have earned better options for unit testing JavaScript. Whether we are using Node paired with a test framework like Mocha or Jasmine, in a headless browser, we have a variety of options. However, it does not mean that the code which is tested is as easy on us as our tools are!</p>
<p>Organizing and writing code is easily testable and requires some efforts, but&nbsp;functional programming concepts are inspired by few patterns which can help in&nbsp;testing our code.</p>
<p>Here in this article, we will go through some useful tips and patterns for writing&nbsp;testable code in JavaScript.</p>
<h3>Keep Business Logic and Display Logic Separate</h3>
<p>JavaScript&shy;based browser application primally listens to DOM events which is&nbsp;triggered by the end user. It is always tempting to write an anonymous function that&nbsp;does maximum work right while setting up DOM event listeners. This can create&nbsp;aloft both in lines of code and the time for practising.&nbsp;So, it is recommended to, write a named function and pass it to the event handler.&nbsp;This applies to more than the DOM, though. Many APIs, both in the browser and in&nbsp;Node, are serving this purpose.</p>
<div class="precode_">
<p class="commnt_">// hard to test</p>
<p><span class="dollar_">$</span>('.show').on('click', () =&gt; {</p>
<p>&nbsp; &nbsp;<span class="dollar_">$</span>.getJSON('/file_path')</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; .then(data =&gt; {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="dollar_">$</span>('#output&shy;list').html('output: ' + data.join(', '));</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; });</p>
<p>});</p>
<p class="commnt_">// testable; we can directly run fetchList to see if it</p>
<p class="commnt_">// makes an AJAX request without triggering DOM</p>
<p class="commnt_">// events, and we can run showList directly to see that it</p>
<p class="commnt_">// displays data in the DOM without AJAX request</p>
<p><span class="dollar_">$</span>('.show').on('click', () =&gt; fetchList(showList));</p>
<p>function fetchList(callback) {</p>
<p>&nbsp; &nbsp;<span class="dollar_">$</span>.getJSON('/file_path').then(callback);</p>
<p>}</p>
<p>function showList(data) {</p>
<p>&nbsp; &nbsp;<span class="dollar_">$</span>('#output&shy;list').html('output: ' + data.join(', '));</p>
<p>}</p>
</div>
<h3>Use Callbacks or Promises with Asynchronous Code</h3>
<p>In the above example, refactored fetchThings function runs an AJAX request. It&nbsp;means that we can&rsquo;t run the function and test because we didn't know when it had&nbsp;finished running. The common way to proceed is to pass a callback function as a&nbsp;parameter to the function that runs asynchronously.</p>
<p>Apart from this, you may also use the Promise API to organise asynchronous code.&nbsp;Fortunately, $.ajax and most other of jQuery&rsquo;s asynchronous functions return a&nbsp;Promise object already, so a lot of common use cases are already covered.</p>
<div class="precode_">
<p class="commnt_">// hard to test; we don't know for how long the AJAX request will stay</p>
<p>function fetchResult() {</p>
<p><span class="dollar_">&nbsp; &nbsp;$</span>.ajax({ url: '/file_path' });</p>
<p>}</p>
<p class="commnt_">// testable; by passing a callback and run assertions</p>
<p>function fetchResultWithCallback(callback) {</p>
<p><span class="dollar_">&nbsp; &nbsp;$</span>.ajax({</p>
<p>&nbsp; &nbsp; &nbsp; url: '/file_path',</p>
<p>&nbsp; &nbsp; &nbsp; success: callback,</p>
<p>&nbsp; &nbsp;});</p>
<p>}</p>
<p class="commnt_">// also testable; run assertions after the returned Promise resolves</p>
<p>function fetchResultWithPromise() {</p>
<p>&nbsp; &nbsp;return <span class="dollar_">$</span>.ajax({ url: '/file_path' });</p>
<p>}</p>
</div>
<h3>Avoid Side Effects</h3>
<p>Avoid writing functions that alter external state while running. It prevents side&nbsp;effects that could affect your ability to test other code with confidence. Rather it is&nbsp;best to keep side effects as close to the edges of your code as possible, with as little&nbsp;&ldquo;surface area.&rdquo;</p>
<div class="precode_">
<p class="commnt_">// hard to test; we have to set up a globalListOfBikes object and set up a</p>
<p class="commnt_">// DOM with a #model&shy;list node to test this code</p>
<p>function processBikeData() {</p>
<p>&nbsp; &nbsp; const models = globalListOfBikes.map(bike =&gt; bike.model);</p>
<p>&nbsp; &nbsp;&nbsp;<span class="dollar_">$</span>('#model&shy;list').html(models.join(', '));</p>
<p>}</p>
<p class="commnt_">// easy to test; pass an argument and proceed to test its return value, without</p>
<p class="commnt_">// set any values on the window or check the DOM the result</p>
<p>function buildModelsString(bikes) {</p>
<p>&nbsp; &nbsp;&nbsp;const models = bikes.map(bike =&gt; bike.model);</p>
<p>&nbsp; &nbsp;&nbsp;return models.join(',');</p>
<p>}</p>
</div>
<h3>Don&rsquo;t change Parameters</h3>
<p>Create a new object or array in code and then proceed to add values to it. Or, use&nbsp;Underscore or Lodash to clone the passed object or array before using on it.</p>
<div class="precode_">
<p class="commnt_">// alters objects passed to it</p>
<p>function upperCaseLocation(clientInfo) {</p>
<p>&nbsp; &nbsp; clientInfo.location = clientInfo.location.toUpperCase();</p>
<p>&nbsp; &nbsp;&nbsp;return clientInfo;</p>
<p>}</p>
<p class="commnt_">// sends a new object back instead</p>
<p>function upperCaseLocation(clientInfo) {</p>
<p>&nbsp; &nbsp;&nbsp;return {</p>
<p>&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;name: clientInfo.name,</p>
<p>&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;location: clientInfo.location.toUpperCase(),</p>
<p>&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;age: clientInfo.age</p>
<p>&nbsp; &nbsp;&nbsp;};</p>
<p>}</p>
</div>
<h3>Writing Test before Coding</h3>
<p>A test driven development (TDD) is the process of writing unit tests before the code. In practice, TDD is a method that can be difficult to commit to all your code changes. But when it seems worth trying, it&rsquo;s an excellent way to guarantee you are keeping all code testable.</p>
<p>I hope these tips will help you remember, to keep your code simple and functional, this will keep your test coverage high and overall code complexity low!</p>
<p style="border-bottom: solid 1px #ccc; margin-top: -10px;">&nbsp;</p>
<p><strong>Author Bio :</strong></p>
<p><strong>Sophia</strong> is a trained WordPress developer working with WordPrax Ltd.&shy; A leading <a title="Convert HTML to Wordpress" href="http://www.wordprax.com/services/html&shy;to&shy;wordpress" target="_blank">HTML to WordPress</a> conversion services company. If you're planning to convert HTML website to WordPress for a brilliant online presence, she can help you. Some stunning articles related to website markup conversions can be found under her name.</p>
<p><strong>Social Profiles :</strong></p>
<p><a href="https://twitter.com/WordPrax" target="_blank">https://twitter.com/WordPrax</a></p>
<p><a href="https://www.facebook.com/wordprax" target="_blank">https://www.facebook.com/wordprax</a></p>
<p><a href="https://www.pinterest.com/Wordprax/" target="_blank">https://www.pinterest.com/Wordprax/</a></p>