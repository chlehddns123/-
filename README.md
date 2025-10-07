# 🎯 소비 후 일기 (Post-Purchase Diary)

> **AI 감정 분석 기반 소비 기록 서비스**  
> 사용자의 소비 후기를 감정 분석하여, 일기처럼 기록하고 감정 흐름을 시각화하는 웹 애플리케이션입니다.



---------------------------------



 📘 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **프로젝트명** | 소비 후 일기 (Post-Purchase Diary) |
| **개발 기간** | 미정 |
| **참여 인원** | 1명 (본안) |
| **주요 목적** | 소비 후 감정 분석 및 시각 피드백을 통한 자기 인식 향상 |




-------------------------------------------------------------------------




🔍 1. 문제 정의

현대인은 “소비”를 많이 하지만, 소비 이후 반성/성찰의 과정이 거의 없음

돈을 어떻게, 왜 썼는지에 대한 기록이 부족함

소비를 단순한 지출이 아닌 감정·의미의 행위로 분석하고 싶음

💡 핵심 아이디어

“소비” 후 사용자가 짧게 일기를 작성하면,
AI가 감정/소비 유형을 분석하고 “소비 성찰 리포트”를 생성

소비를 단순 기록이 아니라 자기 성찰 콘텐츠로 전환

❤️ 사용자 타겟

20~30대 MZ세대: 소비는 즐기지만 후회가 많은 사용자

자기관리 / 자산관리 / 감정 기록을 선호하는 사람들



------------------------------------------------------------------------




💡 2. 핵심 기능

| 기능명 | 설명 |
|--------|------|
| 🧠 감정 분석 | Gemini API를 통해 소비 후기를 감정별로 분류 |
| 📒 감정 일기 | 날짜별 후기 및 감정 결과 기록 |
| 🎨 AI 일러스트 | 감정 결과에 따라 자동 생성되는 카드형 이미지 |
| 📊 감정 통계 | 감정 비율 및 시간대별 변화 시각화 (Recharts) |
| 💾 데이터 저장 | MongoDB에 사용자별 기록 저장 및 불러오기 |





---=====================================================================================






🧩 3. 기술 스택

### 🌐 Frontend
- React (Vite)
- Styled-Components
- Axios
- Recharts (통계 시각화)
- Lucide-react (아이콘)

⚙️ Backend 9백엔드)
- Node.js (Express)
- MongoDB (Mongoose)
- Gemini API (AI 감정 분석)
- dotenv (환경 변수 관리)



------------------------------





🧠 4. 시스템 아키텍처

```mermaid
graph TD
A[사용자 입력 - 소비 후기] --> B[Gemini 감정 분석 API]
B --> C[감정 결과 DB 저장]
C --> D[AI 이미지 생성]
D --> E[일기 카드 UI 렌더링]
E --> F[통계 시각화]





-----------------------------------------




🎨 5. UI / UX

| 감정    | 색상 코드     | 설명              |
| ----- | --------- | --------------- |
| 😊 행복 | `#FFD966` | 밝고 긍정적인 소비 경험   |
| 😔 슬픔 | `#6FA8DC` | 후회·슬픔이 동반된 소비   |
| 😌 충족 | `#93C47D` | 목표 달성형 소비       |
| 😇 절제 | `#C27BA0` | 소비 자제 및 자기통제 성공 |




-------------------------------------------------------------




🚀 6. 실행 방법
# 1️⃣ 프론트엔드 실행
cd client
npm install
npm start

# 2️⃣ 백엔드 실행
cd server
npm install
npm start


그러면 해당 사이트 으로 접속이 됩니다




__________________________________________________




📁 7. 디렉토리 구조
📦 root
 ┣ 📂 client           # React (Frontend)
 ┃ ┣ 📂 components     # UI 구성 요소
 ┃ ┣ 📂 pages          # 주요 화면
 ┃ ┣ 📂 assets         # 감정별 이미지 / 스타일
 ┃ ┗ 📜 App.jsx
 ┣ 📂 server           # Express (Backend)
 ┃ ┣ 📂 routes         # API 라우터
 ┃ ┣ 📂 models         # MongoDB 스키마
 ┃ ┗ 📜 index.js
 ┣ 📜 .env
 ┣ 📜 README.md
 ┗ 📜 package.json






____________________________________________________________________________________________






🧪 8. AI 감정 분석 프로토타입 (예시 코드)
// frontend/src/api/analyzeEmotion.js
import axios from "axios";

export const analyzeEmotion = async (text) => {
  const response = await axios.post("http://localhost:5000/api/analyze", { text });
  return response.data; // { emotion: "happy", score: 0.87 }
};

// server/routes/analyze.js
import express from "express";
import { GoogleGenerativeAI } from "@google/generative-ai";
import dotenv from "dotenv";
dotenv.config();

const router = express.Router();
const genAI = new GoogleGenerativeAI(process.env.GEMINI_API_KEY);

router.post("/", async (req, res) => {
  const { text } = req.body;
  const result = await genAI.generateText({
    model: "gemini-1.5-flash",
    prompt: `Analyze the emotion of this text in one word: ${text}`,
  });
  res.json({ emotion: result.response.text() });
});

export default router;




__________________________________________________________________________________





🌈 9. 시연 이미지
감정 카드 예시	설명

	행복 소비 예시 = 행복한 이미지

	슬픈 소비 예시 = 슬픈 이미지 

	충족된 소비 예시 = 충족한 이미지




______________________________________________________________________________________



🧾 10. 기대 효과

소비 감정의 패턴화 / 시각화

사용자 자기인식 향상

감정 기반 소비 관리 서비스 모델 가능성 검증

📄 11. 향후 발전 방향

개인 맞춤형 소비 피드백 추천

감정 기반 소비 리포트 월간/주간 자동 생성

Google Calendar / KakaoPay 소비 내역 연동




_________________________________________________________________________________




🌿 마무리 (Conclusion)

이번 프로젝트 **「소비 후 일기」**는 단순한 소비 기록을 넘어,
AI 감정 분석을 통해 **‘나의 소비 패턴을 감정으로 바라보는 경험’**을 제안했습니다.

기획 단계부터 실제 프로토타입 구현까지의 과정을 통해

사용자의 행동 데이터가 어떻게 감정으로 연결될 수 있는가,

그리고 그 감정을 어떻게 시각적으로 표현하고 피드백할 수 있는가
를 고민했습니다.

이번 프로젝트를 통해 우리는

“기술이 인간의 감정을 이해할 수 있을까?”
라는 질문에 한 걸음 다가갔습니다.

앞으로는 AI 모델의 정확도를 높이고,
실제 소비 내역과 연동되는 실용적 감정 리포트 서비스로 확장할 예정입니다.

“모든 소비에는 감정이 있다.
그 감정을 이해할 때, 비로소 현명한 소비가 시작된다.”

























