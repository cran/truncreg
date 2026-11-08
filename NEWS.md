# truncreg 0.3-0

* Code repository changed from R-Forge to Codeberg at:
  <https://codeberg.org/zeileis/truncreg/>

* Added basic altdoc page with overview and documentation at:
  <https://zeileis.codeberg.page/truncreg/>

* Add support for [distributions3](https://zeileis.github.io/distributions3/)
  (and hence also [topmodels](https://zeileis.codeberg.page/topmodels/)).


# truncreg 0.2-5

* Removed link to `mhurdle` as `mhurdle` was archived on CRAN.


# truncreg 0.2-4

* `NAMESPACE` improvements.


# truncreg 0.2-3

* The Mills ratio is computed in logs for numerical stability.


# truncreg 0.2-2

* A `scaled` version is added.


# truncreg 0.2-1

* E-mail of the maintainer changed.


# truncreg 0.2-0

* Added/improved support for standard extractor methods:
  `logLik()`, `model.matrix()`, `model.frame()`, `terms()`, `predict()`.

* Extended information provided in `truncreg` objects to
  support methods above, e.g., the terms and number of
  observations are now conveniently accessible, model/y/x
  are optionally available. 

* Added internal check that the response is actually truncated
  and an error is thrown if not.
