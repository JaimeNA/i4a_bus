# Code base notes

- Each device has two posible modes, either it's a `STATION` or an `AP`(access point).
- The orientation of each device determines its function:

	| Code  | Orientation |
	|-------|-------------|
	| North | 0           |
	| South | 1           |
	| East  | 2           |
	| West  | 3           |
	| None  | 9           |

- The each esp32 controller ring program consist of three main parts: `lowlevel`, `internal` and `netif`. Each has their own queue that stores incoming payloads.

## Structure

- **Components**: Library, has all the needed component to setup an application.
- **Docs**: Minimal software documentation, hardware documentation and nodes mainboard schematics labeled as kicad.
- **Test**: Test for the library and examples of the workflow of the library.

## Minimal setup

In order to remove any token ring related code and leave only a basic SPI implementation, changes on the `internal` and `routing` folders had to be made.

## Control flow

### Access Point
Based on test code:

1. Setup config
2. Create a `Device`(Components->wireless->device), this will be our node, and have a pointer to it.

```
struct Device {
	// Members
	char device_uuid[32];
	uint8_t device_orientation;
	uint8_t device_is_root;
	char ssid[32];
	char password[64];
	uint8_t channel;
	Device_Mode mode;
	Device_State state;
	AccessPoint access_point;
	AccessPointPtr access_point_ptr;
	Station station;
	StationPtr station_ptr;
};
```
3. Initialize wifi and ring
4. The device must be initialized with an `uuid`, `orientation`, `network_prefix`, `ap_channel`, `ap_max_sta`, `device_is_root`, `mode`.
5. Start the access point.

### Station

Similar to an access point, changing its mode. 


## Internal logic



