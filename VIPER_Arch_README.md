VIPER Architecture Guideline
================
# Role Play

## *Module
The highest level of VIPER's components, which means each Module contains View, Interactor, Presenter, Entity, Router. The concept of VIPER divides the application's functionality into modules (Modularization).

## *View
The view controller doesn’t and shouldn’t care who and how business logic is done. <u>View controller only response for "Detect" user behavior, "Request" data, and "Recieve" the response data (ViewModel), then "Display" the updated view with data.</u>

A typical scenario goes like. The user taps a button in the app’s user interface. The tap gesture comes in through the IBActions in the view controller. The view controller constructs a request object and sends it to the interactor. The interactor takes the request object and performs some work. It then puts the results in a response object and sends it to the presenter. The presenter takes the response object and formats the results. It then puts the formatted result in a view model object and sends it back to the view controller. Finally, the view controller displays the results to the user.

## *Interactor
The interactor contains your app’s business logic. The user taps and swipes in your UI in order to interact with your app. The view controller collects the user inputs from the UI and passes it to the interactor. It then retrieves some models and asks some workers to do the work.

## *Presenter
After the interactor produces some results, it passes the response to the presenter. The presenter then marshal the response into view models suitable for display. It then passes the view models back to the view controller for display to the user.

## Worker
A profile view may need to fetch the user from Core Data, download the profile photo, allows users to like and follow, …etc. You don’t want to swamp the interactor with doing all these tasks. Instead, you can break it down into many workers, each doing one thing. You can then reuse the same workers elsewhere.

## Router
The router variable is a reference to {Scenes}Router and is used to navigate to different scenes. When the user taps the next button to navigate to the next scene in the storyboard, a segue is trigged and a new view controller is presented. A router extracts this navigation logic out of the view controller. It is also the best place to pass any data to the next scene. As a result, the view controller is left with just the task of controlling views.

## Models
In order to completely decouple the Clean Swift components, we need to define data models to pass through the boundaries between them, instead of just using raw data models. There are 3 primary types of models:

- Request – The view controller constructs a request model and passes it to the interactor. A request model contains mostly user inputs, such as text entered in text fields and values chosen in pickers.

- Response – After the interactor finishes doing work for a request, it encapsulates the results in a response model and then passes it to the presenter.

- View Model – After the presenter receives the response from the interactor, it formats the results into primitive data types such as String and Int, and stuff them in the view model. It then passes the view model back to the view controller for display.


### Where is the builder?
Example1: Modules/Post Discovery
builder is at /Modules/Post Discovery/Module/PostDiscoveryModule.swift

Note: If Modules has builder, which it must locate in /Module/{Name}Module.swift, and it must use {module_name}Scene.swift.

Example2: Modules/Registration
builder is at /Modules/Wireframe/Registration Wireframe.swift

But the builder in ViewInterface is less complex, so it will use init to do the job:

```
required init(root: RootWireframeInterface?, view: RegistrationViewInterface)
```

### When to use {module_name}Scene or {module_name}ViewInterface to design a VIPER's View protocol?

Basically, if the Module is fully functional with more complex user interaction, which means it responsible for one of the main features in the app, then it will go the Module/Scene solution.

If the Module is less complex, it may be just a one view feature with few functions, then it will go to the Module/ViewInterface solution.

#### Definition of Scene and View:

View (noun)- 1. the ability to see something or to be seen from a particular place
Example: The house came into view as we got near.
2. a particular way of considering or regarding something; an attitude or opinion; opinion, point of view, etc.
Example: He has strong political views.
(verb)- look at or inspect (something); 
Example: The public can view the famous hall with its unique staircase
Scene- (noun) 1.the place where an incident in real life or fiction occurs or occurred.
Example: This is the scene of the crime.
2.a sequence of continuous action in a play, movie, opera, or book.
Example: I love the scenes in that movie.
Reference: https://hinative.com/en-US/questions/80505

#### Note:
ZX's supplementary explanation, using the <u>underline</u> to hightlight. <br>
\* sign means it is the core idea about Clean Swift.

--------
### Reference
https://clean-swift.com/clean-swift-ios-architecture/

### Copyright
Copyright © 2019 ZX - All Rights Reserved

### Permission
We do not want anyone to clone our source code, but if for any reason our code is cloned or otherwise obtained, we want to have a license that does not allow disclosure of any kind.


