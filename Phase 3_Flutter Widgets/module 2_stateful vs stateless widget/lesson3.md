
# Lesson 3: Comparing Stateless and Stateful Widgets

- **Overview**: Key differences between stateless and stateful widgets.
- **Key Concepts**:
  - Lifecycle Differences 🔄
  - Performance Considerations 🚀
  - Use Cases for Each Type 📝

# Lifecycle Differences 🔄

- **Stateless Widgets**:
  - Created once and never rebuilt unless the parent widget rebuilds.

- **Stateful Widgets**:
  - Have a lifecycle that includes creation, state initialization, state updates, and disposal.

# Performance Considerations 🚀

- **Stateless Widgets**:
  - Generally faster because they are not rebuilt on state changes.

- **Stateful Widgets**:
  - Slightly slower due to the overhead of managing state, but necessary for dynamic UIs.

# Use Cases for Each Type 📝

- **Stateless Widgets**:
  - Use for static content, such as a header or a label.

- **Stateful Widgets**:
  - Use for interactive or dynamic content, such as forms, animations, and user input fields.
