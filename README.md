classDiagram
  class DataAcquisition {
    +__init__()
    +_get_file_list()
    +load_all_data()
    +load_file_data()
  }

  class TimeDomain {
    +__init__()
    +extract_features_streaming()
    +extract_features()
    +get_chunks()
    +check1()
    +get_rms()
    +get_mean()
    +get_variance()
    +get_crestfactor()
    +get_kurtosis()
    +get_skewness()
    +get_peak_to_peak()
    +get_shape_factor()
    +get_impulse_factor()
  }

  class FrequencyDomainFeatures {
    +__init__()
    +calculate_bearing_frequencies()
    +freq2index()
    +get_fft()
    +get_power_spectral_density()
    +get_total_power()
    +get_mean_frequency()
    +get_peak_frequency()
    +get_frequency_entropy()
    +get_dominant_frequency()
    +extract_general_features()
    +extract_bearing_features()
  }

  class Nonstationary {
    +__init__()
  }

  class DataPreprocessing {
    +__init__()
    +preprocess()
    +lowpass_filter()
    +apply_savgol_filter()
    +normalize_data()
    +high_pass_filter()
    +band_pass_filter()
    +ar_filter()
    +handle_outliers()
  }

  class SignalProcessor {
    +__init__()
    +dephase()
    +apply_med()
    +angular_resample()
    +calculate_envelope()
    +convert_to_order_domain()
    +synchronous_average()
    +calculate_difference_signal()
    +spectral_kurtosis()
    +envelope_analysis()
  }
