
# DataPreprocessing API

The **`DataPreprocessing`** class provides a set of methods to preprocess time-series or signal data through filtering, smoothing, and normalization. It allows customizable preprocessing pipelines.

---

## Class: `DataPreprocessing`

### **`DataPreprocessing(filter_order, cutoff_frequency)`**

#### **Arguments**:
- **`filter_order`** (*int*):  
  Order of the Butterworth lowpass filter.  
  Determines the complexity of the filter and the sharpness of the cutoff frequency.  

- **`cutoff_frequency`** (*float*):  
  Normalized cutoff frequency of the lowpass filter (range: 0.0 to 1.0).

#### **Example**:
```python
from preprocessing import DataPreprocessing

# Initialize the class with filter order 4 and cutoff frequency 0.2
preprocessor = DataPreprocessing(filter_order=4, cutoff_frequency=0.2)
```

---

## Method: `preprocess(signal, operations=None)`

Preprocess the input signal using a series of operations (filtering, smoothing, normalization).

#### **Arguments**:
- **`signal`** (*array-like*):  
  Input data (e.g., a signal or time-series) to preprocess.

- **`operations`** (*list of str, optional*):  
  List of preprocessing operations to perform. Options:
  - `'filter'` - Apply lowpass Butterworth filter.
  - `'smooth'` - Apply Savitzky–Golay smoothing.
  - `'normalize'` - Normalize the data (z-score normalization).

  If `None`, defaults to `['filter', 'smooth', 'normalize']`.

#### **Returns**:
- **`signal`** (*array-like*):  
  The preprocessed signal.

#### **Example**:
```python
# Apply filtering, smoothing, and normalization
processed_signal = preprocessor.preprocess(raw_signal, operations=['filter', 'smooth', 'normalize'])
```

---

## Method: `butter_lowpass_filter(data)`

Applies a lowpass Butterworth filter to the input data.

#### **Arguments**:
- **`data`** (*array-like*):  
  Input signal to filter.

#### **Returns**:
- **`filtered_data`** (*array-like*):  
  Filtered signal.

#### **Example**:
```python
# Filter the signal using the Butterworth lowpass filter
filtered_signal = preprocessor.butter_lowpass_filter(raw_signal)
```

---

## Method: `apply_savgol_filter(data, window_length=201, polyorder=3)`

Applies a Savitzky–Golay filter to smooth the input signal.

#### **Arguments**:
- **`data`** (*array-like*):  
  Input signal to smooth.

- **`window_length`** (*int, optional*):  
  Length of the filter window (must be odd). Default is `201`.

- **`polyorder`** (*int, optional*):  
  Order of the polynomial used to fit the samples. Default is `3`.

#### **Returns**:
- **`smoothed_data`** (*array-like*):  
  Smoothed signal.

#### **Example**:
```python
# Smooth the signal using a Savitzky–Golay filter
smoothed_signal = preprocessor.apply_savgol_filter(raw_signal, window_length=101, polyorder=2)
```

---

## Method: `normalize_data(data)`

Normalizes the input data using z-score normalization.

#### **Arguments**:
- **`data`** (*array-like*):  
  Input signal to normalize.

#### **Returns**:
- **`normalized_data`** (*array-like*):  
  Signal normalized to have zero mean and unit variance.

#### **Example**:
```python
# Normalize the signal
normalized_signal = preprocessor.normalize_data(raw_signal)
```

---

## Usage Example:

```python
from preprocessing import DataPreprocessing

# Initialize the DataPreprocessing class
preprocessor = DataPreprocessing(filter_order=4, cutoff_frequency=0.2)

# Define a raw signal
raw_signal = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Preprocess the signal
processed_signal = preprocessor.preprocess(raw_signal)

# Apply individual operations
filtered_signal = preprocessor.butter_lowpass_filter(raw_signal)
smoothed_signal = preprocessor.apply_savgol_filter(raw_signal, window_length=5, polyorder=2)
normalized_signal = preprocessor.normalize_data(raw_signal)
```
