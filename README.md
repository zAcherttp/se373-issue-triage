# SE373 · BTVN-02 · Issue Triage mini-app

Thang Tuấn Phát · 23521150

Mini-app phân loại issue phần mềm, làm lại theo demo Buổi 02. Mỗi script là một
bước tăng dần, từ một lời gọi LLM trần tới UI Streamlit có function calling.

| Script | Yêu cầu của đề | Nội dung |
|---|---|---|
| `00_minimal_triage.py` | nhận mô tả issue | một lời gọi chat completion, trả prose |
| `01_measure_tokens.py` | (offline) | so sánh token EN/VI qua `tiktoken`, không gọi API |
| `02_structured_output.py` | prompt template; `IssueTriage` bằng Pydantic; validate ở application | so sánh prompt-only JSON với `response_format=IssueTriage` |
| `triage_workflow.py` | khai báo tool; application thực thi | `get_component_owner` khai báo bằng JSON Schema, validate rồi mới thực thi |
| `03_function_calling.py` | trace `tool_call → execute → tool_result → final` | in trace ba phần ra terminal |
| `04_streamlit_triage.py` | UI | form nhập issue, hiện trace rồi mới hiện kết quả |

## Chạy

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env   # điền OPENAI_API_KEY, OPENAI_BASE_URL, OPENAI_MODEL

./01_measure_tokens.py          # không cần API
./00_minimal_triage.py
./02_structured_output.py
./03_function_calling.py
streamlit run 04_streamlit_triage.py --server.headless true
```

Provider bất kỳ có endpoint OpenAI-compatible đều dùng được, miễn model hỗ trợ
structured output (`response_format` json_schema) và tool calling.

## Kết quả chạy

Ảnh chụp từng demo nằm trong `screenshots/`. Bản nộp (PDF) ở repo LaTeX riêng.
