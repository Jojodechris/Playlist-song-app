### Conceptual Exercise

Answer the following questions below:

- What is PostgreSQL?
 It's like having a digital library system that keeps track of books, borrowers, due dates, and even the relationships between different books and authors.

In the digital world, PostgreSQL is an advanced and powerful open-source database management system. Just like the librarian organizes and retrieves books, PostgreSQL stores and manages large amounts of structured data. It's commonly used by applications and websites to store information such as user profiles, product catalogs, or transaction records.

- What is the difference between SQL and PostgreSQL?
Basically PostgreSQL is a database system that can understand a specific queries and provide appropriate data in response of that query. On the other hand, SQL, is actually the programming language we use to perform queruies so that it can be understoood by PostgreSQL.

- In `psql`, how do you connect to a database?
\c database_name

- What is the difference between `HAVING` and `WHERE`?

WHERE  is a sql filter  less specific than HAVING .


- What is the difference between an `INNER` and `OUTER` join?
Inner join is a sql method that only group matching data. On the other hand, Outer join is a sql method that group matching data but also unmatching data.

- What is the difference between a `LEFT OUTER` and `RIGHT OUTER` join?
In SQL, a LEFT OUTER JOIN retrieves all rows from the left table  and the matching rows from the right table. A RIGHT OUTER JOIN fits this situation. It retrieves all rows from the right table  and the matching rows from the left table.

- What is an ORM? What do they do?

- What are some differences between making HTTP requests using AJAX 
  and from the server side using a library like `requests`?

AJAX is used on the front end to fetch and manipulate data dynamically within a web page, while the requests library is used on the server side to communicate with external services, APIs, or other servers. Each approach serves a different purpose and context within web development.


- What is CSRF? What is the purpose of the CSRF token?
CSRF is a cyberattack where an attacker tricks a user into performing unintended actions on a website they're authenticated on.

CSRF Token is like a secret code, it's a defense mechanism against CSRF attacks. It's a unique value attached to requests, ensuring that the action was intended by the user

- What is the purpose of `form.hidden_tag()`?

 It Generates a hidden input field within an HTML form, which contains a CSRF token to help ensure the integrity of form submissions and prevent CSRF attacks.
