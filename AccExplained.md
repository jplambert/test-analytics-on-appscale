#  Introduction #

Test Analytics allows you to efficiently construct an ACC model for your project.  This ACC model, shorthand for Attributes-Components-Capabilities, will in many ways replace a conventional test plan.  It's faster to write, can direct you toward missing coverage, and is the framework for calculating a risk surface map for your project.

For a moderately sized project, an initial ACC breakdown might take 20 minutes to an hour.  In this time, you'll define the three parts of the ACC model for your project: Attributes, Components, and Capabilities.

# Why ACC? #

Many test plans suffer from one or more common problems:
  * Difficult to keep up-to-date and become obsolete
  * Written ad-hoc, leading to holes in coverage
  * Ignored after initial creation or review
  * Give little actionable data
  * Disorganized, difficult to consume all related information at once

In addition, we've found that when trying to utilize risk-based testing methodologies, a conventional test plan doesn't give a good visual map of the project -- there's no great place to start or end when determining risk, nor do they provide a good mechanism by which to visualize the risk.

ACC aims to solve that in a simple way.  It's an easy-to-follow process that can be applied consistently to projects quickly.  At the end of the process, you have a system of coherent and logically-related elements, in a form which is easy to digest.

# What is ACC? #

ACC consists of three different parts that define your system under test: Attributes, Components, and Capabilities.  An easy way to think of each of these elements is by relating them to a part of speech relating to your project.

  * **Attributes (adjectives of the system)** are qualities and characteristics that promote the product and distinguish it from the competition; examples are "Fast", "Secure", "Stable", and "Elegant".  A product manager could have a hand in narrowing down the list of Attributes for the system.

  * **Components (nouns of the system)** are building blocks that together constitute the system in question. Some examples of Components are "Firmware", "Printing", and "File System" for an operating system project, or "Database", "Cart", and "Product Browser" for an online shopping site.

  * **Capabilities (verbs of the system)** describe the abilities of a particular Component in order to satisfy the Attributes of the system. An example Capability for a shopping site could be "Processes monetary transactions using HTTPS". You can see that this could be a Capability of the "Cart" component when trying to meet the "Secure" Attribute. The most important aspect of Capabilities is that they are testable.

Defining Capabilities requires you to visit each intersection point between Attributes and Components; this often can lead to discovery of areas which otherwise may have gone unrecognized or untested in a conventional test plan.  This could be as simple as assuring there is thought put into the security of an entire system (via the Attribute "Secure"), or details specific to your project when considered to specific characteristics you want your product to exhibit.  It can also help assure consideration is given to all qualities are considered as new Capabilities are added to your product.

# How? #

Constructing an ACC model is designed to be a simple, methodical process that can be executed quickly.  No special tools are required to construct an ACC model -- you could draft one on paper, or a whiteboard -- but Test Analytics was specifically designed to make construction a breeze.  In addition, it has a few built-in visualizations that add value to the model you make.

## Define Your Attributes ##

The first step is to figure out your product's Attributes.  To start, think about the qualities of your product that are critical to its success.  You can also consider what differentiates your product from any competitors. Attributes are big-picture items; don't worry if they seem vague at first.

Here are some common items we've noticed have appeared in several projects, which might spark some ideas:

  * Secure
  * Fast
  * Powerful
  * Stable
  * Personal
  * Social

You can define these on the Attribute page of Test Analytics.

## Define Your Components ##

The Components of your project are the big pieces of your application.  They might echo how a developer on your product would split the project apart.  In an e-commerce website these could be things like "Shopping Cart" or "Account Page".

Since the Components of projects can vary a lot depending on the type of project it is, there's not a list of "typical" parts.  Here are a few that may help you think how to divide your project:

  * Database
  * API
  * Search
  * Sharing
  * Login
  * Shopping Cart

You enter these, similar to Attributes, but on the Components page of your Test Analytics project.

## Define Your Capabilities ##

Now comes the fun part!  Capabilities are the things your project does.  To compare to a test plan, a Capability might cover a group of related tests all in one succinct sentence.

A Capability is tied to one specific parent Attribute and Component -- a Capability will be what your product needs to do to make sure a Component fulfills the Attribute.  To use some of the previous examples, you would define capabilities under pairs like "Database is Secure" or "Search is Fast".

Each Attribute and Component pair could have several Capabilities associated with it, or possibly none if that combination doesn't make sense.  **Login** is **Social** may not have any Capabilities associated with it whereas **API** is **Powerful** might have several.

Here's some examples of Capabilities:

  * **Database** is **Secure**: "All credit card information is stored encrypted", "Passwords are not stored plain-text"
  * **Search** is **Fast**: "All search queries return in less than 1 second"

To define your Capabilities, Test Analytics presents you with a grid of your Attributes versus Components.  You can select a cell which represents an Attribute and Component pair.  After selecting, you can then start defining Capabilities for that pair.

This is where value of ACC can shine: by showing a grid pairing what qualities of your application are important against the parts of your application, it can yield tests you may not previously have considered.

The Capabilities themselves should not be test cases themselves: they're intended to be higher level.  They can serve as a good starting point for a manual testing tour, or as a classification under which you can define test cases.

Once you've defined your Capabilities, you're ready to start using the risk assessment portions of Test Analytics to start visualizing the parts of your application that need attention.