# 🌟 ZenID: High-Performance Face Swap & Fusion 🌟
### (Một phiên bản Fork được tối ưu hóa hiệu năng và tính năng)

Dự án này là một phiên bản **fork** từ [**ZenID gốc của vuongminh1907/ZenAI**](https://github.com/vuongminh1907/ComfyUI_ZenID), tập trung vào việc cải thiện và tối ưu hóa quy trình làm việc. Toàn bộ công lao cho các tính năng cốt lõi thuộc về tác giả gốc, và chúng tôi xin ghi nhận công sức của họ.

Phiên bản này ra đời sau quá trình nghiên cứu và phát triển sâu rộng, tập trung vào hai mục tiêu chính: **tối ưu hóa hiệu năng** và **mở rộng tính năng cốt lõi**.

**✨ Nếu bạn thấy những cải tiến này hữu ích, hãy cân nhắc tặng một sao cho cả dự án này và [dự án ZenID gốc](https://github.com/vuongminh1907/ComfyUI_ZenID)! ✨**

---

## 📑 **Mục Lục**
1. [🚀 **Các Cải tiến Đột phá trong phiên bản này**](#enhancements)
    * [Tối ưu hóa Hiệu năng (Caching & Workflow)](#performance)
    * [Nâng cấp Tính năng (Xử lý nhiều ảnh)](#features)
2. [✨ Các tính năng gốc của ZenID](#original-features)
3. [⚙️ Cài Đặt](#installation)

---

## 🚀 **Các Cải tiến Đột phá trong phiên bản này** <a name="enhancements"></a>

### 1. Tối ưu hóa Hiệu năng (Caching & Workflow) <a name="performance"></a>

#### a. Caching Model thông minh
- **Vấn đề:** Phiên bản gốc tải lại các model (InstantID, InsightFace) mỗi khi chạy workflow, gây lãng phí thời gian.
- **Giải pháp:** Phiên bản này tích hợp một **cơ chế cache (bộ nhớ đệm) thông minh**. Các model sẽ chỉ được tải vào VRAM một lần duy nhất trong suốt phiên làm việc.
- **Kết quả:** Các lần chạy lặp lại gần như **tức thì**, tiết kiệm rất nhiều thời gian chờ đợi.

#### b. Workflow "Xử lý theo vùng" hiệu năng cao
- **Vấn đề:** Xử lý toàn bộ ảnh để thay đổi một vùng nhỏ là không hiệu quả.
- **Giải pháp:** Cung cấp một workflow tiên tiến sử dụng kỹ thuật **"Cắt & Ghép" (Crop & Stitch)**. Quy trình này chỉ xử lý vùng mặt nạ bạn chỉ định, sau đó ghép kết quả trở lại.
- **Kết quả:**
    - **⚡ Tốc độ tăng vọt:** Thời gian tạo ảnh giảm đáng kể.
    - **📉 Tiết kiệm VRAM:** Cho phép chạy Face Swap ở độ phân giải cao trên các GPU yếu hơn.
- **Yêu cầu:** Workflow này cần custom node **[ComfyUI-Inpaint-CropAndStitch](https://github.com/lquesada/ComfyUI-Inpaint-CropAndStitch)**.

**➡️ Tải và trải nghiệm workflow hiệu năng cao tại đây:** [`ZenID_HiPerf_FaceSwap.json`](https://github.com/blackmoon96/ComfyUI_ZenID_optimal/blob/main/workflow/ZenID_HiPerf_FaceSwap.json)

### 2. Nâng cấp Tính năng (Xử lý nhiều ảnh) <a name="features"></a>

#### a. Tổng hợp Embedding từ nhiều ảnh tham chiếu
- **Vấn đề:** Một ảnh tham chiếu duy nhất có thể không nắm bắt được đầy đủ các đặc điểm của một khuôn mặt ở các góc độ và điều kiện ánh sáng khác nhau.
- **Giải pháp:** Node `ApplyZenID` giờ đây có thể nhận đầu vào là một **batch nhiều ảnh mặt**. Nó sẽ tự động trích xuất embedding từ mỗi ảnh và tổng hợp chúng lại thành một embedding đại diện duy nhất, chính xác hơn.
- **Kết quả:** **Độ chính xác và nhất quán của khuôn mặt được cải thiện đáng kể**, đặc biệt khi bạn muốn tạo ra một nhân vật ở nhiều tư thế khác nhau.
- **Tùy chọn:** Cung cấp các phương pháp tổng hợp khác nhau (ví dụ: `average`, `norm_average`) để người dùng có thể tinh chỉnh.

---







# 🌟 ZenID: Face Swap 🌟
Repo này được lấy cảm hứng và modify từ [**InstantID**](https://github.com/instantX-research/InstantID) và [**InstantID Comfy**](https://github.com/cubiq/ComfyUI_InstantID)

**ZenID Node** đã được chỉnh sửa lại để phục vụ các tác vụ chuyên biệt như _Face Swap_

**✨ Hãy ủng hộ sự phát triển thêm của dự án bằng cách đánh dấu sao cho dự án! ✨**

## 📑 **Mục Lục** 
1. [Tính Năng ZenID](#zenid-features) 
    * [Face Swap](#zenid-face-swap) 
    * [Face Combine](#zenid-face-combine) 
2. [Cài Đặt](#installation)

## 🌟 **Tính Năng ZenID** <a name="zenid-features"></a>

### 🔗 **ZenID Face Swap** <a name="zenid-face-swap"></a>
- **Workflows**
    File mẫu [`ZenID_FaceSwap.json`](https://github.com/vuongminh1907/ComfyUI_ZenID/blob/main/workflow/ZenID_FaceSwap.json) được đính kèm trong thư mục `workflow`.

    Ở bước này, bạn có thể dùng mask tự vẽ hoặc để cho nodes tự sinh ra mask để swap

    **NOTE: Dùng tay tự vẽ mask thì kết quả đẹp hơn**

    ![ZenID Face Swap Example](https://github.com/vuongminh1907/ComfyUI_ZenID/blob/main/examples/zenid_faceswap.png)

- **Ví Dụ**
    - **Hình Ảnh Gốc**  
      <img src="https://github.com/vuongminh1907/ComfyUI_ZenID/blob/main/examples/blackwukong.png" width="300" /> 
      <img src="https://github.com/vuongminh1907/ComfyUI_ZenID/blob/main/examples/domixi.png" width="300" />

    - **Kết Quả**  
       <img src="https://github.com/vuongminh1907/ComfyUI_ZenID/blob/main/examples/result_faceswap.png" width="600" />


### 🔗 **ZenID Face Combine** <a name="zenid-face-swap"></a>
- **Workflows**

    File mẫu [`ZenID_combineFace.json`](https://github.com/vuongminh1907/ComfyUI_ZenID/blob/main/workflow/ZenID_combineFace.json) được đính kèm trong thư mục `workflow`.
    ![ZenID Face Combine Example](https://github.com/vuongminh1907/ComfyUI_ZenID/blob/main/examples/zenid_combineface.png)
- **Ví Dụ**
    - **Hình Ảnh Gốc**  
      <img src="https://github.com/vuongminh1907/ComfyUI_ZenID/blob/main/examples/haitu.jpg" width="300" /> 
      <img src="https://github.com/vuongminh1907/ComfyUI_ZenID/blob/main/examples/sontung.jpg" width="300" />

    - **Kết Quả**  
       <img src="https://github.com/vuongminh1907/ComfyUI_ZenID/blob/main/examples/result_facecombine.png" width="600" />

## ⚙️ Cài đặt <a name="installation"></a>
1. Clone repo của ComfyUI 
```
git clone https://github.com/comfyanonymous/ComfyUI
```
2. Sao chép hoặc tải về repo này vào thư mục `ComfyUI/custom_nodes/`.
```
cd ComfyUI/custom_nodes/
git clone https://github.com/vuongminh1907/ComfyUI_ZenID
```
3. Tải model để có thể chạy được
```
pip install -r ComfyUI_ZenID/requirements.txt
python ComfyUI_ZenID/downloadmodel.py
```
4. Khởi chạy ComfyUI.

