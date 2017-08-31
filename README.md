# Web-Storage---SlashDB
Using SlashDB and Browser Local Storage for Cached Data Presentation
Storing information locally within modern browsers local or session storage facilities is a great strategy for assuring that data is available in the case when users are offline (not connected to the Internet) and still want to use back-end data that you can locally cache.  The usual way that developers have stored data the web’s stateless HTTP transport layer has been via cookies. But cookies have restrictions that you will want to avoid especially if you are going the distance of storing relational data that is accessed via SlashDB through Restful API calls.  Basic cookie limitations include:
Cookies only allow for 4KB of storage
Cookies have a bad rap these days as advertising networks are dropping third party cookies in proliferation.  Cookies enable servers to aggregate requests—and thus data—around a particular user.
Cookies can add to the load of the page from that domain
Using local storage can help you cut down on requests for database data especially as users go from page to page on your website.  You can think of local storage as a data cache that has a 5MB storage limit.    Security concerns are similar to any other concerns that would be found around sessions and cookies in any language.
Using HTTP Restful API calls via SlashDB and continuously writing the response data to the local or session storage is easy to do and allows for uninterrupted application use if your users experience Internet connectivity problems or simply wish to work offline with SlashDB-sourced data (e.g. when flying in a plane).   All that needs to be done is a modification of the localStorage object in Javascript and this blog post will show you a full example that you can quickly experiment with and use in your SlashDB web-based application.  The localStorage object has convenient getItem and setItem methods that make it a cinch to work with the browsers local storage and persist data from session to session.  This means that once the session (domain / origin) is run up again in the browser, the user doesn’t even have to be connected to the Internet to use the application, if the server-side relational data does not have to be immediately fresh.  And you can use sessionStorage instead of localStorage if you want the data to be maintained and associated to the origin (your domain) only until the browser window is closed.

These storage techniques use the individual column data returned via SlashDB to store this data as key/value pairs as seen here:





<script>
  localStorage.setItem("BillingCountry", "Brazil");
  sessionStorage.setItem("BillingPostalCode", "12202-9293");
</script>



In the example code shown below, we made an HTTP API call via SlashDB and asked for each of the Email addresses from the sample Chinook datastore.  This was done with a JSON formatted response using this URL:  http://demo.slashdb.com/db/Chinook/Customer/Email.json
SlashDB has implemented storage of sample Chinook database data.  Details of this relational database example project can be found at https://github.com/lerocha/chinook-database.  The Chinook data model represents a digital media store (e.g. iTunes), including tables for Customers as in the example below where we do a full table scan for their Email addresses.

When viewed in Safari through the Web Inspector we see the key/value pairs for the local storage for the current domain.  Additionally, we see the results of reading (again, using the getItem method on the localStorage Javascript object) the data and presenting it, one Email per DIV tag:
