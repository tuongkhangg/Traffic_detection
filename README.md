# Team 03:
## Thành Viên:
* Đoàn Phú Đức
* Dat Tran
* Duong Le Tuong Khang
* Quang Long Nguyen

## Stage 1: Detection
### Colab: Baseline_EfficientDet
* Sử dụng pretrained model Efficientdet-d4 để thực hiện detection
#### Nhận xét:
* Model detect khá tốt car, bus, truck. Tuy vậy lại bỏ qua khá nhiều motor, điều này ảnh hưởng đến việc tracking ở bước tiếp theo.
* Ở cam 09 và cam 10 ( 2 cam tối), model detect kém, bỏ qua khá nhiêu xe và bị nhiễu khá nhiều. Vì vậy nhóm đã quyết định thực hiện lại việc label dữ liệu, train lại model để cải thiện khả năng detect ở cam 09 và cam 10, đồng thời tăng detect xe máy.


### Colab: train_efficientdet
* Train model với dữ liệu được gán nhãn  
* Dữ liệu được gán nhãn ở cam 01, cam 02, cam 03, cam 04, cam 09 và cam 10. Các nhãn được gán là: Bicycle, Motor, Truck, Bus, Car và ở bước detection được chuyển thành 4 class như yêu cầu ở cuộc thi HCMcity AI Challenges.
* Link dataset cam 10, fullcam(cam 01 + cam 02 + cam 03 + cam 04 + cam 09 + 1 phần cam 10 (khoảng 2000 tấm): https://drive.google.com/drive/folders/1GGI2TXdGIdsCXGqaMl1IvT6ETytQTDyK?usp=sharing

#### Training:
* Nhóm thực hiện theo 2 cách:
  * Cách 1: chỉ train với dữ liệu cam 10 ( cam 10 nhóm label được khoảng trên 4000 tấm) và dùng dữ liệu đó detect cho cam 10. (link file pth: và onnx: https://drive.google.com/drive/folders/1-34bMb8YwSLPlfpc9Zd2OzjbAtZxMb5l?usp=sharing )
  * Cách 2: train với toàn bộ dữ liệu cam 01, cam 02, cam 03, cam 04, cam 09, cam 10 ( cam 01 -> cam 09: mỗi cam khoảng 200 tấm) và thực hiện detect lại cho toàn bộ dataset.(
  link pth và onnx: https://drive.google.com/drive/folders/1Xf0XT2EV2ChKSAR5h6k2wwPvRdEteij4?usp=sharing )
#### Nhận xét:
* Sau khi thực hiện train lại, model đã có thể detect tốt hơn ở cam 09 và cam 10 ( cải thiện score sau khi thực hiện train lại).
* Tuy vậy, điểm số cải thiện không nhiều. Điều này có thể do việc thực hiện fine-tuning không tốt, ảnh hưởng đến weight ban đầu của model. 
## Stage 2: Tracking
