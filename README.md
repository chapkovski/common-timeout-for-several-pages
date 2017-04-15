# Timeout for several pages in oTree
The pages that have to have a common timer have to be based not a 'normal'
Page class, but on GTOPage (which is imported from `gto_timeout_page.py`)
GTO abbreviation is just from General TimeOut :)

If you use this page and would like to have an overall timeout for several pages
in `models.py`, in `Constants` you have to set:
`gto_seconds`. If you forget to set it, then by default the general timeout will be 600 seconds.

By default general timeout is for one round. If a player starts next next round
the overall time for a set of GTO pages start over again.
If you need to have a general timeout for all pages in all rounds, then  insert in
Constants:
`GTO_in_round = False`

since the code for general timeout uses standard oTree functions, it overrides `is_displayed`, `before_next_page`, and `vars_for_template`. If you need to use them for your individual pages under the common timeout, please use instead the following functions:

``` python
def gto_is_displayed(self):
    ...

def gto_before_next_page(self):
    ...

def gto_vars_for_template(self):
    ...
```
