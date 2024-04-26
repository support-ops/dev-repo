---
title: Handling Null ItemSource in Progress® Kendo UI® Application
description: Learn how to manage scenarios where the ItemSource is null in a Kendo UI application.
type: how-to
page_title: How to Handle Null ItemSource in Kendo UI Applications
slug: handling-null-itemsource-kendo-ui
tags: kendo-ui, itemsouce, null, handling
res_type: kb
related_questions:
  - How to deal with null ItemSource in Kendo UI?
  - What to do when ItemSource is null in a Kendo UI application?
  - How to handle data binding issues in Kendo UI?
  - Can ItemSource be null in Kendo UI components?
  - How to ensure Kendo UI components work with null sources?
category: knowledge-base
ticketid: 1584467
---

## Environment

| Property | Value                                     |
|----------|-------------------------------------------|
| Product  | Application for Progress® Kendo UI® 2022.3.913 |

## Description

In some cases, when working with data in a Kendo UI application, the source of data (`ItemSource`) might be set to `null`. This can lead to unexpected behavior or errors. Understanding how to handle such scenarios ensures the application remains robust and error-free.

## Solution

To effectively handle a scenario where `ItemSource` is `null`, follow these guidelines:

1. **Initialize `ItemSource`**: Before binding data to a Kendo UI component, ensure that `ItemSource` is initialized to an empty collection rather than `null`. This prevents the component from encountering a `null` source, which could lead to errors.

2. **Check for `null` Before Binding**: Always check if the data source is `null` before binding it to a UI component. If it is `null`, initialize it as an empty collection or provide a default value that the component can handle without issues.

3. **Use Fallback Values or Placeholders**: For components that display data (like grids or lists), you can implement fallback values or placeholders that appear when the `ItemSource` is `null`. This approach improves user experience by providing feedback that the data is currently unavailable.

4. **Implement Null Object Pattern**: In some situations, using the Null Object pattern can simplify the handling of `null` values. This involves creating a class that represents a non-functional implementation of an expected data structure. Instead of using `null`, use an instance of this class, which the components can safely interact with without performing any operation.

By following these steps, you can ensure that your Kendo UI application gracefully handles cases where `ItemSource` is `null`, maintaining stability and providing a better user experience.

## Notes

- Always validate data before binding to components to avoid unexpected errors.
- Consider the specific requirements and behavior of each Kendo UI component when implementing null handling strategies.

## See Also

- [Kendo UI Documentation](https://docs.telerik.com/kendo-ui/)
- [Handling Null Values in C#](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/nullable-types/)
- [Design Patterns: Null Object](https://refactoring.guru/design-patterns/null-object)
