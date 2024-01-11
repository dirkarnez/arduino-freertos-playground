https://github.com/feilipu/Arduino_FreeRTOS_Library/tree/master/examples

### TODOs
- [ ] Task operation
- [ ] inter-task communication
  - `QueueHandle_t`
    - `xQueueReceive`
    - `xQueueSend`
  - Notification
- [ ] fsm
  - use `xQueueCreate` to create a queue of length only 1 to store state
  - then use a simple switch case to do logic
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
  - Queue (https://github.com/feilipu/Arduino_FreeRTOS_Library/blob/master/examples/StructQueue/StructQueue.ino)
    - ```cpp
      // Include queue support
      #include <queue.h>
      
      // Define a struct
      struct pinRead {
        int pin;
        int value;
      };
      
      /* 
       * Declaring a global variable of type QueueHandle_t 
       * 
       */
      QueueHandle_t structQueue;
      
      void setup() {
      
        /**
         * Create a queue.
         * https://www.freertos.org/a00116.html
         */
        structQueue = xQueueCreate(10, // Queue length
                                    sizeof(struct pinRead) // Queue item size
                                    );
        if (structQueue != NULL) {
          // TODO
        }
      }
      ```
