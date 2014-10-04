Interview Questions. Databases
=========


This chapter will help you to get answers on typical interview questions for **developers who use databases** in work.


Questions list
---------

#### What difference between `MyISAM` and `InnoDB`?

`InnoDB` supports transations, foreign keys.


#### How to use `compotite key`?

**Composite key** is used if we need to create index based on two or more columns. If we need to search by first column from composite key - we don't need to create additional index. But for all other columns that follow after this first column - we need to create additonal indexes.

For example, we have table `users` with 3 columns: `name`, `age` and `company_name`. We have composite key for all 3 columns `KEY (name, age, company_name)`. In this case we can search user by `name` OR by `name` and `age` OR by `name`, `age` and `company_name`. But we can't search by `age` or `company_name` because index should find `name` before go forward to search by next column. To search by `age` or `company_name` we need to create additonal index.
