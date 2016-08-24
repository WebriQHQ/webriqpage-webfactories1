---
title: Effective Guide to Write Testable JavaScript
shortdesc: " With the growth in technology, we have earned better options for unit testing JavaScript. Whether we are using Node paired with a test framework like Mocha or Jasmine, in a headless browser, we have a variety of options. However, it does not mean that the code which is tested is as easy on us as our tools are!  "
cmsUserSlug: effective-guide-to-write-testable-javascript
date: 2016-08-04T16:00:00.000Z
banner: /img/uploads/testable-javascript2.jpg
categories: recent-blog
writer: Sophia
---

With the growth in technology, we have earned better options for unit testing JavaScript. Whether we are using Node paired with a test framework like Mocha or Jasmine, in a headless browser, we have a variety of options. However, it does not mean that the code which is tested is as easy on us as our tools are!

Organizing and writing code is easily testable and requires some efforts, but functional programming concepts are inspired by few patterns which can help in testing our code.

Here in this article, we will go through some useful tips and patterns for writing testable code in JavaScript.

**Keep Business Logic and Display Logic Separate**

JavaScript­based browser application primally listens to DOM events which is triggered by the end user. It is always tempting to write an anonymous function that does maximum work right while setting up DOM event listeners. This can create aloft both in lines of code and the time for practising. So, it is recommended to, write a named function and pass it to the event handler. This applies to more than the DOM, though. Many APIs, both in the browser and in Node, are serving this purpose.

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