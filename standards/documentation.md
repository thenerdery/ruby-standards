# Documentation

Good documentation makes a long-lived project easier to understand and maintain. It can help introduce new developers to an unfamiliar codebase, or serve as a reference point for the team coming back to code 6 months later. Documentation may also cover important architectural decisions, complex business logic, or quirks and workarounds of the tech we're working with. Just as we put effort into making tests that last to ensure our application is stable and robust, we also focus on providing meaningful documentation.

A great article on improving Rails-based documentation published by Aaron Sumner can be found here. Many of the practices described below are pulled from his philosophy.

## Start with the README
Your application’s README is still its gateway, the first thing new developers will likely read when they access its source code. If your app’s README consists of the default given to every new Rails app, it’s time to change it.

Your README should include:

* A brief description of what the application does.
* How to install dependencies, especially those that are more complex than a simple `bundle install`. For example, if I need to to install Redis or ImageMagick to work on the app, or configure environment variables to talk to external services, let me know up front.
* How to run the application’s test suite, to verify that setup was successful. Again, note special external dependencies, like PhantomJS.
* How to generate the docs, to get to a more detailed description of the application’s code.

## Remove generated documentation from source control

The HTML version of your Rails docs will need to be regenerated regularly, in order to keep up with the code they explain. Ignoring the doc/app directory makes sure that stale documentation doesn't stick around from commit to commit, and just makes commits cleaner in general. This is why it’s important to mention how to generate the docs in your README as they won’t be easily accessible, otherwise.

## Write clear documentation

* __Don't assume knowledge of the business__: If you've been working in the application for awhile, the names you've given your classes and methods may seem obvious, but to a newcomer they can be a large hurdle to overcome. Help explain ___why___ things are called what they are.
* __Do assume knowledge of Rails__: The rule of thumb is to document ___why___, now ___how___. Document under the assumption that the reader can read Ruby code, or at least knows how to search Google or Stack Overflow to learn more about specific methods.

## YARD + RDOC

We recommend utilizing the [YARD gem](http://yardoc.org/) in conjunction with the standard [RDOC documentation system](http://rdoc.sourceforge.net/doc/) to provide clear and consistent documentation on our projects. YARD fills in some of the gaps that RDOC does not address by allowing us to organize our codes meta and behavioural data through the use of [tags](http://www.rubydoc.info/gems/yard/file/docs/Tags.md). Not only does this create consistency between our projects, but it also more closely represents the way documentation blocks are handled via the other disciplines at The Nerdery, making point of entry into the language easier for an outside developer to understand.

### The `.yardopts` file

YARD accepts [many different options](http://www.rubydoc.info/gems/yard/YARD/CLI/Yardoc), and for ease of development it is recommended that you use a `.yardopts` file to outline these options. YARD will automatically parse this file every time `yard` is run and conform to it's requests. A recommended starter file is outlined below

    --private
    --markup=markdown
    app/**/*.rb -
    lib/**/*.rb -
    
This starter file tells YARD to document all private methods, interpret and render markup in the docblocks, and generate documenation for all *.rb files located in the app and lib folders. 

### Markdown format

YARD supports [multiple formats](http://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md#Which_Markup_Format_) for it's markup rendering. Due to the industry wide acceptance and use of standard Markdown for most circumstances we recommends utilizing `markdown` as the format of choice on our Ruby projects.

### Do's & Dont's

[YARD](http://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md) and [RDOC](http://rdoc.sourceforge.net/doc/) are very extensive. We encourage you to read over the documentation and explore the vast amount of options available to you, however documenting too much, or using unwise practices can make your documentation just as bad as not having any at all. In this section we'll cover our recommended practices while using this documentation engine combination:

#### __DO__ 
* Provide a documentation block at the top of every class file. This should contain:
    * A description of the classes function (___why___ not ___how___) within the application.
    * Your [author name](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#author).
    * A [version number](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#since) of when the class was first added to the project. 
* Provide a documentation block at the top of every method with the exception of standard CRUD controller operations (`index`|`new`|`create`|`show`|`edit`|`update`|`destroy`). This should contain:
    * A description of the methods function (___why___ not ___how___) within the class.
    * All [paramaters](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#param) of the method.
    * All [options](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#option) if an options Hash is being used as a param.
    * A [return](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#return) value. If no return value is produced by the method `void` would be the expected return.
* Document all [model attributes](http://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md#Documenting_Attributes). Obviously this means writing each to their own line and not strining them together via commas. In the event you need separate documenation for the attributes getter and setter then follow [these steps]( http://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md#Documentation_for_a_Separate_Attribute_Writer).
* Use [Duck-Type specifiers](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#Duck-Types) when appropriately.
    
#### __DON'T__
* Use YARD based [reference tags](http://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md#Reference_Tags). Although this methodology reduces DRY documentation it also enforces coupling.
* Overload your documentation. Having overly cumbersome documentation is just as bad as having no documentation at all. Keep your docblocks small, concise, and to the point. Often throughout the RubyDocs and YARD documentation pages you will be presented with large docblocks filled with markdown and html structures, unless this type of documentation adds significant understandability to the class or method we ask that you refrain from emulating this. "Short, Sweet, To The Point"
* Don't create [custom tags](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#Adding_Custom_Tags) unless absolutely vital to the understandability of the documentation. If you are presented with a case where you do need to make them ensure that you are always namespacing them.