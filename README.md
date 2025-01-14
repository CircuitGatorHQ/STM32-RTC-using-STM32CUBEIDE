# STM32-RTC-using-STM32CUBEIDE
Below is an easy and short code you can use to access the real time clock (RTC) of an STM32 microcontroller. The date and time obtained is displayed on a serial terminal using UART.
The full tutorial video is available on YouTube:

    /* Private includes ----------------------------------------------------------*/
    /* USER CODE BEGIN Includes */
    #include <stdio.h>
    /* USER CODE END Includes */
    
    
    /* Private variables ---------------------------------------------------------*/
    /* USER CODE BEGIN PV */
    char buffer[100];  // Buffer to hold time and date strings
    /* USER CODE END PV */
    
    
    /* USER CODE BEGIN 2 */
    RTC_TimeTypeDef sTime;
    RTC_DateTypeDef sDate;
    /* USER CODE END 2 */
    
    /* USER CODE BEGIN WHILE */
      while (1)
      {
        /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
      // Get the current time and date from RTC
      HAL_RTC_GetTime(&hrtc, &sTime, RTC_FORMAT_BIN);
      HAL_RTC_GetDate(&hrtc, &sDate, RTC_FORMAT_BIN);

      // Format time and date into a string
      snprintf(buffer, sizeof(buffer), "Time: %02d:%02d:%02d, Date: %02d-%02d-%02d\r\n",
               sTime.Hours, sTime.Minutes, sTime.Seconds,
               sDate.Date, sDate.Month, sDate.Year + 2000);

      // Transmit the formatted string over USART
      HAL_UART_Transmit(&huart2, (uint8_t*)buffer, strlen(buffer), HAL_MAX_DELAY);

      HAL_Delay(1000);  // Update every second
      }
      /* USER CODE END 3 */
