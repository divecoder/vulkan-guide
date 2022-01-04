# Runtime Error and warning
Introduced by
```
void VulkanEngine::init_vulkan()
{
	vkb::InstanceBuilder builder;

	//make the vulkan instance, with basic debug features
	auto inst_ret = builder.set_app_name("Example Vulkan Application")
		.request_validation_layers(bUseValidationLayers)
		.use_default_debug_messenger()
		.require_api_version(1, 1, 0)
		.build();

```
## harmless ?
[ERROR: General]
loader_get_json: Failed to open JSON file C:\Program Files\NVIDIA Corporation\Nsight Systems 2019.4.3\Target-Windows\x86_64\VkLayers\VkLayer_nsight-sys_windows.json

[WARNING: General]
loaderAddLayerProperties: C:\VulkanSDK\1.2.182.0\Bin\VkLayer_api_dump.json invalid layer manifest file version 1.2.0.  May cause errors.

[WARNING: General]
loaderAddLayerProperties: C:\VulkanSDK\1.2.182.0\Bin\VkLayer_device_simulation.json invalid layer manifest file version 1.2.0.  May cause errors.

[WARNING: General]
loaderAddLayerProperties: C:\VulkanSDK\1.2.182.0\Bin\VkLayer_gfxreconstruct.json invalid layer manifest file version 1.2.0.  May cause errors.

[WARNING: General]
loaderAddLayerProperties: C:\VulkanSDK\1.2.182.0\Bin\VkLayer_khronos_synchronization2.json invalid layer manifest file version 1.2.0.  May cause errors.

[WARNING: General]
loaderAddLayerProperties: C:\VulkanSDK\1.2.182.0\Bin\VkLayer_khronos_validation.json invalid layer manifest file version 1.2.0.  May cause errors.

[WARNING: General]
loaderAddLayerProperties: C:\VulkanSDK\1.2.182.0\Bin\VkLayer_screenshot.json invalid layer manifest file version 1.2.0.  May cause errors.
The gpu has a minimum buffer alignement of 64

[WARNING: Performance]
Validation Performance Warning: [ UNASSIGNED-CoreValidation-Shader-OutputNotConsumed ] Object 0: handle = 0x67022e000000004b, type = VK_OBJECT_TYPE_SHADER_MODULE; | MessageID = 0x609a13b |
