# STM32 智慧溫控風扇系統 (Smart Temperature Fan Control)

本專題基於 STM32 實現 PWM 風扇轉速控制、TIM 輸入捕捉 (Input Capture) 轉速測量，以及外部中斷 (EXTI) 開關控制。

---

## 🛠️ 硬體與軟體環境
- **微控制器**：STM32 Nucleo 板卡
- **開發工具**：STM32CubeIDE
- **周邊配置**：
  - `PA8`：TIM1_CH1 (PWM 輸出)
  - `PA0`：TIM2_CH1 (TIM Input Capture 輸入捕捉)
  - `PC13`：EXTI 外部中斷 (B1 藍色按鍵)
  - `PA5`：GPIO Output (LD2 綠色 LED 指示燈)

---

## 🔄 測試驗證 (Hardware Loopback Test)
為了驗證計時器 PWM 輸出與輸入捕捉計算的準確度，採用硬體自環測試 (Loopback)：
1. 使用杜邦線將 **`PA8` (PWM 輸出)** 與 **`PA0` (輸入捕捉)** 跨接。
2. 啟動 Debug 模式並開啟 `Live Expressions` 觀察全域變數 `rpm_val`。
3. 實測結果：`rpm_val` 穩定顯示為 **`30000`** RPM，證明 TIM1 與 TIM2 邏輯運作正常。
4. 按下板載 `PC13` 按鍵，可正常觸發 EXTI 切換 `PA5` LED 狀態。

---

## 📂 專案結構
- `Core/Src/main.c`：主要主程式、Timer 初始化與中斷服務常式
- `Core/Inc/`：頭文件與定義
- `lab1.ioc`：STM32CubeMX 腳位與周邊配置檔
