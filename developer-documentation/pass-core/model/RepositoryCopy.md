# Repository Copy

A Repository Copy represents a copy of a [Publication](Publication.md) that exists in a target [Repository](Repository.md). The Repository Copy either (1) was the result of an accepted [Deposit](Deposit.md) from PASS, in which case there would be a link to the Copy from the related Deposit record, or (2) was created outside of PASS by some other process. In the second case, PASS stores information to help determine whether a Publication is already compliant with the repository's requirements.

| Field       | Type     | Description                                                                                         |
|-------------|----------|-----------------------------------------------------------------------------------------------------|
| id*         | String   | Autogenerated identifier of object                                                                  |
| externalIds | String[] | IDs assigned to this entity by the target repository                                                |
| copyStatus* | String   | Status of the copy in the external repository's workflow ([_see list below_](#copy-status-options)) |
| accessUrl   | String   | URL to access the item in the repository, could allow Users to see the final result                 |

| Relationship | Type   | Target  	                     | Description                        |
|--------------|--------|-------------------------------|------------------------------------|
| publication* | To One | [Publication](Publication.md) | Publication that this is a copy of |
| repository*  | To One | [Repository](Repository.md)   | Repository being deposited to      |
 
*required 

## Copy status options

These are the possible statuses for a Deposit in the order they could occur. Note that not all repositories will go through every status.

| Value       | Description                                                                                                                                                                                                                                                                                                                                  |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accepted    | The target [Repository](Repository.md) has indicated that the Deposit has been accepted                                                                                                                                                                                                                                                      |
| in-progress | The target [Repository](Repository.md) is processing the Deposit                                                                                                                                                                                                                                                                             |
| stalled     | The target [Repository](Repository.md) has detected a problem that has caused the progress to stall. This will likely require some direct interaction with the repository to re-initiate the process. Examples include when there are incorrect files or when a user did not respond to a validation request in a reasonable amount of time. |
| complete    | The target [Repository](Repository.md) has accepted the Deposit, and publication is pending if not already complete                                                                                                                                                                                                                          |
| rejected    | The target [Repository](Repository.md) has rejected the Deposit.                                                                                                                                                                                                                                                                             |
