# Concise Guide to Identifying (and resolving) a Web Platform Bug

Web developers rely on a great many software packages, libraries, and tools to build applications. End users expect to have the same experience on these applications regardless of their environment. The web is an ever-evolving platform to target as platforms add new features and APIs, and web standards bodies incorporate them into final specifications. Thus, hitting a bug can be a frustrating experience particularly when it is not clear _where_ the bug originates - is it in your code, the library code, the browser, the specification, or something else? Below are some questions to guide you through determining whether you have found a platform bug, and how to report it.



1. **Reduce, reduce, reduce**

    Bugs often appear in complex setups, and it can be unclear which part or which feature the bug is stemming from. The first step of any bug investigation is to eliminate code unrelated to the bug so that its causes can be more clearly investigated. This is called a _reduced testcase_ or _reduction_. A reduction will not only help you understand what is happening much better, it will also help you communicate about the issue with spec developers, browser engineers, and other stakeholders. Moreover, it will also help your bug being fixed faster: bugs that include links to reduced testcases are generally triaged a lot faster.  \
 \
Copy over the current page, script, or even your entire project and start aggressively *removing* code, checking that you can still reproduce the bug with the code left. This also applies to the UI: Shorten any non-relevant text, eliminate any unrelated CSS styling, simplify any HTML subtree. You can almost always reduce more than you think. Most bugs can be reduced to &lt; 20 lines of code, often significantly less than that. If you’ve used unit tests before, it's a very similar process: imagine that you are writing a unit test to test if that particular bug is fixed.  



    These additional resources may be helpful in learning how to create better reduced testcases: 
	* [https://webkit.org/test-case-reduction/](https://webkit.org/test-case-reduction/)
   * [https://css-tricks.com/reduced-test-cases/](https://css-tricks.com/reduced-test-cases/) 


2. **What kind of bug do you have?** \
In addition to the cross-browser compatibility bugs you might run into as you build your application, you may also hit bugs in a test environment, or in sample code/documentation, or in areas where a feature has been underspecified. Interoperability bugs deal with situations in which browsers behave differently from each other, and the specification either: agrees with one or more; requires a behavior that is not implemented anywhere; or is not clear about the correct behavior. Sometimes, browsers will agree on a behavior, and the relevant specification will be inaccurate, or underspecified for the correct behavior - let’s call these clarification bugs. \
 \
To determine which is the case (and that you’re interpreting the issue correctly as well) start with reputable source documentation for the feature you are trying to use, such as [MDN Web Docs](https://github.com/mdn/content) or the documentation site for your browser engine. These resources will often note where there are known bugs, and will typically link you directly to the relevant specification(s) and their test suite(s) from these pages. A careful read of the spec may further clarify which kind of bug you are dealing with. 

3. **Does the problem exist across multiple browsers?** \
Before you report the bug, you’ll want to have a good understanding of its behavior under certain conditions and which browsers may be impacted. Verify your bug by testing in multiple browsers - and multiple versions of the browser, such as the latest stable and latest nightly edition. This information is critical to writing a great bug report that browser engineers and spec authors can use. If you’re seeing what appears to be the same (incorrect) behavior across multiple browsers, you may want to first create a reduced test case to determine if your interpretation is faulty, or if supporting documentation needs to be improved. If you’re seeing different behavior across multiple browsers, you’ve found a compatibility bug. Check whether others have reported your bug.  
  

4. **Is the feature/API you are trying to use available in all browsers?** \
Web standards are often updated on a “living” basis - meaning that the feature may be made available to use by browsers before it’s been enshrined into the specification, or that the specification has described intended behaviors that have not yet been put into implementations by all browsers. It also means that certain features may have been deprecated and are no longer available. Tools such as the Browser Compat Data tables and caniuse.com are great resources to help determine whether a feature is ready for you to use in production. Generally, these tables are updated as web specifications advanced through their respective committees, and as test suites and supporting documentation are added. Experimental features may also be represented in the data, but are often marked as such and should be used carefully - experimental features may change their behavior without notice. If you find a bug on an experimental feature, it can be really helpful to report it - it can provide the feature developer more information about developer behavior. 

5. **Is there a test for the feature you are using, and if so, is it passing or failing?** \
Most modern web standards have either a test suite or a reference implementation associated with them: for HTML and CSS, the Web Platform Tests project contains the most authoritative test suite; Javascript’s test suite is called Test262. If there is a test suite, run tests relating to the bug you found in the implementation you were using.   Does your implementation run the tests correctly? If the implementation seems to be correct, double-check your application code - you may have found an issue with the way a library or tool you’re using has implemented the standard, rather than an issue with the standard itself.  


    If there is a reference implementation, try the scenario in which you found a bug in the presumably standard-compliant reference implementation. If you see behavior you think is buggy in the reference implementation, the specification itself may need fixing. 


6. **Have other developers reported a similar issue?** \
Check whether your bug, or similar bugs, have already been filed - look at the repositories for the browser engines, the specification (final and draft versions, if these are kept separately), and test suites. Look at what other developers have reported, and whether the appropriate team has already provided a status update or other information relevant to your issue. Duplicating a bug report is generally seen as poor etiquette, but you may be able to add additional information, context, or data to an existing bug report that helps the team.   \
 \
If you’ve found a new bug - congratulations! Web platform bugs can be very fun problems to solve, but you may also find that you have to work a bit differently to resolve them. In addition to thoroughly understanding the bug, you may find that you have to do a lot of leg work to help others understand it - and agree to the resolution. It may require you to build consensus between engineers with competing implementations, contribute tests, or present research about usage patterns to spec proposal authors. 

**Additional Resources:**



* Web Platform Contribution Guide [https://wpc.guide/bug-guide/](https://wpc.guide/)
* Web Compat Project [https://webcompat.com/](https://webcompat.com/)
* How to Report a Bug [http://testthewebforward.org/docs/bugs.html](http://testthewebforward.org/docs/bugs.html)
* Case Study: The Caper of the Flakey Test [https://bocoup.com/blog/the-caper-of-the-flaky-test](https://bocoup.com/blog/the-caper-of-the-flaky-test)
