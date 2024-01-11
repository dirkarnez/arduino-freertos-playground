https://github.com/feilipu/Arduino_FreeRTOS_Library/tree/master/examples

### TODOs
- [ ] Task operation
- [ ] inter-task communication
  - `QueueHandle_t`
  - Notification
- [ ] fsm
- [ ] interrupt attach
- [ ] semaphores

### Snipppets
- Task operation
  - ```cpp
    void TaskSerial(void* pvParameters){
    /*
     Serial
     Send "s" or "r" through the serial port to control the suspend and resume of the LED light task.
     This example code is in the public domain.
    */
      (void) pvParameters;
       for (;;) // A Task shall never return or exit.
       {
        while(Serial.available()>0){
          switch(Serial.read()){
            case 's':
              vTaskSuspend(TaskBlink_Handler); 
              Serial.println("Suspend!");
              break;
            case 'r':
              vTaskResume(TaskBlink_Handler);
              Serial.println("Resume!");
              break;
          }
          vTaskDelay(1);
        }
       }
    }
    ```
