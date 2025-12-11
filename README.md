### Open-EP introduces PIXPAPER-213-M
A 2.13 inch prototype mono color Electronic Paper Display (EPD) module, in collaboration with Triangle Alien Studio for the first time, showcasing craftsmanship and excellent hardware quality.<br>
It is based on an SPI interface and is fully compatible with our NXP edge fanless AIoT computing solutions.<br>
We will gradually port it to more embedded platforms, so this page will be updated periodically!

----------------------


#### Overview
|                         Model                         | SKU.                                                  |                       Driver support                       |
| :----------------------------------------------------------: | :----------------------------------------------------------- | :---------------------------------------------------------| 
| <img src="https://github.com/user-attachments/assets/e00df005-ca89-47c5-b0a2-7c61cb5a84d4" width="200"> | **PIXPAPER-213-M (Mono)** <br />  | ARM MPU platform <br> ARM MCU platform |


|                         Specifications                         |                                                   |
| :----------------------------------------------------------: | :----------------------------------------------------------- |
| Screen size | 2.13 inch |
| Resolution | 250x122 |
| Color | black, white, 4 grayscale |
| PPI | 130.6 |
| Active area | 23.7046×48.55(mm) |
| Interface | SPI |
| Partial update | YES |
| PINOUT | 3.3V, GND, MOSI, SCK, CS#, DC#, RST#, BUSY (DC#, RST#, BUSY are GPIOs)|
| Enclosure | Plastic using 3D printer |
|Operating temperature| 0-40 ℃ |

----------------------

#### MPU Supported Platforms (ARM64)

| **Platform** | <a href="https://www.renesas.com/" target="_blank"><br> <img src="https://www.macnica.com/apac/galaxy/zh_tw/products-support/products/renesas.coreimg.jpeg/structure/_jcr_content/root/container/container/bannerimage/1653236359047.jpeg" width="" height="100" /></a> | Status |<a href="https://www.nxp.com/" target="_blank"><br> <img src="https://github.com/TechNexion-Vision/.github/assets/28101204/67cc61c0-6bb7-44d5-889a-1ba5d4c0b9b5" width="" height="80" /></a> | Status | <a href="https://www.telechips.com/" target="_blank"><img width="" height="90" alt="image" src="https://github.com/user-attachments/assets/4f260b12-4d99-42e3-b9bd-6b90b2bbec16" /> | Status |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| **Porting Guide** | [KAKIP SBC(RZ/V2H)](https://github.com/open-ep/PIXPAPER-213-M/blob/main/KAKIP_PIXPAPAER-213-M.md) | &#10004;  |  [FRDM-IMX93(IMX93)](https://github.com/open-ep/PIXPAPER-213-M/blob/main/FRDM-IMX93_PIXPAPAER-213-M.md) | &#10004;| [TOPST D3-G(Dolphin 3M)](https://github.com/open-ep/PIXPAPER-213-M/blob/main/D3-G_PIXPAPAER-213-M.md) | &#10004; |
