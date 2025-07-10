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
