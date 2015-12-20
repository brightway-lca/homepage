Color scheme: 
http://paletton.com/#uid=70i0u0kdLfc8IpEc3kGjucRoo9N

Get pygments formatting:
code = """In [1]: from brightway2 import *

In [2]: from scipy.stats import kendalltau

In [3]: import numpy as np

In [4]: db = Database("ecoinvent 3.2 cutoff")

In [5]: gwp, usetox = ('IPCC 2013', 'climate change', 'GWP 100a'), ('USEtox', 'human toxicity', 'total')

In [6]: lca = LCA({db.random(): 1}, method=gwp); lca.lci(factorize=True); lca.lcia()

In [7]: def calculate_correlation(n=1000):
   ....:         results = np.zeros((2, n))
   ....:         for x, method in enumerate((gwp, usetox)):
   ....:                 lca.switch_method(method)
   ....:                 for y, activity in enumerate(db):
   ....:                         if y == n:
   ....:                                 break
   ....:                         lca.redo_lcia({activity: 1})
   ....:                         results[x, y] = lca.score
   ....:         return kendalltau(*results)

In [8]: kendalltau(*calculate_correlation())
Out[8]: KendalltauResult(correlation=-0.004769486612148318, pvalue=0.82132482572697252)"""

from pygments import highlight
from pygments.lexers import PythonLexer
from pygments.formatters import HtmlFormatter

print(highlight(code, PythonLexer(), HtmlFormatter()))
