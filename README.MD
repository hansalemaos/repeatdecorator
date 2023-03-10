# A decorator to call a function every n seconds


### pip install repeatdecorator

```python

import time
from random import choice, uniform

from repeatdecorator import repeat_func, repeatdec_vars


@repeat_func(
    repeat_time=0.1,
    variablename="represults",
    activate_lock=True,
    ignore_exceptions=True,
    exception_value="EXCEPTION",
    max_len_allresults=None,
    print_results=False,
    print_exceptions=True,
    execution_limit=20,
    max_concurrent_threads=10,
    check_max_threads_every_n_seconds=0.015,
)
def ha():
    vall = choice([0, 1, 2])
    time.sleep(uniform(.2, 1))
    print(f'Running threads: {repeatdec_vars.active()} ')


    return 5 / vall


print(f'START: Running threads: {repeatdec_vars.active()} ')
ha()
while not hasattr(repeatdec_vars, "represults"):
    continue

for r in range(15):
    print(f"{repeatdec_vars.represults=}")
    time.sleep(0.5)
    if r == 5:
        repeatdec_vars.represults["enabled"] = False
        break


#OUTPUT: 
START: Running threads: 4 
Running threads: 10 
division by zero
repeatdec_vars.represults={'results': ['EXCEPTION'], 'enabled': True, 'total_count': 6}
repeatdec_vars.represults={'results': ['EXCEPTION'], 'enabled': True, 'total_count': 6}
Running threads: 10 
repeatdec_vars.represults={'results': ['EXCEPTION', 5.0], 'enabled': True, 'total_count': 7}
Running threads: 10 
repeatdec_vars.represults={'results': ['EXCEPTION', 5.0, 5.0], 'enabled': True, 'total_count': 8}
Running threads: 10 
division by zero
repeatdec_vars.represults={'results': ['EXCEPTION', 5.0, 5.0, 'EXCEPTION'], 'enabled': True, 'total_count': 9}
Running threads: 10 
repeatdec_vars.represults={'results': ['EXCEPTION', 5.0, 5.0, 'EXCEPTION', 2.5], 'enabled': True, 'total_count': 10}
Running threads: 10 
division by zero
Running threads: 9 
Running threads: 8 
Running threads: 7 
division by zero
Running threads: 6 
Running threads: 5 



#Summary of repeat_func

    Args:
        f_py (Any)
            Description Don't use - reserved for the function
            Default     None
        repeat_time (Union[float,int])
            Description Execute each n seconds
            Default     1.0
        variablename (str)
            Description Creates a dict for the results in repeatdec_vars - Use repeatdecorator.repeatdec_vars.variablename to access it
            Default     "threadresults"
        activate_lock (bool)
            Description Threading Rlock
            Default     False
        ignore_exceptions (bool)
            Description Continue on Exceptions?
            Default     False
        exception_value (Any)
            Description Ignored if  ignore_exceptions is False
            Default     None
        max_len_allresults (Union[int,None])
            Description If None, results are stored in a list (no limit), if int, a deque is used to store
                        the results. Results can be found here: repeatdecorator.repeatdec_vars.variablename["results"]
                        Make sure to save the results before calling the function again.
            Default     None
        print_results (bool)
            Description Print the return value from each function?
            Default     True
        print_exceptions (bool)
            Description Print Exceptions
            Default     True
        execution_limit (int)
            Description Stop timer after n executions / -1 = No limit
            Default     -1
        max_concurrent_threads (int)
            Description Thread limit  / -1 = No limit
            Default     -1
        check_max_threads_every_n_seconds (Union[float,int])
            Description Sleep time before checking the current number of threads again.
            Default     0.015

    Returns:
        Any: Description of return value


```

