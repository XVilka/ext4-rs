## Status

[![Build status](https://api.travis-ci.org/FauxFaux/ext4-rs.png)](https://travis-ci.org/FauxFaux/ext4-rs)
[![](https://img.shields.io/crates/v/ext4.svg)](https://crates.io/crates/ext4)

`ext4-rs` can extract the basic `stat` information, directory listings, and file content
  from real images generated by other tools, and by the Linux kernel.

This operates directly on partitions. To read actual disc images, probably need to handle
  partition tables. This can be accomplished with the `bootsector` crate.

All basic file types are represented: files, directories, symlinks, char and block devices,
  fifos and sockets. Hard links are not a type of thing that makes sense: the item is just in
  multiple directories.


### Practical problems

 * No support for extended flags (e.g. `immutable`, `append-only`).
 * Probably contains overflows and fencepost errors, many of which Rust will translate to
     panics for you. At least, in debug mode.


### Non-goals

This is not a filesystem driver. It does not support efficiently modifying real filesystems.
  Currently, it doesn't support modifying anything at all, but that may change.

I'm not especially interested in resource-constrained platforms: memory and IO are not used
  efficiently.

## Changelog

 * `0.5.0`: update `bitflags` for associated constants, and rename some public constants.
 * `0.4.1`: fix for an infinite loop parsing directory entries


## Development


### Tests

Some of the tests read generated image files. These images are not directly checked into git,
  and will be unpacked by `build.rs`. These files are apparently very large, but should take
  very little space. This requires a decent `tar` to be on the path.

These test assets can be rebuilt (on Linux, with root) by running
  `./extract-test-data --refresh`.


### License note

The code is licensed under the super-permissive MIT license.

However, a number of struct and bitfield definitions, and some maths expressions,
  are lifted directly from the Linux, or e2fsprogs, source code. These code-bases are
  under the GPLv2. I believe this to be fair use: these places *are* the documentation,
  and only interface definitions have been extracted, no code. I leave the final decision
  to you.


## Thanks

This would have been practically impossible without the work a `Djwong` has done on
  the [ext4 disk layout](https://ext4.wiki.kernel.org/index.php/Ext4_Disk_Layout) page on
  the kernel wiki. I believe this person is [Darrick Wong](https://djwong.org/). Thanks, man.
