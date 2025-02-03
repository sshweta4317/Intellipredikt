# data_acquisition API Documentation

## Import

```python
from IntelliMaint.data_acquisition import DataAcquisition
```

## Overview
The `DataAcquisition class` is part of the IntelliMaint module and provides a set of methods to facilitate the loading and processing of data files. It allows users to specify directory paths, file patterns, delimiters, and other configurations for handling and combining data from multiple files.

## Initialization

### `__init__(self, config)`
#### Description:
Initializes the `DataAcquisition` class with a configuration dictionary containing file loading parameters. Internally, it calls the `_get_file_list()` method to populate self.files with a list of files that match the given pattern.

#### Parameters:
- `config` (dict): A dictionary containing configurations for data acquisition:
  - `DATA_DIR_PATH` (str): Path to the directory containing data files.
  - `file_pattern` (str): Pattern to match filenames (e.g., "*.csv", ".txt", "200*").
  - `delimiter` (str): Delimiter used in the files (e.g., "," or "\t").
  - `header` (int or None): Row number to use as column names, or `None` if no header.
  - `skiprows` (int): Number of rows to skip at the beginning of each file.

#### Returns:
None

#### Example:
```python
config = {
    "DATA_DIR_PATH": "./data",
    "file_pattern": "*.csv",
    "delimiter": ",",
    "header": 0,
    "skiprows": 1
}
data_loader = DataAcquisition(config)
```

---

## Method: `_get_file_list(self)`

#### Description:
Retrieves a list of files from the specified directory that match the given pattern.

#### Parameters:
None

#### Returns:
- `list`: A sorted list of file paths that match the specified file pattern in the configured directory.

#### Raises:
- `FileNotFoundError`: If no files matching the pattern are found.

#### Example:
```python
files = data_loader._get_file_list()
print(files)
```

---

## Method: `load_all_data(self)`
#### Description:
Loads all files matching the given pattern in the specified directory and combines their contents into a single DataFrame.
Each file is read using the parameters specified in the configuration dictionary (delimiter, header, skiprows).

#### Parameters:
None

#### Returns:
- `pd.DataFrame`: A DataFrame containing combined data from all files.

#### Example:
```python
df = data_loader.load_all_data()
print(df.head())
```

---

## Method: `load_file_data(self, file_path)`
#### Description:
Loads data from a single file located at file_path.
Reads the file using the configuration parameters such as delimiter, header, and skiprows.

#### Parameters:
- `file_path` (str): Path to the file to be loaded.

#### Returns:
- `pd.DataFrame`: A Pandas DataFrame containing the data from the specified file.

#### Example:
```python
# Load a specific file's data
file_path = "./data/sample.csv"
df = data_loader.load_file_data(file_path)

# Print the data from the specific file
print(df.head())
```

---

## Notes
- The class assumes all files have a consistent structure and delimiter.
- The `_get_file_list` method is called automatically during initialization.
- The `load_all_data` method concatenates all files into a single DataFrame, which can be useful for batch processing.

## Example Usage:

```python

from IntelliMaint.data_acquisition import DataAcquisition

def main():
    # Configuration for data acquisition
    config = {
        "DATA_DIR_PATH": r'C:\Users\DELL\Tool_wear_data/',
        "file_pattern": "*.csv",
        "delimiter": ",",
        "header": None,
        "skiprows": 1,
    }
    
    # Initialize DataAcquisition with config
    data_acquisition = DataAcquisition(config)
    
    # Iterate through files
    for file_path in data_acquisition.files:
        print(f"Processing file: {file_path}")
        df = data_acquisition.load_file_data(file_path)
    
        # Process each column in the file
        for Col in range(df.shape[1] - 1):  # Exclude last column if it's non-signal data
            signal = pd.to_numeric(df.iloc[:, Col], errors="coerce").dropna().values
            signal = np.array(signal, dtype=float)  # Ensure it's a numpy array

            print(signal)
            print(len(signal))

if __name__ == "__main__":
    main()
```

