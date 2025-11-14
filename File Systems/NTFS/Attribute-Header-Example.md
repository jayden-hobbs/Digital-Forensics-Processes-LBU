For a resident attribute:

| Size (byte)    | Description               |                                                      |
| -------------- | ------------------------- | ---------------------------------------------------- |
| 4              | attribute type identifier |                                                      |
| 4              | length of attribute       | in bytes                                             |
| 1              | non-resident flag         | 0=attribute is resident. 1=attribute is non-resident |
| 1              | length of name            | often zero (no name)                                 |
| 2              | offset to name            | often zero (no name)                                 |
| 2              | flags                     | access rights (read write etc)                       |
| 2              | attribute identifier      | number unique in MFT                                 |
| 4              | size of content           | attribute size in bytes                              |
| 2              | offset to content         | from start of attribute                              |
| 2              | not used                  |                                                      |
| ***24 BYTES*** |                           |                                                      |

For a non-resident attribute:


| Size (bytes)   | Description                                                                                                                          |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| 16             | same as for resident attribute                                                                                                       |
| 48             | entries describing the location of the rest of the attribute - must be able to `point at` data running over several sets of clusters |
| ***64 BYTES*** |                                                                                                                                      |
