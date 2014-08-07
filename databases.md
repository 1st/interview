Interview Questions. Databases
=========


This chapter will help you to get answers on typical interview questions for **developers who use databases** in work.


Questions list
---------

#### What difference between `MyISAM` and `InnoDB`?

`InnoDB` supports transations, foreign keys.


#### How to use `compotite key`?

`Composite key` is used if we need to create index based on two or more columns. If we need to search by first column from composite key - we don't need to create additional index. But for all other columns that follow after this first column - we need to create additonal indexes.
