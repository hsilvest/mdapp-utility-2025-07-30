## Model‑Driven App Utility – Telephone Requirement

This repository contains a small JavaScript utility function designed for Microsoft Power Apps model‑driven applications.  The function demonstrates how to follow Dynamics 365 JavaScript best practices—using proper namespacing, avoiding global variables, and adding descriptive comments—while delivering a useful piece of functionality that can easily be adapted to other forms.

### What it does

The utility automatically toggles the **Telephone** field (`telephone1`) between a required and optional state depending on the user’s selection in the **Preferred Contact Method** (`preferredcontactmethodcode`) field.  If the user selects **Telephone** as their preferred method of contact, the script sets the telephone field to *Required* and displays an informational notification on the form.  For any other preferred contact method, it resets the telephone field to *Optional* and clears the notification.

### Why this is useful

In real‑world scenarios, business rules often dictate that certain fields become mandatory based on other selections.  For example, if a customer prefers to be contacted via phone, capturing their telephone number becomes critical.  Doing this validation on the form ensures data quality at the point of entry and improves the user experience by providing immediate feedback.

### Files included

| File | Description |
|---|---|
| `telephoneRequirement.js` | Contains the namespaced JavaScript functions used to handle the telephone requirement logic.  It exports two methods: `onLoad` (registered on the form’s `onLoad` event) and `toggleTelephoneRequirement` (a helper method you could reuse elsewhere). |

### How to use

1. **Add the web resource**: Upload the `telephoneRequirement.js` file as a JavaScript web resource in your Dynamics 365 or Power Apps environment.
2. **Add to form libraries**: Open the form editor for your Contact (or other) form, and add the JavaScript web resource to the form’s libraries.
3. **Register the events**:
   - **Form onLoad**: Register `MyCRM.ContactForm.onLoad` on the form’s `onLoad` event and ensure that the execution context is passed as the first parameter.
   - **Preferred Contact Method onChange**: The provided code automatically registers a change handler for the `Preferred Contact Method` field when the form loads; no manual registration is necessary.
4. **Publish the form**: Save and publish your customizations.

### Customization notes

- **Option set value**:  In standard Dynamics 365 deployments, the option set value for **Telephone** in the `preferredcontactmethodcode` field is `2`.  If your environment uses a different value or a custom option set, update the constant `PREFERRED_METHOD_PHONE` in the script accordingly.
- **Field names**:  The attribute logical names (`preferredcontactmethodcode` and `telephone1`) correspond to the default Contact entity schema.  If you’re using a different entity or custom fields, replace these names with your own logical names.
- **Notification ID**:  The script uses a notification ID of `phoneRequirement` when displaying a form notification.  If you integrate this script with other customizations that also use form notifications, ensure the IDs are unique to prevent accidental removal of unrelated notifications.

This is the first in a series of small utilities.  New repositories will be created each day over the coming week, featuring different JavaScript helpers for model‑driven applications.  Feel free to adapt and extend these examples to suit your own business requirements.
