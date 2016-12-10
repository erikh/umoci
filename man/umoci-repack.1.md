% umoci-repack(1) # umoci repack - Repacks an OCI runtime bundle into an image tag
% Aleksa Sarai
% DECEMBER 2016
# NAME
umoci repack - Repacks an OCI runtime bundle into an image tag

# SYNOPSIS
**umoci repack**
**--image**=*image*[:*tag*]
[**--history.comment**=*comment*]
[**--history.created_by**=*created_by*]
[**--history.author**=*author*]
[**--history-created**=*date*]
*<bundle>*

# DESCRIPTION
Given a modified bundle extracted with **umoci-unpack**(1), **umoci-repack**(1)
computes the filesystem delta for the OCI bundle's *rootfs*. The delta is used
to generate a delta layer, which is then appended to the original image
manifest (that was used as an argument to **umoci-unpack**(1)) and tagged as a
new image tag. Between a call to **umoci-unpack**(1) and **umoci-repack**(1)
users SHOULD NOT modify the OCI image in any way.

All **--uid-map** and **--gid-map** settings are implied from the saved values
specified in **umoci-unpack**(1), so they are not available for
**umoci-repack**(1).

# OPTIONS
The global options are defined in **umoci**(1).

**--image**=*image*[:*tag*]
  The destination tag for the repacked OCI image. *image* must be a path to a
  valid OCI image (and the same *image* used in **umoci-unpack**(1) to create
  the *bundle*) and *tag* must be a valid tag name. If another tag already has
  the same name as *tag* it will be overwritten.

**--history.comment**=*comment*
  Comment for the history entry corresponding to this modification of the image
  If unspecified, **umoci**(1) will generate an implementation-dependent value.

**--history.created_by**=*created_by*
  CreatedBy entry for the history entry corresponding to this modification of
  the image. If unspecified, **umoci**(1) will generate an
  implementation-dependent value.

**--history.author**=*author*
  Author value for the history entry corresponding to this modification of the
  image. If unspecified, this value will be the image's author value **after**
  any modifications were made by this call of **umoci-config**(1).

**--history-created**=*date*
  Creation date for the history entry corresponding to this modifications of
  the image. This must be an ISO8601 formatted timestamp (see **date**(1)). If
  unspecified, the current time is used.

# SEE ALSO
**umoci**(1), **umoci-unpack**(1)