# Cách training mô hình

## Cấu trúc dataset
- Vào thư mục dataset rồi xem
  
## Sửa các file sau:
- config.yaml:
  - sửa đường dẫn TRAIN_PATH, TEST_PATH và CHECKPOINT
- train.py:
  - line 23: sửa đường dẫn file config.yaml
- ./src/lora.py:
  - line 172: sửa đường dẫn file config.yaml
- ./src/segment_anything/build_sam:
  - line 104: sửa đường dẫn checkpoint
  - Tải file checkpoint để cùng thư mục LoRA-SAM
```bash
wget https://dl.fbaipublicfiles.com/segment_anything/sam_vit_b_01ec64.pth
```
## Training
```bash
cd LoRA-SAM
CUDA_VISIBLE_DEVICES=1 python train.py
```

# Inference
- Vào inference.py đọc các tham số. Sau khi train xong sẽ có một file tên lora_rank512.safetensors đặt trong thư mục lora_weights. Ví dụ về test file 1.png ở thư mục images và lưu vào thư mục output với tên 1_test.png và tính IoU với ảnh mask 1_mask.png ở thư mục masks:
```bash
CUDA_VISIBLE_DEVICES=0 python inference.py -l ./lora_weights/lora_rank512.safetensors ./images/1.png -o ./output/1_test.png -m ./masks/1_mask.png
```
