This section describes the python APIs of `PPLNN`. Refer to [pplnn.py](../../tools/pplnn.py) for usage examples and [py_pplnn.cc](../../python/py_pplnn.cc) for exported symbols.

## Common APIs in `pyppl.nn`

### TensorShape

```python
dims = TensorShape::GetDims()
```

Returns a tuple of array dimensions.

```python
data_type = TensorShape::GetDataType()
```

Returns the data type of elements in tensor. Data types are defined in `pyppl.common`.

```python
data_format = TensorShape::GetDataFormat()
```

Returns the data format of tensor. Data formats are defined in `pyppl.common`.

```python
is_scalar = TensorShape::IsScalar()
```

Tells whether a tensor is a scalar.

### Tensor

```python
name_str = Tensor::GetName()
```

Returns the tensor's name.

```python
tensor_shape = Tensor::GetShape()
```

Returns a `TensorShape` info of the tensor.

```python
ret_code = Tensor::ConvertFromHost(numpy_ndarray)
```

Copies NDARRAY data to the tensor from an `ndarray` object. `ret_code` is an instance of `RetCode` defined in `pyppl.common`.

```python
tensor_data = Tensor::ConvertToHost()
```

Copies tensor's data to host in NDARRAY format. We can use `numpy.array` to create an `ndarray` instance using `numpy_ndarray = numpy.array(tensor_data, copy=False)`.

### Engine

```python
name_str = Engine::GetName()
```

Returns engine's name.

### RuntimeOptions

Refer to [runtime_options.h](../../include/ppl/nn/runtime/runtime_options.h) for more details.

### OnnxRuntimeBuilderFactory

```python
runtime_builder = OnnxRuntimeBuilderFactory::CreateFromFile(onnx_model_file, engines)
```

Creates an `OnnxRuntimeBuilder` instance from an ONNX model. `engines` is a list of `Engine` instances that may be used to evaluate the model.

### OnnxRuntimeBuilder

```python
runtime_options = RuntimeOptions()
runtime = OnnxRuntimeBuilder::CreateRuntime(runtime_options)
```

Creates a `Runtime` instance for inferencing.

### Runtime

```python
input_count = Runtime::GetInputCount()
```

Returns the number of model inputs.

```python
input_tensor = Runtime::GetInputTensor(idx)
```

Returns the input tensor in position `idx`, which is in range [0, input_count).

```python
ret_code = Runtime::Run()
```

Evaluates the model. `ret_code` is an instance of `RetCode` defined in `pyppl.common`.

```python
ret_code = Runtime::Sync()
```

Waits for all operations to finish.

```python
output_count = Runtime::GetOutputCount()
```

Returns the number of model outputs.

```python
output_tensor = Runtime::GetOutputTensor(idx)
```

Returns the output tensor in position `idx`, which is in range [0, output_count).

## Device Specific APIs in `pyppl.nn`

### X86

#### X86EngineFactory

```python
x86_engine = X86EngineFactory::Create()
```

Creates an `Engine` instance running on x86-64 compatiable CPUs.

```python
ret_code = x86_engine.Configure(option)
```

Configures `x86_engine`. Refer to [x86_options.h](../../include/ppl/nn/engines/x86/x86_options.h) for available options.

### CUDA

#### CudaEngineOptions

Refer to [cuda_engine_options.h](../../include/ppl/nn/engines/cuda/cuda_engine_options.h) for more details.

#### CudaEngineFactory

```python
cuda_options = CudaEngineOptions()
cuda_engine = CudaEngineFactory::Create(cuda_options)
```

Creates an `Engine` instance running on NVIDIA GPUs.

```python
ret_code = cuda_engine.Configure(option)
```

Configures `cuda_engine`. Refer to [cuda_options.h](../../include/ppl/nn/engines/cuda/cuda_options.h) for available options(some options are not exported yet).

## Other Utilities

```python
version_str = pypplnn.GetVersionString()
```

Returns the version string of current version.

```python
msg_str = pyppl.common.GetRetCodeStr(ret_code)
```

Returns a human-readable message of `ret_code`.

```python
pyppl.common.SetLoggingLevel(log_level)
log_level = pyppl.common.GetLoggingLevel()
```

Sets and gets the current logging level respectively. Logging levels are defined in `pyppl.common`.
