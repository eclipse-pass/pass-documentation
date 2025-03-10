# Funder

Funder / sponsor of a [Grant](Grant.md).

| Field    | Type   | Description                                                                                                                                                                                                                                              |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id*      | String | Autogenerated identifier of object                                                                                                                                                                                                                       |
| name*    | String | Funder name                                                                                                                                                                                                                                              |  
| url      | String | Funder URL                                                                                                                                                                                                                                               |
| localKey | String | Local key assigned to the funder within the researcher's institution to support matching between PASS and a local system. The value is in the form of : `domain:type:value`. For a funder at JHU, an example would be`"johnshopkins.edu:funder:8675309"` |

| Relationship   | Type   | Target    | Description |
| -------------- | ------ | --------- | ----------- | 
| policy         | To One | [Policy](Policy.md) | Policy associated with the Funder  |
 
*required 
