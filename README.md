openapi: 3.1.0
info:
  title: Học Tập ChatGPT API
  description: API hỗ trợ học sinh đặt câu hỏi và gửi bài tập để nhận lời giải từ chatbot học tập.
  version: 1.1.0
servers:
  - url: https://donggia39k.com/v1
    description: Server chính cho ứng dụng học tập

paths:
  /question:
    post:
      operationId: postQuestion
      summary: Gửi câu hỏi từ học sinh
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Question'
      responses:
        '200':
          description: Phản hồi từ Chatbot cho câu hỏi
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Response'

  /homework:
    post:
      operationId: postHomework
      summary: Gửi bài tập từ học sinh để nhận lời giải
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Homework'
      responses:
        '200':
          description: Phản hồi từ Chatbot với lời giải bài tập
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Solution'

components:
  schemas:
    Question:
      type: object
      properties:
        studentId:
          type: string
          description: Mã định danh của học sinh
        questionText:
          type: string
          description: Câu hỏi mà học sinh gửi
      required:
        - studentId
        - questionText

    Response:
      type: object
      properties:
        responseText:
          type: string
          description: Câu trả lời từ ChatGPT
      required:
        - responseText

    Homework:
      type: object
      properties:
        studentId:
          type: string
          description: Mã định danh của học sinh
        homeworkText:
          type: string
          description: Mô tả bài tập cần giải, ví dụ: bài toán, câu hỏi lý thuyết hoặc yêu cầu về bài tập
        subject:
          type: string
          description: Môn học liên quan, ví dụ: Toán, Vật Lý, Hóa Học, v.v.
      required:
        - studentId
        - homeworkText
        - subject

    Solution:
      type: object
      properties:
        solutionText:
          type: string
          description: Lời giải chi tiết cho bài tập từ ChatGPT
        explanation:
          type: string
          description: Giải thích bổ sung để học sinh hiểu lời giải
      required:
        - solutionText
        - explanation
