# lesson learned
- It is common that applications to use data from a single request in multiple different queries. If The condition `OR 1=1` reaches an `UPDATE` or `DELETE` statement, for example, it can result in an accidental loss of data.
- Escaping points
  - ost SQL injection vulnerabilities occur within the `WHERE` clause of a `SELECT` query
  - In `UPDATE` statements, within the updated values or the `WHERE` clause.
  - In `INSERT` statements, within the inserted values.
  - In `SELECT` statements, within the table or column name.
  - In `SELECT` statements, within the `ORDER BY` clause.


---
The goal for this challenge is to cause the application to display one or more unreleased products. 
---
![](https://github.com/sinSeptember/CTF/blob/main/portSwigger/sqli/assets/sqli1.0.png)
---
`SELECT * FROM products WHERE category = 'Gifts' AND released = 1`

In the query we have released value = 1 assume its true, lets true to get 0 to see if we can get the unreleased products and retrieving hidden data.
 ---
![](https://github.com/sinSeptember/CTF/blob/main/portSwigger/sqli/assets/1.2.png)
---
The quote reflected to the main page, lets add boolean condition and some spicy comments
---
![](https://github.com/sinSeptember/CTF/blob/main/portSwigger/sqli/assets/1.3.png)
"SELECT * FROM products WHERE category = 'Gifts'' OR 1=1 -- `AND released = 1"`
