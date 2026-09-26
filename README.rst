keel-nodejs-nginx
=================

Stack layer for Keel appliances: nginx, Node.js and Redis from the Debian
archive, on top of ``core``. Compatible with TurnKey Linux appliances, and
tracking ``turnkeylinux-apps/nodejs`` and the ``nginx.mk`` of ``common`` for
the parts it reuses.

It is a layer, not an appliance: nothing here answers on a port by itself.
NodeBB and any other appliance that needs a Node.js runtime behind nginx is
built on it, so the runtime is fetched, configured and measured once::

    bt-layer nodejs-nginx --parent core
    bt-layer nodebb --parent nodejs-nginx

Contents
--------

======================  ====================================================
``Makefile``            the common includes: ``turnkey/nginx.mk``, ``turnkey.mk``
``plan/main``           the packages this layer adds over core
``changelog``           the version ``bt-layer`` records in the manifest
======================  ====================================================

Why it is a repository
----------------------

``bt-layer`` derives ``SOURCE_DATE_EPOCH`` from the recipe's git history when
the environment does not name one, so a recipe that is only a directory on the
build host cannot be built reproducibly and cannot be rebuilt by anyone else.
This layer existed as such a directory until 2026-09-26, when a release failed
on it with ``no usable SOURCE_DATE_EPOCH``.
