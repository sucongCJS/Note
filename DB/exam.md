## Insertion anomaly

## Modification anomaly
- inconsistancies
- example:
  - don't konw which one is correct

## Database types/implementation model:
- Relational
- Heirachical
- Network
- No SQl databases

## relational integrity constraints
- entity integrity:
> a constrain on the PK.
> It requires that PK is unique, not null and minimal

- referential integrity
> relates to the integrity of relationship and hence to the integrity of FK.
> It means that the FK in one relation must reference a PK in another relation.

- domain integrity
> concerned with the allowable values of attributes.
> Attributes values are taken from a domain or pool of allowable values

## data modelling approaches
- __top down__ approach - ER diagram
- __bottom up__ approach - normalization

# view
## why use views?
- to restrict db access - some users may use data available in the view raher than the correspondin base table
- great simplification
- to make complex queries easy
- to allow data independence
- to present different views of the same data

## can views be updated?
- not all views can be updated, only simple views canbe updated.
- simple views are the views using __single tables__ and containing __no functions__(AVG, SUM etc.) or __groups__ (GROUP BY)

# transaction
## what is a transaction?
> any action that reads from and/or write to db is a _transaction_

- a transaction is a sequence of db operations that performed as a single logical unit of work
- a successful transaction changes the db from one consistent state to another
- a transaction must be either **entirely** completed or aborted

## a transaction will end due to one of the below
- A COMMIT statement is reached – will permanently record the changes
- A ROLLBACK statement is reached – will abort all the changes and the database is rolled back to its previous state.
- If end of the program is successfully reached - this is equivalent to COMMIT.
- The program is terminated incomplete (eg. Power loss) will abort all the changes and the database is rolled back to its previous - this is equivalent to ROLLBACK.

### subquery involves a table listed in outer query
