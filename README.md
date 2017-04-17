# Timeout for several pages in oTree
The pages that have to have a common timer have to be based not a 'normal'
Page class, but on GTOPage (which is imported from `gto_timeout_page.py`)
*GTO abbreviation is just abbreviation of  **G**eneral **T**ime**O**ut* :)

If you use this page and would like to have an overall timeout for several pages
in `models.py` you can set a common timeout for a set of pages:
```python
class Constants(BaseConstants):
    ...
    gto_seconds = 100
```
By default the commont timeout will apply only to the
 set of GTOPages in one round only and it will restart at the next round.
 If you need to have your common timeout for all rounds, set `overallrounds`
 variable in `models.py: Constants` to true:
 ```python
 class Constants(BaseConstants):
     ...
     gto_seconds = 100
     overallrounds = True
 ```

If you forget to set these variables, then by default the general timeout will
be 600 seconds and by default it will valid for one round only.

in `views.py` you should first import `GTOPage`:
``` python
from .gto_timeout_page import GTOPage
```
and then you define those of your pages that you need to include into one common timeout based on `GTOPage`. For example:
```python
class Intro(Page):
    timeout_seconds = 100


class Demographics(GTOPage):
    general_timeout = True
    ...

class BigFive(GTOPage):
    general_timeout = True
    ...
```
So in this example, `Intro` page will be just a normal page, with its own timeout of 100 seconds. Pages `Demographics` and `BigFive` are under the common timeout (if you'd like to exclude temporarily the page from common timeout, set its `general_timeout = False`).


since the code for general timeout uses standard oTree functions, it overrides `is_displayed`, `before_next_page`, and `vars_for_template`. If you need to use them for your individual pages under the common timeout, please use instead the following functions:

``` python
def gto_is_displayed(self):
    ...

def gto_before_next_page(self):
    ...

def gto_vars_for_template(self):
    ...
```
