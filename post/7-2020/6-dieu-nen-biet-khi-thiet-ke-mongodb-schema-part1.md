# 6 quy tắc nên biết khi thiết kế mongoDB schema: phần 1



*Viết bởi William Zola, Lead Technical Support Engineer tại MongoDB (2014)*

## Mở đầu

"Tôi cố khá nhiều kinh nghiệm với SQL, với MongoDB tôi chỉ là beginner. Làm sao triển khai mối quan hệ 1-N lên database?" Đây là câu hỏi phổ biến tôi nhận được từ người dùng sau giờ làm việc tại MongoDB.

Tôi không có câu trả lời ngắn gọn cho câu hỏi này bởi vì không chỉ có 1 cách triển khai, mà là có rất rất nhiều cách để thực hiện điều này. MongoDB có rất nhiều từ ngữ sắc thái khác nhau để biểu đạt điều này. Tại SQL, có câu để diển tả điều này là "mối quan hệ 1-N". Để tôi đưa bạn đi một tour lựa chọn cách modeling mối quan hệ 1-N trong MongoDB.

