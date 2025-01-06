# esp32-built-in-temperature-sensor

how to read ESP32-S2 built-in temperature sensor

```c++
#include "driver/temperature_sensor.h"

void read_temperature() {
    static temperature_sensor_handle_t temp_handle;
    if (!temp_handle) {
        temperature_sensor_config_t temp_sensor = TEMPERATURE_SENSOR_CONFIG_DEFAULT(20, 100);
        temperature_sensor_install(&temp_sensor, &temp_handle);
    }

    temperature_sensor_enable(temp_handle);
    float tsens_out;
    temperature_sensor_get_celsius(temp_handle, &tsens_out);
    temperature_sensor_disable(temp_handle);

    Serial.printf("Temperature: %.02f Celsius\r\n", tsens_out);
}
 
void setup() {
  Serial.begin(115200); 
}

void loop() {
  read_temperature();
  delay(5000);
}
```
