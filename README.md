About this module

This module lets you use a Drupal site as a web tool to import tickets into Unfuddle from a CSV file.
I wrote this to spare our project managers some data entry drudgery.


Using this module

First, install it and its dependencies (unfuddle_api and parser_csv).

Then, configure the connection to Unfuddle on the unfuddle_api settings page.  Go to 
admin/settings/unfuddle_api and fill out all the fields:  the URL of your Unfuddle instance, an 
Unfuddle username and password that will be the ticket creator, and optionally the project ID.

Then, prepare your CSV file.  Your CSV file has to have a header row, with the exact headers that 
this module expects:

    Required columns: summary
    Optional columns: description, priority, status, assignee, milestone, hours*

"summary" is the title of the ticket; "description" is the body.  "priority" should be an integer from 
1 to 5 (1 for "lowest", 5 for "highest", defaults to 3, "normal").  "status" should be one of the 
following text strings: new, unaccepted, reassigned, reopened, accepted, resolved, closed.  To set 
"assignee" and "milestone", you'll need to go log in to Unfuddle and find the appropriate milestone
and person IDs, which are strings of digits.  *"hours" is a float (a number that can have a decimal 
point).  It's for the "Hours Estimate, Initial" on the ticket.  If you want to include hours, you have 
to apply the included patch to the unfuddle_api module, to add hours support to the createTicket 
method.


How it works

It uses the code from two modules: the Unfuddle API module (unfuddle_api) for talking to Unfuddle, 
and the CSV Parser (parser_csv) module for parsing the CSV file.  (CSV Parser also depends on FeedAPI,
so you'll have to install that one too just to enable CSV Parser, even though we don't use any of the
FeedAPI code.)
