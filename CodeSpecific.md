# DataAcquisition API Documentation

## Overview

The `DataAcquisition` class provides a set of methods to handle and process data files in a specified directory. It supports loading multiple data files, processing their contents, and offering flexibility for customization through a configuration dictionary.

## Class: `DataAcquisition`

### Constructor: `__init__(self, config)`

#### Parameters:
- `config` (dict): A configuration dictionary that contains the following keys:
  - `DATA_DIR_PATH` (str): Path to the directory containing the data files.
  - `file_pattern` (str): Pattern to match filenames (e.g., `"*.csv"`).
  - `delimiter` (str): Delimiter used in the files (e.g., `","` for CSV).
  - `header` (int or None): Row number to use as the column names, or `None` if no header is present.
  - `skiprows` (int): Number of rows to skip at the start of each file.

#### Description:
- Initializes the `DataAcquisition` object with a given configuration dictionary.
- Calls `_get_file_list()` internally to populate `self.files` with a list of files matching the `file_pattern` in the specified `DATA_DIR_PATH`.

---

### Method: `_get_file_list(self)`

#### Returns:
- `list`: A sorted list of file paths matching the given pattern in the directory.

#### Description:
- Searches the directory specified in `DATA_DIR_PATH` for files matching the `file_pattern`.
- Returns a list of file paths or raises a `FileNotFoundError` if no files match the pattern.

---

### Method: `load_all_data(self)`

#### Returns:
- `pd.DataFrame`: A Pandas DataFrame containing the combined data from all matching files.

#### Description:
- Loads all files in the directory and combines their contents into a single DataFrame.
- Each file is read using the configurations (delimiter, header, skiprows) defined in the `config` dictionary.

---

### Method: `load_file_data(self, file_path)`

#### Parameters:
- `file_path` (str): Full path to the file to be loaded.

#### Returns:
- `pd.DataFrame`: A Pandas DataFrame containing the data from the specified file.

#### Description:
- Loads data from a single file located at the specified `file_path`.
- Reads the file using the configuration parameters (`delimiter`, `header`, `skiprows`) from the `config` dictionary.

---

## Example Usage

```python
# Configuration for data acquisition
config = {
    "DATA_DIR_PATH": r"C:\Users\DELL\Desktop\Madhumitha files\Tool_wear_All_data",  # Directory path
    "file_pattern": "*.csv",  # File pattern (e.g., all CSV files)
    "delimiter": ",",  # Delimiter used in files
    "header": None,  # No header row
    "skiprows": 1,  # Skip the first row of each file
}

# Initialize DataAcquisition with config
data_acquisition = DataAcquisition(config)

# Load and combine all data
all_data = data_acquisition.load_all_data()

# Print the combined DataFrame
print(all_data)

# Process individual files
for file_path in data_acquisition.files:
    print(f"Processing file: {file_path}")
    df = data_acquisition.load_file_data(file_path)
    print(df.head())  # Print first few rows of the file data
