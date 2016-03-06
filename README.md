# winunionfs
Automatically exported from code.google.com/p/winunionfs
UnionFS like user mode file system for Windows

The goal of this project is to allow a windows user to see in a single directory hierarchy files from multiple directory hierarchies. Furthermore, when a user changes or creates a file in this directory hierarchy, the changes are not necessarily recorded in the same directory hierarchy, as the original file or containing directory. In the current implementation, this poject uses the Dokan Library to merge a readonly directory hierarchy with a read/write directory hierarchy. The result of the merger is viewed as a new Drive letter. If a file path on the new drive letter corresponds to existing files on both directory hierarchies the file in the writable hierarchy will be seen in the merger. If a file is deleted in the merged filesystem it will be deleted from the underlying writable hierarchy if it existed and even if it existed in the readonly hierarchy, it will be not shown until the merge fs is not remounted.

