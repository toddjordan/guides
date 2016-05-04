Now that we are displaying a list of rentals on our main application page, we want to add the ability to drill down on a listing and see more details and larger images.
We also want the ability to reserve a rental.

We want a distinct URL to represent each of these logical pages, so that users can bookmark rentals they like and make use of the browser's back button.

Here's a list of existing and proposed routes for Super Rentals

* / Home page - Redirect to /rentals
* /about - Information about the company 
* /rentals - Filter and view a list of rentals
* /rentals/_dasherized-rental-name_ - View a specific rental
* /rentals/_dasherized-rental-name_/reserve - Make a reservation for a rental
