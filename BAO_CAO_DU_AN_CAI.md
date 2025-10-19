# BÁO CÁO CHI TIẾT DỰ ÁN CYBERSECURITY AI (CAI)

## TỔNG QUAN DỰ ÁN

### Giới thiệu
**Cybersecurity AI (CAI)** là một framework mã nguồn mở nhẹ và mạnh mẽ được thiết kế để hỗ trợ các chuyên gia bảo mật xây dựng và triển khai các giải pháp tự động hóa an ninh mạng dựa trên trí tuệ nhân tạo. CAI đã trở thành framework tiêu chuẩn cho AI Security, được sử dụng bởi hàng nghìn người dùng cá nhân và hàng trăm tổ chức trên toàn thế giới.

### Thông tin cơ bản
- **Tên dự án**: CAI (Cybersecurity AI)
- **Phiên bản hiện tại**: 0.5.5
- **Giấy phép**: Kép - MIT và Proprietary
- **Ngôn ngữ chính**: Python (yêu cầu ≥ Python 3.9)
- **Nhà phát triển**: Alias Robotics S.L.
- **Repository**: https://github.com/aliasrobotics/cai
- **Email liên hệ**: research@aliasrobotics.com

### Tầm nhìn và Mục tiêu
CAI được xây dựng với mục tiêu:
1. **Dân chủ hóa AI an ninh mạng**: Làm cho các công cụ AI an ninh mạng tiên tiến có thể tiếp cận được với toàn bộ cộng đồng bảo mật
2. **Minh bạch trong khả năng AI**: Cung cấp điểm chuẩn minh bạch về những gì hệ thống AI thực sự có thể làm trong bối cảnh an ninh mạng
3. **Hỗ trợ nghiên cứu**: Miễn phí cho mục đích nghiên cứu và học thuật
4. **Tăng cường hiệu quả**: Nâng cao khả năng của con người trong việc phát hiện và xử lý các lỗ hổng bảo mật

---

## KIẾN TRÚC HỆ THỐNG

### Các Thành Phần Chính

CAI được xây dựng dựa trên 8 trụ cột chính:

#### 1. **Agents (Tác nhân)**
- Định nghĩa: Hệ thống thông minh tương tác với môi trường
- Mô hình: Áp dụng mô hình ReACT (Reasoning and Action)
- Chức năng:
  - Cảm nhận môi trường qua các cảm biến
  - Suy luận về mục tiêu
  - Hành động dựa trên suy luận
- File liên quan: `src/cai/agents/`

#### 2. **Tools (Công cụ)**
- Cung cấp khả năng thực thi cho agents
- Các loại công cụ chính:
  1. **Reconnaissance** (Trinh sát): Thu thập thông tin, quét mạng
  2. **Exploitation** (Khai thác): Tấn công và khai thác lỗ hổng
  3. **Privilege Escalation** (Leo thang đặc quyền)
  4. **Lateral Movement** (Di chuyển ngang)
  5. **Data Exfiltration** (Đánh cắp dữ liệu)
  6. **Command and Control** (Chỉ huy và điều khiển)
- Công cụ tích hợp sẵn:
  - `LinuxCmd`: Thực thi lệnh hệ thống
  - `WebSearch`: Tìm kiếm OSINT
  - `Code`: Thực thi script động
  - `SSHTunnel`: Truy cập từ xa an toàn
- Thư mục: `src/cai/tools/`

#### 3. **Handoffs (Chuyển giao)**
- Cho phép agent ủy quyền nhiệm vụ cho agent khác
- Tạo chuỗi xác thực bảo mật
- Phân tách nhiệm vụ và tận dụng khả năng chuyên môn hóa
- Ví dụ: Agent CTF có thể chuyển giao cho Agent phân biệt cờ

#### 4. **Patterns (Mẫu tác nhân)**
- Định nghĩa: Paradigm thiết kế có cấu trúc cho hệ thống AI tự động
- Các loại Pattern:
  - **Swarm (Phi tập trung)**: Agents tự phân công nhiệm vụ
  - **Hierarchical (Phân cấp)**: Agent cấp cao chỉ định nhiệm vụ
  - **Chain-of-Thought (Tuần tự)**: Pipeline có cấu trúc tuyến tính
  - **Auction-Based (Đấu giá)**: Agents "đấu thầu" nhiệm vụ
  - **Recursive (Đệ quy)**: Agent tự tinh chỉnh đầu ra của mình
- Thư mục: `src/cai/agents/patterns/`

#### 5. **Turns and Interactions (Lượt và Tương tác)**
- **Interaction**: Trao đổi giữa một hoặc nhiều agents
  - Gồm: Bước suy luận (LLM) + Hành động (gọi Tools)
- **Turn**: Chu kỳ của một hoặc nhiều interactions
  - Kết thúc khi Agent trả về `None`
- Triển khai: `src/cai/core.py`

#### 6. **Tracing (Theo dõi)**
- Sử dụng Phoenix cho khả năng quan sát AI
- Dựa trên chuẩn OpenTelemetry
- Chức năng:
  - Giám sát thời gian thực
  - Phân tích tương tác agent
  - Theo dõi việc sử dụng công cụ
  - Debug chuỗi khai thác phức tạp

#### 7. **Guardrails (Rào chắn bảo mật)**
- Bảo vệ chống tấn công prompt injection
- Ngăn chặn thực thi lệnh nguy hiểm
- Các lớp bảo vệ:
  - **Input Guardrails**: Phát hiện và chặn prompt injection
  - **Output Guardrails**: Xác thực đầu ra trước khi thực thi
  - **Multi-layered Defense**: Bảo vệ đa tầng
  - **Base64/Base32 Aware**: Giải mã và phân tích payload
- File: `docs/guardrails.md`

#### 8. **HITL (Human-In-The-Loop)**
- Nhấn mạnh hoạt động bán tự động
- Cho phép can thiệp của con người
- Thao tác: Nhấn `Ctrl+C` để tương tác với agent
- Triển khai: `src/cai/core.py` và `src/cai/repl/`

### Sơ đồ Kiến trúc

```
                  ┌───────────────┐           ┌───────────┐
                  │      HITL     │◀─────────▶│   Turns   │
                  └───────┬───────┘           └───────────┘
                          │
                          ▼
┌───────────┐       ┌───────────┐       ┌───────────┐      ┌───────────┐
│  Patterns │◀─────▶│  Handoffs │◀────▶ │   Agents  │◀────▶│    LLMs   │
└───────────┘       └─────┬─────┘       └─────┬─────┘      └───────────┘
                          │                   │
                          │                   ▼
┌────────────┐       ┌────┴──────┐       ┌───────────┐     ┌────────────┐
│ Extensions │◀─────▶│  Tracing  │       │   Tools   │◀───▶│ Guardrails │
└────────────┘       └───────────┘       └───────────┘     └────────────┘
                                              │
                          ┌─────────────┬─────┴────┬─────────────┐
                          ▼             ▼          ▼             ▼
                    ┌───────────┐┌───────────┐┌────────────┐┌───────────┐
                    │ LinuxCmd  ││ WebSearch ││    Code    ││ SSHTunnel │
                    └───────────┘└───────────┘└────────────┘└───────────┘
```

---

## TÍNH NĂNG CHÍNH

### 1. Hỗ trợ Đa Mô hình AI
CAI hỗ trợ hơn **300+ mô hình AI** thông qua tích hợp LiteLLM:

#### Các Nhà cung cấp Chính:
- **Anthropic**: Claude 3.7, Claude 3.5, Claude 3, Claude 3 Opus
- **OpenAI**: O1, O1 Mini, O3 Mini, GPT-4o, GPT-4.5 Preview
- **DeepSeek**: DeepSeek V3, DeepSeek R1
- **Ollama**: Qwen2.5 72B, Qwen2.5 14B, v.v.
- **Azure OpenAI**: Hỗ trợ các mô hình doanh nghiệp
- **OpenRouter**: Giao diện thống nhất cho LLMs

### 2. Công cụ Bảo mật Tích hợp
- Công cụ trinh sát và vũ khí hóa
- Công cụ khai thác lỗ hổng
- Công cụ leo thang đặc quyền
- Công cụ di chuyển ngang
- Công cụ đánh cắp dữ liệu
- Công cụ chỉ huy và điều khiển

### 3. Kiến trúc Agent
- Thiết kế mô-đun cho các nhiệm vụ bảo mật khác nhau
- Hỗ trợ nhiều agent chuyên môn hóa
- Các pattern tác nhân linh hoạt

### 4. Tích hợp MCP (Model Context Protocol)
CAI hỗ trợ MCP qua hai cơ chế:
- **SSE (Server-Sent Events)**: Cho máy chủ web
- **STDIO (Standard Input/Output)**: Cho giao tiếp IPC cục bộ

### 5. Bảo vệ Guardrails
- Phòng chống prompt injection
- Xác thực lệnh nguy hiểm
- Phát hiện homograph Unicode
- Phân tích dựa trên AI

### 6. Streaming và Real-time
- Hỗ trợ streaming responses
- Tương tác thời gian thực
- Giám sát liên tục

---

## CÀI ĐẶT VÀ THIẾT LẬP

### Cài đặt Cơ bản
```bash
pip install cai-framework
```

### Cài đặt trên Các Hệ điều hành

#### macOS
```bash
brew update && brew install git python@3.12
python3.12 -m venv cai_env
source cai_env/bin/activate && pip install cai-framework
echo -e 'OPENAI_API_KEY="sk-1234"\nANTHROPIC_API_KEY=""\nOLLAMA=""\nPROMPT_TOOLKIT_NO_CPR=1\nCAI_STREAM=false' > .env
cai
```

#### Ubuntu 24.04
```bash
sudo apt-get update && sudo apt-get install -y git python3-pip python3.12-venv
python3.12 -m venv cai_env
source cai_env/bin/activate && pip install cai-framework
echo -e 'OPENAI_API_KEY="sk-1234"\nANTHROPIC_API_KEY=""\nOLLAMA=""\nPROMPT_TOOLKIT_NO_CPR=1\nCAI_STREAM=false' > .env
cai
```

#### Windows WSL
```bash
sudo apt-get update && sudo apt-get install -y git python3-pip python3-venv
python3 -m venv cai_env
source cai_env/bin/activate && pip install cai-framework
echo -e 'OPENAI_API_KEY="sk-1234"\nANTHROPIC_API_KEY=""\nOLLAMA=""\nPROMPT_TOOLKIT_NO_CPR=1\nCAI_STREAM=false' > .env
cai
```

#### Android
Sử dụng UserLand với Kali Linux, yêu cầu tối thiểu 8GB RAM

### Cấu hình File .env
CAI sử dụng file `.env` để cấu hình:
```bash
OPENAI_API_KEY="sk-1234"
ANTHROPIC_API_KEY=""
OLLAMA=""
PROMPT_TOOLKIT_NO_CPR=1
CAI_STREAM=false
```

### Các Biến Môi trường Quan trọng
| Biến | Mô tả |
|------|-------|
| CAI_MODEL | Mô hình sử dụng cho agents |
| CAI_DEBUG | Mức độ debug output (0-2) |
| CAI_MAX_TURNS | Số lượt tối đa |
| CAI_TRACING | Bật/tắt tracing |
| CAI_AGENT_TYPE | Loại agent (boot2root, one_tool...) |
| CAI_GUARDRAILS | Bật/tắt guardrails (mặc định: true) |
| CAI_PRICE_LIMIT | Giới hạn chi phí (USD) |

---

## CÁCH SỬ DỤNG

### Khởi động CAI
```bash
cai
```

Màn hình khởi động:
```
          CCCCCCCCCCCCC      ++++++++   ++++++++      IIIIIIIIII
       CCC::::::::::::C  ++++++++++       ++++++++++  I::::::::I
     CC:::::::::::::::C ++++++++++         ++++++++++ I::::::::I
    C:::::CCCCCCCC::::C +++++++++    ++     +++++++++ II::::::II
   C:::::C       CCCCCC +++++++     +++++     +++++++   I::::I
  C:::::C                +++++     +++++++     +++++    I::::I
  C:::::C                ++++                   ++++    I::::I
  C:::::C                 ++                     ++     I::::I
  C:::::C                  +   +++++++++++++++   +      I::::I
  C:::::C                    +++++++++++++++++++        I::::I
  C:::::C                     +++++++++++++++++         I::::I
   C:::::C       CCCCCC        +++++++++++++++          I::::I
    C:::::CCCCCCCC::::C         +++++++++++++         II::::::II
     CC:::::::::::::::C           +++++++++           I::::::::I
       CCC::::::::::::C             +++++             I::::::::I
          CCCCCCCCCCCCC               ++              IIIIIIIIII

                      Cybersecurity AI (CAI), vX.Y.Z
                          Bug bounty-ready AI

CAI>
```

### Các Lệnh CLI Cơ bản
- `/help` - Hiển thị trợ giúp
- `/agent` - Liệt kê tất cả agents có sẵn
- `/model` - Thay đổi mô hình AI
- `/config` - Hiển thị cấu hình
- `/history` - Xem lịch sử
- `/compact` - Nén lịch sử
- `/graph` - Hiển thị đồ thị
- `/memory` - Quản lý bộ nhớ
- `/mcp load` - Tải MCP server
- `/mcp add` - Thêm công cụ MCP vào agent
- `/load` - Tải log JSONL vào context
- `Ctrl+C` (2 lần) - Tương tác với agent

### Ví dụ Sử dụng

#### 1. Tạo Agent Cơ bản
```python
from cai.sdk.agents import Agent, Runner, OpenAIChatCompletionsModel
import os
from openai import AsyncOpenAI
from dotenv import load_dotenv
load_dotenv()

agent = Agent(
    name="Custom Agent",
    instructions="""You are a Cybersecurity expert Leader""",
    model=OpenAIChatCompletionsModel(
        model=os.getenv('CAI_MODEL', "openai/gpt-4o"),
        openai_client=AsyncOpenAI(),
    )
)

message = "Tell me about recursion in programming."
result = await Runner.run(agent, message)
```

#### 2. Agent với Tools
```python
from cai.tools.reconnaissance.exec_code import execute_code
from cai.tools.reconnaissance.generic_linux_command import generic_linux_command

agent = Agent(
    name="Security Agent",
    instructions="""You are a Cybersecurity expert""",
    tools=[
        generic_linux_command,
        execute_code
    ],
    model=OpenAIChatCompletionsModel(
        model=os.getenv('CAI_MODEL', "openai/gpt-4o"),
        openai_client=AsyncOpenAI(),
    )
)
```

#### 3. Agent với Handoffs
```python
flag_discriminator = Agent(
    name="Flag discriminator",
    description="Agent focused on extracting the flag",
    instructions="You are an agent tailored to extract the flag from output.",
    model=OpenAIChatCompletionsModel(
        model=os.getenv('CAI_MODEL', "qwen2.5:14b"),
        openai_client=AsyncOpenAI(),
    )
)

ctf_agent = Agent(
    name="CTF agent",
    description="Agent focused on conquering security challenges",
    instructions="You are a Cybersecurity expert Leader facing a CTF",
    tools=[execute_cli_command],
    model=OpenAIChatCompletionsModel(
        model=os.getenv('CAI_MODEL', "qwen2.5:14b"),
        openai_client=AsyncOpenAI(),
    ),
    handoffs=[flag_discriminator]
)
```

---

## TÁC ĐỘNG VÀ THÀNH TỰU

### Thành tích Thi đấu
- Top 90 Tây Ban Nha trên HackTheBox (5 ngày)
- Top 50 Tây Ban Nha trên HackTheBox (6 ngày)
- Top 30 Tây Ban Nha trên HackTheBox (7 ngày)
- Top 500 Thế giới trên HackTheBox (7 ngày)
- Top 1 (AIs) Thế giới trong HTB "Human vs AI" CTF
- Top 1 Tây Ban Nha trong HTB "Human vs AI" CTF
- Top 20 Thế giới trong HTB "Human vs AI" CTF
- Giải $750 từ HTB CTF
- Giải $2,500 từ Mistral AI Robotics Hackathon

### Tác động Nghiên cứu
- Tiên phong LLM-powered AI Security với PentestGPT
- Thành lập lĩnh vực nghiên cứu "Cybersecurity AI"
- **6 bài báo và báo cáo kỹ thuật** được công bố
- Cải thiện hiệu suất **3,600× so với pentester con người**
- Phát hiện lỗ hổng **CVSS 4.3-7.5** trong hệ thống production
- Dân chủ hóa nghiên cứu lỗ hổng dựa trên AI
- Đánh giá có hệ thống các mô hình ngôn ngữ lớn
- Thiết lập các mức độ tự động trong an ninh mạng
- Đóng góp framework phòng thủ toàn diện chống prompt injection

### Các Nghiên cứu Xuất bản
1. **CAI: An Open, Bug Bounty-Ready Cybersecurity AI** (arXiv:2504.06017)
2. **The Dangerous Gap Between Automation and Autonomy** (arXiv:2506.23592)
3. **CAI Fluency: A Framework for Cybersecurity AI Fluency** (arXiv:2508.13588)
4. **Hacking the AI Hackers via Prompt Injection** (arXiv:2508.21669)
5. **Humanoid Robots as Attack Vectors** (arXiv:2509.14139)
6. **The Cybersecurity of a Humanoid Robot** (arXiv:2509.14096)

### Case Studies
1. **Ecoforest Heat Pumps (OT)**: Phát hiện lỗ hổng nghiêm trọng cho phép truy cập từ xa không được phép
2. **Mobile Industrial Robots - MiR (Robotics)**: Kiểm tra bảo mật qua tấn công tiêm tin nhắn ROS tự động
3. **Mercado Libre (IT/Web)**: Phát hiện lỗ hổng API qua tấn công liệt kê tự động
4. **MQTT Broker (OT)**: Phát hiện lỗ hổng nghiêm trọng trong broker MQTT

---

## CẤU TRÚC DỰ ÁN

### Thư mục Chính
```
cai/
├── src/cai/                    # Mã nguồn chính
│   ├── agents/                 # Triển khai Agent
│   │   ├── patterns/          # Các mẫu agent
│   │   └── meta/              # Meta agents
│   ├── internal/              # Chức năng nội bộ CAI
│   │   └── components/        # Các thành phần
│   ├── prompts/               # Database Prompt
│   │   └── core/              # Prompts cốt lõi
│   ├── repl/                  # CLI và lệnh
│   │   ├── commands/          # Lệnh REPL
│   │   └── ui/                # Giao diện người dùng
│   ├── tools/                 # Công cụ agent
│   │   ├── reconnaissance/    # Công cụ trinh sát
│   │   ├── exploitation/      # Công cụ khai thác
│   │   ├── privilege_scalation/ # Leo thang đặc quyền
│   │   ├── network/           # Công cụ mạng
│   │   ├── command_and_control/ # C&C
│   │   ├── misc/              # Công cụ khác
│   │   └── others/            # Công cụ bổ sung
│   └── sdk/                   # CAI SDK
├── tools/                     # Công cụ bổ sung
├── tests/                     # Test suite
├── docs/                      # Tài liệu
├── examples/                  # Ví dụ
├── benchmarks/                # Benchmarks
├── fluency/                   # Tài liệu CAI Fluency
└── media/                     # Media files
```

### File Quan trọng
- `src/cai/__init__.py` - Entry point chính
- `src/cai/cli.py` - CLI entry point
- `src/cai/core.py` - Core logic
- `src/cai/util.py` - Utility functions
- `pyproject.toml` - Cấu hình dự án
- `.env.example` - Mẫu cấu hình
- `README.md` - Tài liệu chính

---

## TÀI LIỆU VÀ HỌC TẬP

### CAI Fluency - Chương trình Học tập
CAI cung cấp chương trình học tập toàn diện:

| Episode | Nội dung | Link |
|---------|----------|------|
| **Episode 0** | What is CAI? - Giới thiệu CAI | YouTube |
| **Episode 1** | The CAI Framework - Tầm nhìn & Đạo đức | YouTube |
| **Episode 2** | From Zero to Cyber Hero - Hướng dẫn cho người mới | YouTube |
| **Episode 3** | Vibe-Hacking Tutorial - Hack đầu tiên | YouTube |
| **Episode 4** | Intro ReAct - Tiến hóa của LLMs | YouTube |
| **Episode 5** | CAI on CTF challenges - CTF với CAI | YouTube |

### Tài liệu Kỹ thuật
1. **Installation Guide** (`docs/cai_installation.md`)
2. **Quickstart** (`docs/cai_quickstart.md`)
3. **Architecture** (`docs/cai_architecture.md`)
4. **Guardrails** (`docs/guardrails.md`)
5. **Prompt Injection** (`docs/cai_prompt_injection.md`)
6. **FAQ** (`docs/cai_faq.md`)
7. **Development** (`docs/cai_development.md`)

### Ví dụ Code
Thư mục `examples/` chứa 71+ ví dụ Python về:
- Tạo agents cơ bản
- Sử dụng tools
- Handoffs và patterns
- Multi-agent systems
- CTF challenges
- Security assessments

---

## PHÁT TRIỂN

### Yêu cầu Môi trường
- Python ≥ 3.9
- Git
- Virtual environment

### Cài đặt cho Developer
```bash
git clone https://github.com/aliasrobotics/cai
cd cai
python3.12 -m venv cai_env
source cai_env/bin/activate
pip install -e .
```

### Pre-commit Hooks
```bash
pip install pre-commit
pre-commit run --all-files
```

### Testing
```bash
pytest
pytest-asyncio
```

### Công cụ Phát triển
- **mypy**: Type checking
- **ruff**: Linting và formatting
- **pytest**: Testing framework
- **coverage**: Code coverage
- **mkdocs**: Documentation

### VS Code Dev Container
CAI cung cấp môi trường phát triển VS Code đầy đủ

---

## GIẤY PHÉP VÀ SỬ DỤNG

### Cấu trúc Giấy phép Kép

#### 1. MIT License (Thành phần mã nguồn mở)
- Áp dụng cho code từ openai/openai-agents-python
- Tìm trong thư mục `src/cai/agents`
- File: `LICENSE-MIT`

#### 2. Research-Use License (Bổ sung Proprietary)
- Áp dụng cho tất cả bổ sung và sửa đổi bởi Alias Robotics
- **Miễn phí** cho nghiên cứu và học thuật
- **Cấm** sử dụng thương mại mà không có giấy phép
- Liên hệ: https://aliasrobotics.com

### Cách thức Giấy phép Hoạt động
- ✅ **Miễn phí** cho nghiên cứu
- ✅ **Miễn phí** cho học thuật
- ✅ **Miễn phí** cho đánh giá bảo mật cá nhân
- ⚠️ **Yêu cầu giấy phép thương mại** cho:
  - Dịch vụ pentesting thương mại
  - Sử dụng trong sản xuất
  - Triển khai doanh nghiệp

---

## CAI PRO - PHIÊN BẢN CHUYÊN NGHIỆP

### Tính năng CAI PRO
- **Unlimited alias1 tokens**: Không giới hạn token
- **Zero refusals**: AI không giới hạn
- **Beats GPT-5**: Vượt GPT-5 trong benchmark CTF
- **Professional support**: Hỗ trợ chuyên nghiệp
- **European data sovereignty**: Chủ quyền dữ liệu EU
- **Giá**: €350/tháng

### So sánh Community vs PRO

| Tính năng | Community | PRO |
|-----------|-----------|-----|
| Giá | Miễn phí | €350/tháng |
| Models | 300+ | 300+ + alias1 |
| Tokens | Giới hạn theo API | Unlimited alias1 |
| Support | Community | Professional |
| Use case | Research/Learning | Enterprise/Production |

---

## THU THẬP DỮ LIỆU SỬ DỤNG

### Mục đích
CAI thu thập dữ liệu sử dụng để:
- Cải thiện độ chính xác phát hiện
- Hiểu cách framework được sử dụng
- Ưu tiên tính năng mới
- Xuất bản nghiên cứu bảo mật mở

### Dữ liệu được Thu thập
- Thông tin hệ thống cơ bản (OS, Python version)
- Username và IP
- Patterns sử dụng công cụ
- Metrics hiệu suất
- Tương tác mô hình và thống kê token

### Cơ sở Pháp lý
- Art. 6 (1)(f) GDPR
- Lợi ích hợp pháp trong việc duy trì công cụ bảo mật
- Art. 89 safeguards cho nghiên cứu

### Tắt Thu thập Dữ liệu
```bash
CAI_TELEMETRY=False cai
```

**Lưu ý**: CAI khuyến khích giữ telemetry để đóng góp cho nghiên cứu

---

## NGUYÊN TẮC ĐẠO ĐỨC

### Tại sao Mã nguồn Mở?
1. **Dân chủ hóa Cybersecurity AI**: Công cụ AI tiên tiến phải tiếp cận được với toàn bộ cộng đồng
2. **Minh bạch về Khả năng AI**: Cung cấp benchmark minh bạch về khả năng thực sự của AI

### Nguyên tắc Cốt lõi
- **Cybersecurity oriented**: Thiết kế đặc biệt cho use cases an ninh mạng
- **Open source, miễn phí cho nghiên cứu**
- **Lightweight**: Nhanh và dễ sử dụng
- **Modular**: Thiết kế agent-centric
- **Tool-integration**: Dễ dàng tích hợp công cụ
- **Logging và tracing**: Tích hợp sẵn với Phoenix
- **Multi-Model Support**: 300+ models được hỗ trợ

### Cảnh báo và Miễn trừ Trách nhiệm
⚠️ **QUAN TRỌNG**:
- CAI đang trong phát triển tích cực
- KHÔNG sử dụng cho cybercrime
- KHÔNG can thiệp trái phép vào hệ thống
- Chỉ sử dụng cho pentest hợp pháp
- Tuân thủ luật pháp địa phương

---

## HỖ TRỢ VÀ CỘNG ĐỒNG

### Liên hệ
- **Email nghiên cứu**: research@aliasrobotics.com
- **Website**: https://aliasrobotics.com
- **Discord**: https://discord.gg/fnUFcTaQAC
- **GitHub**: https://github.com/aliasrobotics/cai

### Hợp tác Học thuật
CAI hỗ trợ:
- Dự án nghiên cứu PhD
- Nghiên cứu benchmarking học thuật
- Sáng kiến giáo dục bảo mật
- Đóng góp mã nguồn mở từ phòng lab nghiên cứu

### Đóng góp
Đóng góp được hoan nghênh qua:
- Pull requests
- Bug reports
- Feature requests
- Documentation improvements
- Case studies

---

## ROADMAP VÀ TƯƠNG LAI

### Dự báo 2028
**"Đến năm 2028, các công cụ kiểm tra bảo mật dựa trên AI sẽ vượt số lượng pentester con người"**

### Tầm nhìn
- Tăng cường khả năng con người với AI
- Làm cho công nghệ AI bảo mật tiên tiến dễ tiếp cận
- Duy trì transparency và open source
- Xây dựng cộng đồng bảo mật mạnh mẽ

### Các Alternatives Closed-source
CAI theo dõi các sáng kiến closed-source:
- Autonomous Cyber
- CrackenAGI
- ETHIACK
- Horizon3
- Irregular
- Và nhiều hơn nữa...

**Lập trường CAI**: Closed-source là lãng phí tài nguyên và nỗ lực trùng lặp

---

## FAQ - CÂU HỎI THƯỜNG GẶP

### 1. OLLAMA báo lỗi 404?
Sử dụng:
```bash
OLLAMA_API_BASE=http://IP:PORT/v1
```

### 2. Làm sao xóa Python cache?
```bash
find . -name "*.pyc" -delete && find . -name "__pycache__" -delete
```

### 3. Có thể mở rộng khả năng CAI bằng log trước đó?
Có, sử dụng lệnh `/load`:
```bash
CAI>/load logs/cai_20250408_111856.jsonl
```

### 4. Làm sao thay đổi model khi CAI đang chạy?
Sử dụng lệnh `/model`

### 5. Làm sao liệt kê tất cả agents?
Sử dụng lệnh `/agent`

### 6. Làm sao tương tác với agent?
Nhấn `Ctrl+C` hai lần

### 7. Trace toàn bộ execution như thế nào?
Đặt `CAI_TRACING=true` trong file `.env`

---

## KẾT LUẬN

### Tóm tắt
**Cybersecurity AI (CAI)** là một framework mã nguồn mở mạnh mẽ và toàn diện cho việc xây dựng và triển khai các giải pháp an ninh mạng dựa trên AI. Với hơn 300 mô hình AI được hỗ trợ, kiến trúc agent linh hoạt, và các công cụ bảo mật tích hợp sẵn, CAI đang dẫn đầu trong việc dân chủ hóa công nghệ AI an ninh mạng.

### Điểm Mạnh Chính
1. ✅ **Mã nguồn mở và miễn phí** cho nghiên cứu
2. ✅ **Hỗ trợ 300+ mô hình AI**
3. ✅ **Kiến trúc mô-đun linh hoạt**
4. ✅ **Công cụ bảo mật tích hợp**
5. ✅ **Được chứng minh trong thực tế** (CTFs, bug bounties)
6. ✅ **Cộng đồng và hỗ trợ mạnh**
7. ✅ **Tài liệu phong phú**
8. ✅ **Nghiên cứu khoa học vững chắc**

### Phù hợp cho
- 🎯 Security researchers
- 🎯 Ethical hackers
- 🎯 Penetration testers
- 🎯 Security students
- 🎯 Academic researchers
- 🎯 Bug bounty hunters
- 🎯 IT professionals
- 🎯 Security teams

### Bắt đầu Ngay
```bash
pip install cai-framework
cai
```

### Citation
Nếu sử dụng CAI trong nghiên cứu, vui lòng trích dẫn:
```bibtex
@misc{mayoralvilches2025caiopenbugbountyready,
    title={CAI: An Open, Bug Bounty-Ready Cybersecurity AI},
    author={Víctor Mayoral-Vilches and others},
    year={2025},
    eprint={2504.06017},
    archivePrefix={arXiv},
    url={https://arxiv.org/abs/2504.06017},
}
```

---

## PHỤ LỤC

### A. Cấu trúc File Chi tiết
```
/home/runner/work/cai/cai/
├── .devcontainer/          # Dev container config
├── .github/                # GitHub workflows
├── benchmarks/             # Benchmarks
├── ci/                     # CI/CD scripts
├── docs/                   # Documentation
├── examples/               # 71+ Python examples
├── fluency/                # CAI Fluency materials
├── media/                  # Images and videos
├── src/cai/               # Main source (5,610 lines)
├── tests/                  # Test suite
├── tools/                  # Additional tools (6 files)
├── pyproject.toml         # Project config
├── README.md              # Main documentation
├── LICENSE                # License info
├── LICENSE-MIT            # MIT License
├── DISCLAIMER             # Disclaimer
├── .env.example           # Environment template
└── pricing.json           # Pricing info
```

### B. Dependencies Chính
- openai==1.75.0
- litellm[proxy]>=1.63.7
- pydantic>=2.10
- rich>=13.9.4
- prompt_toolkit>=3.0.39
- phoenix (tracing)
- matplotlib, pandas, numpy (visualization)
- paramiko (SSH)
- flask (web)
- networkx (graphs)

### C. Thống kê Dự án
- **Tổng dòng code**: ~5,610 dòng Python (src/cai)
- **Số tools**: 6 file
- **Số examples**: 71+ file
- **Số test**: 40+ test files
- **Số docs**: 30+ markdown files
- **Phiên bản**: 0.5.5
- **Python**: ≥3.9
- **License**: Dual (MIT + Proprietary)

---

**Báo cáo này được tạo vào**: 2025-10-19  
**Phiên bản CAI**: 0.5.5  
**Tác giả báo cáo**: Copilot AI Agent  
**Ngôn ngữ**: Tiếng Việt

---

*Để biết thêm thông tin chi tiết, vui lòng tham khảo tài liệu chính tại README.md và thư mục docs/*
