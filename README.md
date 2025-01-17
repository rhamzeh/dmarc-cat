# README.md

## Status

[![GitHub release](https://img.shields.io/github/release/keltia/dmarc-cat.svg)](https://github.com/keltia/dmarc-cat/releases/)
[![GitHub issues](https://img.shields.io/github/issues/keltia/dmarc-cat.svg)](https://github.com/keltia/dmarc-cat/issues)
[![Go Version](https://img.shields.io/badge/go-1.10-blue.svg)](https://golang.org/dl/)
[![Build Status](https://travis-ci.org/keltia/dmarc-cat.svg?branch=master)](https://travis-ci.org/keltia/dmarc-cat)
[![GoDoc](http://godoc.org/github.com/keltia/dmarc-cat?status.svg)](http://godoc.org/github.com/keltia/dmarc-cat)
[![SemVer](https://img.shields.io/badge/semver-2.0.0-blue)](https://semver.org/spec/v2.0.0.html)
[![License](https://img.shields.io/badge/License-BSD-blue)](https://opensource.org/licenses/BSD-2-Clause)
[![Go Report Card](https://goreportcard.com/badge/github.com/keltia/dmarc-cat)](https://goreportcard.com/report/github.com/keltia/dmarc-cat)

## Summary

`dmarc-cat` is a small command-line utility to analyze and display in a usable manner the content of the DMARC XML reports sent by the various email providers around the globe.

## Installation

As with many Go utilities, a simple

    go get github.com/keltia/dmarc-cat

is enough to fetch, build and install.  On some systems you may need to add some environment variables to enable the Go and C compilers to find the `gpgme` include files and libraries.

    CGO_CFLAGS="-I/usr/local/include" CGO_LDFLAGS="-L/usr/local/lib" go get ...

## Dependencies

Aside from the standard library, I use `github.com/intel/tfortools` to generate tables.

    go get -u github.com/intel/tfortools

It also use my own module `github.com/keltia/archive` to handle the various archive types.

If you use Go modules, it should all work automatically.

## Usage

SYNOPSIS
```
dmarc-cat -hvD <zipfile|xmlfile>

Example:

$ dmarc-cat /tmp/yahoo.com\!keltia.net\!1518912000\!1518998399.xml

Reporting by: Yahoo! Inc. — postmaster@dmarc.yahoo.com
From 2018-02-18 01:00:00 +0100 CET to 2018-02-19 00:59:59 +0100 CET

Domain: keltia.net
Policy: p=none; dkim=r; spf=r

Reports(1):
IP            Count   From       RFrom      RDKIM   RSPF
88.191.250.24 1       keltia.net keltia.net neutral pass
```

## Columns

The full XML grammar is available [here](https://tools.ietf.org/html/rfc7489#appendix-C)

The report has several columns:

- `IP` is matching IP address
- `Count` is the number of times this IP was present
- `From` is the `From:` header value
- `RFrom` is the envelope `From` value
- `RDKIM` is the result from DKIM checking
- `RSPF` is the result from SPF checking

## Tests

Getting close to 90% coverage.

## License

This is released under the BSD 2-Clause license.  See `LICENSE.md`.

## References

- [DMARC](https://dmarc.org/)
- [SPF](http://www.rfc-editor.org/info/rfc7208)
- [DKIM](http://www.rfc-editor.org/info/rfc6376)

## Contributing

I use Git Flow for this package so please use something similar or the usual github workflow.

1. Fork it ( https://github.com/keltia/dmarc-cat/fork )
2. Checkout the develop branch (`git checkout develop`)
3. Create your feature branch (`git checkout -b my-new-feature`)
4. Commit your changes (`git commit -am 'Add some feature'`)
5. Push to the branch (`git push origin my-new-feature`)
6. Create a new Pull Request
