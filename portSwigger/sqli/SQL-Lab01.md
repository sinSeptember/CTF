The goal for this challenge is to cause the application to display one or more unreleased products. 
![[sqli1.0.png]]
`SELECT * FROM products WHERE category = 'Gifts' AND released = 1`
In the query we have released value = 1 assume its true, lets true to get 0 to see if we can get the unreleased products and retrieving hidden data.
 
![[1.2.png]]
The quote reflected to the main page, lets add boolean condition and some spicy comments
![[1.3.png]]