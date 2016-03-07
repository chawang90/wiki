Some notes on best practices for placing/adding/refunding/canceling orders for customers.

## Placing a new order

- Always log in as a user and place the order for them using the website the same way they would. 
- Don’t forget to log out afterwards.
- If you need to add an RSVP from the backend, use the orders page (/admin/users/####/orders). Depeneding on the situation you can choose to skip payment or skip customer notifications for the new order. This method should only be used if logging in as a user won't work for some reason.


## Adding to an existing order

- Always use the meal check in screen (/sales) to add to or increase an existing order. 
- This will automatically charge the customer using the card or credit on file.

## Refunding or canceling an existing order

- First, refund the customer on Stripe for the appropriate amount from the associated charge
- Then, use the orders page (/admin/users/####/orders) to reduce the # of portions ordered to the correct amount.
- Changes on this page to portions ordered are entirely superficial and exist only in our system - they do not communicate with Stripe in any way shape or form.
