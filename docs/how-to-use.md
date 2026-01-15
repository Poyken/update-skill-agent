# Cách sử dụng nền tảng hiệu quả

## Cấu trúc thư mục

```
update-skill-agent/
├── prompts/          # Nơi bạn copy và tùy chỉnh các mẫu lệnh
├── tutorials/        # Các bài học đi từ lý thuyết đến thực hành
├── challenges/       # Nơi để bạn tự thử thách và đánh giá bản thân
├── best-practices/   # Tham khảo các kinh nghiệm "xương máu"
└── templates/        # Áp dụng trực tiếp vào dự án thực tế
```

## Mẹo để đạt hiệu quả cao nhất

### 1. Khi sử dụng Thư viện Prompt (`prompts/`)

- **Đừng chỉ copy-paste:** Hãy đọc hiểu cấu trúc của prompt mẫu.
- **Tùy biến ngữ cảnh (Context):** Thay đổi các thông tin về Tech Stack, requirements để phù hợp với dự án của bạn.
- **Quan sát kết quả:** Nếu AI trả về chưa ưng ý, hãy xem lại phần "Best Practices" để điều chỉnh prompt.

### 2. Khi học các Bài học (`tutorials/`)

- **Vừa học vừa làm:** Mở AI Agent của bạn lên và thử nghiệm ngay các ví dụ trong bài học.
- **Đối chiếu:** So sánh code AI viết ra trước và sau khi bạn áp dụng các kỹ thuật như CLEAR Framework.

### 3. Khi thực hiện Thử thách (`challenges/`)

- **Tự làm trước:** Đừng xem phần "Sample Solution" ngay. Hãy thử viết prompt của riêng mình.
- **Cải thiện dần dần:** Nếu lần đầu AI không làm đúng, hãy dùng kỹ thuật "Iterative Refinement" (Cải thiện lặp lại) để dẫn dắt AI đến kết quả đúng.

### 4. Giao tiếp với AI bằng tiếng Việt hay tiếng Anh?

- Bạn hoàn toàn có thể dùng tiếng Việt để mô tả logic.
- **Mẹo:** Nên giữ nguyên các thuật ngữ chuyên môn bằng tiếng Anh (ví dụ: `useEffect`, `middleware`, `generic types`) để AI (vốn được train nhiều bằng tiếng Anh) hiểu chính xác nhất.
