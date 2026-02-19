---
title: "Windows에서 Claude Desktop MCP + Obsidian 연동하기"
date: 2026-02-19
tags: [til, mcp, obsidian, claude]
category: DevOps
status: complete
---

# Windows에서 Claude Desktop MCP + Obsidian 연동하기

## 🎯 한 줄 요약
> Windows Store 버전 Claude Desktop은 config 경로가 일반 설치와 다르다!

## 📝 학습 내용

### 구성 요소
- Obsidian + Local REST API 플러그인 (포트 27124)
- obsidian-mcp 패키지 (npm 글로벌 설치)
- Claude Desktop (Windows Store 버전)

### 핵심 설정 (claude_desktop_config.json)
```json
{
  "mcpServers": {
    "obsidian": {
      "command": "C:\\nvm4w\\nodejs\\node.exe",
      "args": ["C:\\nvm4w\\nodejs\\node_modules\\obsidian-mcp\\build\\main.js", "D:\\JungSun\\Obsidian_Vault"],
      "env": {
        "OBSIDIAN_API_KEY": "your-api-key",
        "OBSIDIAN_HOST": "https://127.0.0.1:27124",
        "NODE_TLS_REJECT_UNAUTHORIZED": "0"
      }
    }
  }
}
```

## 💡 핵심 포인트 (삽질 기록)

- **npx는 안 된다**: nvm4w 환경에서 npx.ps1은 Claude Desktop이 실행 불가. `node.exe`로 직접 실행해야 함
- **dist가 아니라 build**: `obsidian-mcp`의 진입점은 `dist/main.js`가 아니라 `build/main.js`
- **Store 버전 config 경로**: `%APPDATA%\Claude\`가 아니라 `C:\Users\{user}\AppData\Local\Packages\Claude_pzs8sxrjxfjjc\LocalCache\Roaming\Claude\`
- **볼트 경로에 특수문자 금지**: 한글, 이모지 등이 포함되면 MCP 서버가 경로 인식 실패
- **HTTPS 자체 서명 인증서**: `NODE_TLS_REJECT_UNAUTHORIZED=0` 환경변수 필요

## 🔗 관련 링크
- [obsidian-mcp npm](https://www.npmjs.com/package/obsidian-mcp)
- [Obsidian Local REST API](https://github.com/coddingtonbear/obsidian-local-rest-api)
- [MCP 공식 문서](https://modelcontextprotocol.io)

## 🤔 추가 학습이 필요한 부분
- RAG 파이프라인 구축 (Obsidian 노트 기반)
- MCP 서버 커스터마이징

## 📌 연결 노트
- [[START HERE]]
