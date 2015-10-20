Some notes on best practices for placing/adding/refunding/canceling orders for customers.

## Placing a new order

- Always log in as a user and place the order for them using the website the same way they would. 
- Don’t forget to log out afterwards. 

## Adding to an existing order

- Always use the meal check in screen (/sales) to add to or increase an existing order. 
- This will automatically charge the customer using the card or credit on file.

## Refunding or canceling an existing order

- First, refund the customer on Stripe for the appropriate amount from the associated charge
- Then, use the old user RSVPs page (/admin/users/####/rsvps) to reduce the # of portions ordered to the correct amount. 
- Note that there is no way to do this for add-ons at the moment, only portions
- This page is a bandaid solution of sorts - it is a page that exists SOLELY so we can refund orders right now, until a better solution exists. 
- Changes on this page to portions ordered are entirely superficial and exist only in our system - they do not communicate with Stripe in any way shape or form.