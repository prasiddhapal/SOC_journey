# 04 - File Activity Timeline

| Time | Event | Observation |
|---|---|---|
| 21:19:40 | 5145 | `nathan brooks notes.txt` accessed on `\\Marketing` |
| 21:19:41 | 5145 | Synchronization activity |
| 21:19:53 | 5145 | `Zone.Identifier` attributes accessed |
| 21:19:54 | 5145 | Synchronization activity |
| 21:19:56 | 5145 | Read-control activity |
| 21:20:14 | 5145 | **WriteData (or AddFile)** |
| 21:20:14 | 5145 | Read-control activity |
| 21:20:15 | 5145 | Synchronization activity |
| 21:21:00+ | 5145 | Later activity included deletion in the observed file-specific search |

## Important Limitation
The timeline demonstrates SMB activity around the target file. It does not provide a direct process ID for the write operation.
