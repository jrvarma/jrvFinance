# jrvFinance 1.4.2

Dependency fixed. Suggests `markdown` and `rmarkdown` as required by <https://github.com/yihui/knitr/issues/1864>

# jrvFinance 1.4.1

Bug fix release. The `edate` function was giving wrong answers under certain conditions when called with vector inputs. The incorrect `if` statement has now been changed to the correct `ifelse`. Thanks to Thethach Chuaprapaisilp for finding the bug.

# jrvFinance 1.4.0

* All the bond functions now accept an additional parameter `redemption_value` to handle the situation where the bond is expected to be called at premium to par. This is based on code provided by Tom McGinty. (#1)
