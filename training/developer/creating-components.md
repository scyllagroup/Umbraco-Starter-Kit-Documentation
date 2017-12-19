<div class="breadcrumbs">
[Documentation](/) / [Training](/training/) / [Developer](/training/developer/) / Creating Components
</div>

# Creating Components

## Definitions & Introduction

The word "component" can mean different things to different people, depending on the context. For the context of the Umbraco Starter Package, we are defining a component as a document type that has a corresponding view and can be rendered using Umbraco's Grid Editor, Stacked Content or Nested content.

A component can be made of other components and also of subcomponents. A subcomponent is something like a button or a text block...something that you normally would not render by itself.

As a team, we have made the explicit decision to make row based components, meaning that you cannot choose components for each column in a row. However, our components have been designed to be modular so they could be retrofitted to support column based design. We are using [Stacked Content](https://github.com/umco/umbraco-stacked-content) to manage the editing and rendering of our components. This leads to a pleasant content editing experience as well as strongly typed models and an intuitive workflow for developers.

## Building a Component By Example

### The Backoffice Work
When designing a component for integration in the backoffice of Umbraco, we must break it down and figure out what makes it a complete row. To help illustrate this, we will take a "multi card row" from our HTML Framework.

![alt text](/images/three-card-row.png "Three card row")

Looking at this row, we can clearly break it down into three "cards". We can futher break down these cards down into three more components, image, text, and a button.

![alt text](/images/card-doc-type.png "Card Doc Type")
![alt text](/images/card-umbraco-tree-view.png "Three card row")

Notice the "Button" and "Text" are document types themselves (these are subcomponents because they are not rendered on their own, they always are found in a component). These subcomponents are added to the "card" document type using nested content, a theme that is common throughout the component creation process. Nested content essentially allows you to nest and repeat document types within the properties of another document type.

At this point, we only have a card component which is _not_ ready for use in a Stacked Content property yet (because it only defines one column in the row). First we must define how they can appear in a row. For this example, we will allow 2-6 cards per row. To acheive this, we need to create another doc type, we will call it "Multi Card". We will make this a Nested Content that will allow 2-6 of the "Card" doc type.

![alt text](/images/multi-card.png "Multi card row")

Finally, to finish the backoffice portion, we can hook this up to Stacked Content by editing the data type that we are using.

![alt text](/images/configuring-stacked-content.png "Multi card row")

### Hooking Up the Frontend

Now that we have all of the backoffice work done, we need to hookup the frontend view so the content editor can see what they just created and we can see it on the public facing site.

First things first, you need to run the models builder from Visual Studio so the doc types that we just created get created into models.