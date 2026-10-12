# OmniKernel: Virtual File System (VFS) Specification v1.0

The OmniKernel VFS provides a unified interface for accessing diverse storage backends.

## 1. The Capability-Based Namespace
Files and directories are not referenced by paths but by **File Capabilities**. A process must possess a valid capability token to open or modify a file.

## 2. The Inode Structure
OmniKernel uses a synthetic Inode structure:
- `InodeID`: Unique 64-bit identifier.
- `CapabilityMask`: Defines permissions.
- `StoragePointer`: Pointer to the actual data block.

## 3. Symbolic Link Resolution
Symbolic links are resolved recursively by the VFS. To prevent infinite loops, a maximum depth of 16 links is enforced.
