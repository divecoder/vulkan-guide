# Runtime Error and warning
## Layers
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
### Introduced by
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
//....
}
	VkInstanceCreateInfo instance_create_info = {};
	instance_create_info.sType = VK_STRUCTURE_TYPE_INSTANCE_CREATE_INFO;
	detail::setup_pNext_chain (instance_create_info, pNext_chain);
	instance_create_info.flags = info.flags;
	instance_create_info.pApplicationInfo = &app_info;
	instance_create_info.enabledExtensionCount = static_cast<uint32_t> (extensions.size ());
	instance_create_info.ppEnabledExtensionNames = extensions.data ();
	instance_create_info.enabledLayerCount = static_cast<uint32_t> (layers.size ());
	instance_create_info.ppEnabledLayerNames = layers.data ();

	Instance instance;
	VkResult res = detail::vulkan_functions ().fp_vkCreateInstance (
	    &instance_create_info, info.allocation_callbacks, &instance.instance);


```
### Solution try
try the solution mentioned at https://github.com/godotengine/godot/issues/36688
>Had to use RegScanner to find the culprit, and it turns out that it was a registry key that was wrong. The specific location is:

>HKEY_LOCAL_MACHINE\SOFTWARE\Khronos\Vulkan\ExplicitLayers

>That above-mentioned wrong location is stored in this folder. It contains Vulkan SDK JSON locations, the 2020 version, and the 2019 version. The location in the 2020 version was correct, so I uninstalled the 2019 version. For some reason, the 2019 key did not delete itself when I uninstalled the 2019 version, so I had to manually delete it in Registry Editor. Now, there are no errors from that location.

![image](https://user-images.githubusercontent.com/16042439/148046508-6601030a-2b4a-4125-8f45-bf170ef03b3d.png)
#### Vulkan\ExplicitLayers
[Brief guide to Vulkan layers](https://renderdoc.org/vulkan-layer-guide.html)

