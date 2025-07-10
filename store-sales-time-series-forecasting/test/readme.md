Both train and test

```bash

import pandas as pd
import requests
from io import StringIO

# --- Download and merge train parts ---
base_train_url = 'https://raw.githubusercontent.com/anurag0302/test_files/main/store-sales-time-series-forecasting/train'
train_parts = []

for i in range(16):  # part_0.csv to part_15.csv
    url = f'{base_train_url}/part_{i}.csv'
    response = requests.get(url)
    if response.ok:
        train_parts.append(pd.read_csv(StringIO(response.text)))

df_train = pd.concat(train_parts, ignore_index=True)

# --- Load test.csv and clean ---
test_url = 'https://raw.githubusercontent.com/anurag0302/test_files/main/store-sales-time-series-forecasting/test/test.csv'
df_test = pd.read_csv(test_url)

df_test = df_test.dropna(how='all')  # ✅ Remove any blank rows

# --- Final combined DataFrame ---
df = pd.concat([df_train, df_test], ignore_index=True)
print(f'✅ Combined DataFrame shape: {df.shape}')  # Should now be (3029399, 6)

```
