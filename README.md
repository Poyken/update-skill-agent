# 🎯 Lộ Trình Làm Chủ AI Agent cho Developer

Chào mừng bạn đến với chương trình đào tạo nâng cao kỹ năng sử dụng AI trong lập trình. Thay vì sử dụng AI như một chatbot thông thường, lộ trình này sẽ giúp bạn biến AI thành một **Cộng sự (Pair Programmer)** thực thụ.

---

## 🛤️ Lộ Trình Học Tập Từng Bước

### 🏁 Bước 1: Tư duy đúng về AI Agent (Cần 1 giờ)

Trước khi viết code, bạn cần hiểu AI Agent làm được gì và khi nào thì **không** nên dùng nó.

1.  **Hiểu về AI Agent:** Đọc [Bài 1: AI Agent là gì?](./tutorials/01-introduction/lesson-01-what-is-ai-agent.md) để phân biệt AI với IDE truyền thống.
2.  **Xác định thời điểm dùng:** Đọc [Bài 2: Khi nào nên dùng AI Agent?](./tutorials/01-introduction/lesson-02-when-to-use.md) để tránh lãng phí thời gian và rủi ro bảo mật.

### ✍️ Bước 2: Kỹ năng viết Prompt cốt lõi (Cần 2 giờ)

Học cách giao tiếp để AI luôn đưa ra kết quả chính xác ngay từ lần đầu.

1.  **Công thức CLEAR:** Đọc [Bài 1: Khung CLEAR](./tutorials/02-basic-prompting/lesson-01-clear-framework.md). Đây là chìa khóa quan trọng nhất.
2.  **Mẫu câu lệnh phổ biến:** Tham khảo [Bài 2: Các mẫu Prompt cho Dev](./tutorials/02-basic-prompting/lesson-02-common-patterns.md) để biết cách gán vai trò (Role Assignment) và bối cảnh.

### 🚀 Bước 3: Kỹ thuật suy luận Nâng cao (Cần 3 giờ)

Giải quyết các bài toán khó, lỗi logic phức tạp và hệ thống lớn.

1.  **Suy luận từng bước:** Học kỹ thuật [Chain of Thought](./tutorials/03-advanced-techniques/lesson-01-chain-of-thought.md).
2.  **Cải thiện lặp lại:** Học cách [dẫn dắt AI qua nhiều lượt chat](./tutorials/03-advanced-techniques/lesson-02-iterative-refinement.md).
3.  **Quản lý bộ nhớ AI:** Master kỹ năng [Quản lý Ngữ cảnh (Context)](./tutorials/03-advanced-techniques/lesson-03-context-management.md).

### 🛠️ Bước 4: Thực hành và "Xương máu" (Cần 4 giờ)

Áp dụng lý thuyết vào các thử thách thực tế và học cách tránh sai lầm.

1.  **Kinh nghiệm tốt nhất:** Xem danh sách [Mô hình hiệu quả](./best-practices/patterns/effective-patterns.md).
2.  **Lỗi cần tránh:** Rà soát các [Anti-patterns](./best-practices/anti-patterns/common-mistakes.md) để không trở thành "lập trình viên copy-paste".
3.  **Thử thách thực tế:**
    - [Cấp độ Dễ: Refactor code cũ](./challenges/beginner/challenge-01-refactor.md)
    - [Cấp độ Dễ: Sửa lỗi cho API](./challenges/beginner/challenge-02-debug-api.md)

### 🏗️ Bước 5: Dự án Thực tế & Workflows (Hành động ngay)

Áp dụng toàn bộ kỹ năng để xây dựng dự án và chuẩn hóa quy trình làm việc.

1.  **Dự án Todo App:** Thực hành xây dựng [Frontend hoàn chỉnh](./tutorials/04-real-projects/project-01-todo-app.md).
2.  **Dự án REST API:** Thực hành xây dựng [Backend chuyên nghiệp](./tutorials/04-real-projects/project-02-rest-api.md).
3.  **Workflows mẫu:** Sử dụng các [Templates](./templates/) cho công việc hàng ngày của bạn.

### ⚙️ Bước 6: Thiết lập AI cho Dự án Hiện có (Quan trọng!)

Khi bạn đã có dự án riêng, cần "dạy" AI hiểu codebase của bạn.

1.  **Tạo thư mục `.agent`:** Đọc hướng dẫn [Thiết lập .agent cho dự án](./templates/agent-setup/README.md).
2.  **Sử dụng các templates:** Copy các file mẫu sẵn có:
    - [project-context.template.md](./templates/agent-setup/project-context.template.md) - Mô tả dự án
    - [conventions.template.md](./templates/agent-setup/conventions.template.md) - Quy chuẩn code
    - [progress.template.md](./templates/agent-setup/progress.template.md) - Theo dõi tiến độ

---

## 🧰 Thư viện tra cứu nhanh (Cheat Sheet)

| Tác vụ                 | Tài liệu tham khảo nhanh                                             |
| ---------------------- | -------------------------------------------------------------------- |
| **Viết code mới**      | [Prompts Implementation](./prompts/coding/feature-implementation.md) |
| **Gặp lỗi/Bug**        | [Prompts Debugging](./prompts/debugging/error-analysis.md)           |
| **Refactor/Migration** | [Prompts Refactoring](./prompts/refactoring/code-improvement.md)     |
| **Viết Unit Test**     | [Prompts Testing](./prompts/testing/test-generation.md)              |
| **Thiết kế hệ thống**  | [Prompts Architecture](./prompts/architecture/system-design.md)      |
| **Setup AI cho dự án** | [Agent Setup Guide](./templates/agent-setup/README.md)               |

---

_Lưu ý: AI thay đổi rất nhanh, hãy luôn thực hành và cập nhật các mẫu prompt của riêng bạn vào thư mục `/prompts`._
