# DataAcquisition Class Documentation

## Overview
The `DataAcquisition` class is designed to handle loading and processing data files from a specified directory. It supports reading multiple files matching a given pattern, combining them into a single DataFrame, and loading individual files.

## Initialization

### `__init__(self, config)`
#### Description:
Initializes the `DataAcquisition` class with a configuration dictionary containing file loading parameters.

#### Parameters:
- `config` (dict): A dictionary containing configurations for data acquisition:
  - `DATA_DIR_PATH` (str): Path to the directory containing data files.
  - `file_pattern` (str): Pattern to match filenames (e.g., "*.csv").
  - `delimiter` (str): Delimiter used in the files (e.g., "," or "\t").
  - `header` (int or None): Row number to use as column names, or `None` if no header.
  - `skiprows` (int): Number of rows to skip at the beginning of each file.

#### Returns:
None

#### Example Usage:
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
- `list`: A sorted list of file paths that match the pattern.

#### Raises:
- `FileNotFoundError`: If no files matching the pattern are found.

#### Example Usage:
```python
files = data_loader._get_file_list()
print(files)
```

---

## Method: `load_all_data(self)`
#### Description:
Loads and combines data from all matching files in the directory into a single DataFrame.

#### Parameters:
None

#### Returns:
- `pd.DataFrame`: A DataFrame containing combined data from all files.

#### Example Usage:
```python
df = data_loader.load_all_data()
print(df.head())
```

---

## Method: `load_file_data(self, file_path)`
#### Description:
Loads data from a specified file into a DataFrame.

#### Parameters:
- `file_path` (str): Path to the file to be loaded.

#### Returns:
- `pd.DataFrame`: A DataFrame containing the file's data.

#### Example Usage:
```python
file_path = "./data/sample.csv"
df = data_loader.load_file_data(file_path)
print(df.head())
```

---

## Notes
- The class assumes all files have a consistent structure and delimiter.
- The `_get_file_list` method is called automatically during initialization.
- The `load_all_data` method concatenates all files into a single DataFrame, which can be useful for batch processing.

## Dependencies
- `glob`
- `pandas`
- `numpy`


