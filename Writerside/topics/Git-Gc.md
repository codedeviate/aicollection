# gc

The `git gc` command is used to clean up and optimize a Git repository. It stands for "garbage collection" and performs various maintenance tasks to reduce the disk space used by the repository and improve its performance.

## Detailed Explanation

1. **Garbage Collection**: `git gc` removes unreachable objects from the repository. These objects are usually created during operations like rebasing, merging, or resetting and are no longer needed.

2. **Packing Objects**: It packs loose objects into a single pack file, which reduces the number of files in the `.git/objects` directory and improves performance.

3. **Pruning**: It prunes loose objects that are older than a certain age (default is 2 weeks). This helps in cleaning up the repository by removing unnecessary data.

4. **Repacking**: It repacks the repository to optimize the storage of objects. This can include delta compression, which reduces the size of the repository by storing differences between objects.

## Examples

1. **Running Garbage Collection**:
   ```sh
   git gc
   ```
   This command runs the default garbage collection, which includes packing loose objects, pruning unreachable objects, and optimizing the repository.

2. **Aggressive Garbage Collection**:
   ```sh
   git gc --aggressive
   ```
   This command runs a more thorough garbage collection, which can take longer but results in better optimization. It performs more extensive delta compression and repacking.

3. **Pruning Unreachable Objects**:
   ```sh
   git gc --prune=now
   ```
   This command prunes all unreachable objects immediately, instead of waiting for the default 2-week grace period. This can be useful if you need to free up disk space quickly.

These commands help maintain the health and performance of your Git repository by cleaning up unnecessary data and optimizing storage.