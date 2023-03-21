import pandas as pd
import numpy as np
import sqlite3 as sql
import shutil
import matplotlib.pyplot as plt
import matplotlib.dates as mdt
import datetime as dtm

#connection = sql.connect("C:\\Users\kuwon\Code\SavvyCoders\Homework\input\sf-bay-area-bike-share\newstatus.csv")
newstatus = pd.read_csv(r"C:\\Users\kuwon\Code\SavvyCoders\Homework\input\sf-bay-area-bike-share\newstatus.csv")
newstatus.head()

trips_df = pd.read_csv(r"C:\\Users\kuwon\Code\SavvyCoders\Homework\input\sf-bay-area-bike-share\trip.csv")
trips_df.head()

stations_df = pd.read_csv(r"C:\\Users\kuwon\Code\SavvyCoders\Homework\input\sf-bay-area-bike-share\station.csv")
stations_df.head()

import pandas as pd
import numpy as np
import sqlite3 as sql
import shutil
import matplotlib.pyplot as plt
import matplotlib.dates as mdt
import datetime as dtm
import numpy as np
def reduce_mem_usage(df):
    """ iterate through all the columns of a dataframe and modify the data type
        to reduce memory usage.        
    """
    start_mem = df.memory_usage().sum() / 1024**2
    print('Memory usage of dataframe is {:.2f} MB'.format(start_mem))
    for col in df.columns:
        col_type = df[col].dtype
        if col_type != object:
            c_min = df[col].min()
            c_max = df[col].max()
            if str(col_type)[:3] == 'int':
                if c_min > np.iinfo(np.int8).min and c_max < np.iinfo(np.int8).max:
                    df[col] = df[col].astype(np.int8)
                elif c_min > np.iinfo(np.int16).min and c_max < np.iinfo(np.int16).max:
                    df[col] = df[col].astype(np.int16)
                elif c_min > np.iinfo(np.int32).min and c_max < np.iinfo(np.int32).max:
                    df[col] = df[col].astype(np.int32)
                elif c_min > np.iinfo(np.int64).min and c_max < np.iinfo(np.int64).max:
                    df[col] = df[col].astype(np.int64)  
            else:
                if c_min > np.finfo(np.float16).min and c_max < np.finfo(np.float16).max:
                    df[col] = df[col].astype(np.float16)
                elif c_min > np.finfo(np.float32).min and c_max < np.finfo(np.float32).max:
                    df[col] = df[col].astype(np.float32)
                else:
                    df[col] = df[col].astype(np.float64)

    end_mem = df.memory_usage().sum() / 1024**2
    print('Memory usage after optimization is: {:.2f} MB'.format(end_mem))
    print('Decreased by {:.1f}%'.format(100 * (start_mem - end_mem) / start_mem))
    return df
    
--------------------------------------------------------------------    
    Memory usage of dataframe is 2196.79 MB
Memory usage after optimization is: 755.15 MB
Decreased by 65.6%
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 71984434 entries, 0 to 71984433
Data columns (total 4 columns):
 #   Column           Dtype 
---  ------           ----- 
 0   station_id       int8  
 1   bikes_available  int8  
 2   docks_available  int8  
 3   time             object
dtypes: int8(3), object(1)
memory usage: 755.1+ MB

-----------------------------------------------------------
    import pandas as pd
status_df = reduce_mem_usage(pd.read_csv(r"C:\\Users\kuwon\Code\SavvyCoders\Homework\input\sf-bay-area-bike-share\status.csv"))
status_df.info()


weather = pd.read_csv(r"C:\\Users\kuwon\Code\SavvyCoders\Homework\input\sf-bay-area-bike-share\weather.csv")
weather
weather.head()
