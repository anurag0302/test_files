store-sales-time-series-forecasting
for spliting
```bash
import pandas as pd
import os

# Load your large CSV
csv_file = 'train.csv'
chunk_size = 200000  # Change based on size; e.g., 200K rows per file

# Create output folder
output_folder = 'csv_parts'
os.makedirs(output_folder, exist_ok=True)

# Read and split
i = 0
for chunk in pd.read_csv(csv_file, chunksize=chunk_size):
    out_path = os.path.join(output_folder, f'part_{i}.csv')
    chunk.to_csv(out_path, index=False)
    print(f"Saved {out_path}")
    i += 1

print(f"Split complete! Created {i} files.")

import shutil

# Zip the folder into 'csv_parts.zip'
shutil.make_archive('csv_parts', 'zip', 'csv_parts')
files.download('csv_parts.zip')


```

For merging
```bash
import pandas as pd
import requests
from io import StringIO

# GitHub raw file base URL
base_url = 'https://raw.githubusercontent.com/anurag0302/test_files/main/store-sales-time-series-forecasting/train'

# Number of parts
num_files = 15  # Change if more or fewer files

# Download and merge all CSV parts
all_parts = []
for i in range(num_files):
    file_name = f'part_{i}.csv'
    file_url = f'{base_url}/{file_name}'
    print(f'Downloading: {file_url}')
    
    response = requests.get(file_url)
    if response.status_code == 200:
        df = pd.read_csv(StringIO(response.text))
        all_parts.append(df)
    else:
        print(f'⚠️ Failed to download {file_name} (status: {response.status_code})')

# Concatenate into one DataFrame
df = pd.concat(all_parts, ignore_index=True)

print('✅ All parts downloaded and merged into DataFrame `df`')
print(df.head())
```



