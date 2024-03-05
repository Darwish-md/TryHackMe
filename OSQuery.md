Osquery is an open-source agent created by Facebook in 2014. It converts the operating system into a relational database. It allows us to ask questions from the tables using SQL queries.
- To get help with the tool, `.help`
- To list all tables, `.tables`.
- To list all the tables with the term user in them, we will use `.tables user`.
- To list a table's schema with the following meta-command: `.schema table_name`.
- Here is the documentation: `https://osquery.io/schema`.
- Example of a join query: `select p.pid, p.name, p.path, u.username from processes p JOIN users u on u.uid=p.uid LIMIT 10;`
- Count, ` select count(*) from programs;`
