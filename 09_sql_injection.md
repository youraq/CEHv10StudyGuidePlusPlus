# 09-SQL Injection

### SQL Injection

* Injecting SQL commands into input fields to produce output
* Double dash \(--\) tells the server to ignore the rest of the query: `' OR 1 = 1 --`, basically tells the server if 1 = 1 \(always true\)
* Basic test to see if SQL injection is possible is just inserting a single quote `'`
* **In-band SQL injection**: using same communication channel to perform attack
  * **Error-based SQL Injection**: most common used, inserting bad input to get database-level error message
    * System stored procedure
    * Illegal/Logically incorrect query: `SELECT * FROM users WHERE name='bob"' AND password =`, gets `'Unclosed quotation mark after sting " AND password='xxx"."`
  * **UNION SQL Injection**: most common used, using `UNION` clause to append a malicious query
  * **Tautology**: using always true statements to test SQL \(e.g. 1=1\)

    A **End of Line Comment**: writing a line of code that ends in comment `--`

    `SELECT * FROM users WHERE name='admin'--' AND password = 'password'`

  * **Inline Comment**: using in-line comment `/* */`
  * **Piggybacked Query**: using semicolon `;` to add malicious query after original query
* **Out-of-band SQL injection**: using different communication channels \(e.g. export results to file on web server\)
* **Blind/inferential SQL injection**: error messages and screen returns don't occur, usually have to guess whether command work or use timing to know
  * Time delay: inserting wait function for delay
  * Boolean exploitation: manipulating valid statements that evaluate to true and false in HTTP request parameter
    * `https://example.com/item.aspx?id=67 and 1=2` gets SQL query `SELECT * FROM items WHERE ID=67 AND 1=2`, if vulnerable to SQL injection, no item will show
    * `https://example.com/item.aspx?id=67 and 1=1` gets SQL query `SELECT * FROM items WHERE ID=67 AND 1=1`, if vulnerable to SQL injection, item 67 will show
  * Heavy query: in case it's impossible to use time delay function in query, generates heavy queries instead
* **MS SQL Server injection**: running commands from SQL shell by using `xp_cmdshell`
* **Countermeasures**
  * To counter **Database server runs OS commands**
    * Running database service account with minimal rights
    * Disabling commands like xp\_cmdshell
  * To counter **Using privileged account to connect to database**
    * Monitoring DB traffic using an IDS, WAP
    * Using low privileged account for DB connection
  * To counter **Error message revealing important information**
    * Suppressing all error messages
    * Using custom error messages
  * To counter **No Data validation at the server**
    * Filtering all client Data
    * Sanitizing Data
* Tools
  * Sqlmap
  * sqlninja

