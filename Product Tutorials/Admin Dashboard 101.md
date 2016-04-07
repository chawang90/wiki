# Admin Dashboard 101

In general, we only use the Admin Dashboard for tasks that our site doesn’t yet support for cooks and customers (e.g. refunds). As much as possible, we want to use the same flows that our cooks/customers are using so that we can identify bugs and/or feature improvements.

To access the Admin Dashboard, visit this webpage: https://josephine.com/admin and use our super secure login credentials:

| **User name** | **Password** |
| --- | --- |
| tal | saf |

## Use the Admin Dashboard for:
- Add balance to a customer (or your own!) Josephine account
- Reduce the number of portions that a customer has ordered
- RSVP a customer for a meal without charging them
- RSVP a customer for a meal without sending them any notifications
- Sending a newsletter
- Creating a promo code

### Add balance to a customer (or your own!) Josephine account
1. Go to this webpage: https://josephine.com/admin/users
2. Find the appropriate user (Cmd+F is your friend!)
3. Select ‘Edit User’
![edit user](http://i.imgur.com/TX6fqLI.png "edit user")

4. Add balance!

### Reduce the number of portions that a customer has ordered
1. Go to this webpage: https://josephine.com/admin/users
2. Find the appropriate user (Cmd+F is your friend!)
3. Select ‘See Orders”
4. Find the appropriate meal
5. Reduce portions (so that sales screen is accurate)
6. Add credit to customer account or refund through Stripe (so that the customer actually gets their $$$ back)

### RSVP a customer for a meal without charging them, without sending any notifications, or both
1. Go to this webpage: https://josephine.com/admin/users
2 Find the appropriate user (Cmd+F is your friend!)
3. Select **Create Order**
![create order](http://i.imgur.com/OgtFWwE.png "create order")

4. Find the appropriate meal
5. Select the portion and add-on number
6. Check the **Skip Payment**, **Skip Messages**, or both
![skip payment/messages](http://i.imgur.com/msB7jID.png "skip payment/messages")

## Login as an Admin (your own Josephine account) to:
- Access and make edits to a cook meal page
- Access and increase customer orders from a cook sales page
- Access a cook’s reviews page

### Access and make edits to a cook meal page
1. Select meal from Josephine home page
2. Add **/edit** to the meal URL
3. Make and save your edits!

### Access and increase customer orders from a cook sales page
1. Select meal from Josephine home page
2. Add **/sales** to the meal URL
3. Increase and update a customer order!

### Access a cook’s reviews page
1. Select meal from Josephine home page
2. Add **/reviews** to the meal URL
3. Look at the reviews!

## Login in as Customer to:
- Place an order without skipping payments or notifications
- Send the customer a link to review a meal

### Place an order without skipping payments or notifications
1. Select **Login in as user** from the account menu on the Josephine home page
![log in as user](http://i.imgur.com/IKRsDZ8.png "log in as user")

2. Find and select the appropriate user (Cmd+F is your friend!)
3. Find the appropriate meal
4. Place order through the normal ordering flow

### Send the customer a link to review a meal
1. Select meal from Josephine home page
2. Add **/review** to the meal URL
3. Send the hyperlink to the customer!
