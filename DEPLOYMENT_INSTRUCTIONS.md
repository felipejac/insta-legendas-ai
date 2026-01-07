# 🚀 Instruções de Deploy - Instagram Caption Generator

## Opção 1: Deploy Rápido do Seu PC (Recomendado)

### Pré-requisitos:
- Node.js instalado (versão 18+)
- Firebase CLI instalado: `npm install -g firebase-tools`
- Acesso ao seu projeto Firebase

### Passos:

1. **Clone o repositório** na sua máquina:
```bash
git clone https://github.com/felipejac/insta-legendas-ai.git
cd insta-legendas-ai
```

2. **Faça login no Firebase**:
```bash
firebase login
```
(Isso abrirá uma janela do navegador para você autenticar)

3. **Deploy completo** (Hosting + Cloud Functions):
```bash
firebase deploy
```

Isso irá:
- Fazer deploy do site (public/index.html) para Firebase Hosting
- Fazer deploy do Cloud Function para geração de legendas
- Tudo levará cerca de 2-3 minutos

4. **Teste a aplicação**:
- Acesse: https://insta-legendas-ai.web.app/
- Digite uma descrição de foto
- Clique em "Gerar Legenda"
- A legenda deve aparecer em alguns segundos!

## Estrutura do Projeto

```
insta-legendas-ai/
├── public/
│   └── index.html          # Frontend (UI do app)
├── functions/
│   ├── index.js            # Cloud Function (API backend)
│   └── package.json        # Dependências das funções
├── firebase.json           # Configuração Firebase
├── .firebaserc            # Projeto Firebase
└── .gitignore
```

## Arquitetura

```
┌─────────────────┐
│   Browser       │
│ (index.html)    │
└────────┬────────┘
         │ HTTP Request
         │ {prompt: "..."}
         ▼
┌─────────────────────────────┐
│  Firebase Hosting           │
│  + Cloud Function           │
│  (generateCaption)          │
└────────┬────────────────────┘
         │ API Call
         │ (via server, sem CORS)
         ▼
┌─────────────────┐
│  Google Gemini  │
│      API        │
└─────────────────┘
```

## Troubleshooting

### "Error: Failed to authenticate"
- Execute: `firebase login` primeiro
- Verifique se tem acesso ao projeto: `firebase projects:list`

### "Cloud Function deployment fails"
- Verifique o arquivo `functions/index.js`
- Execute: `firebase functions:log` para ver erros

### "App não gera legendas"
- Verifique se o Cloud Function foi deployed corretamente
- Confirme que a API Key do Google está definida
- Abra o console do navegador (F12) para ver erros

## Support

Repositório: https://github.com/felipejac/insta-legendas-ai
Issues: https://github.com/felipejac/insta-legendas-ai/issues
