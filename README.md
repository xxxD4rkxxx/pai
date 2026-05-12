# SkillForge Pro - Instruções de Configuração

## 📁 Estrutura do Projeto

```
skillforge-pro/
├── public/
│   ├── index.html          # HTML principal
│   ├── css/
│   │   └── styles.css     # Estilos CSS
│   └── js/
│       ├── firebase-config.js  # Configuração Firebase
│       ├── database.js         # Camada de dados Firestore
│       ├── engine.js           # Lógica de negócio
│       └── app.js              # Inicialização
├── firebase.json           # Configuração Hosting
├── .firebaserc            # Projeto Firebase
└── README.md              # Este arquivo
```

---

## 🚀 Passo a Passo para Configuração

### 1. Instale o Firebase CLI

```bash
npm install -g firebase-tools
```

### 2. Configure o Firebase

#### A) Acesse o [Firebase Console](https://console.firebase.google.com/)

#### B) Crie um novo projeto
- Clique em "Adicionar projeto"
- Dê um nome ao projeto
- Ative o Google Analytics (opcional)

#### C) Ative o Firestore Database
1. No menu lateral, clique em "Firestore Database"
2. Clique em "Criar banco de dados"
3. Escolha a localização
4. **IMPORTANTE**: Escolha "Modo de teste" (permite leitura/escrita sem autenticação)
   - Later você pode configurar regras de segurança

#### D) Obtenha as configurações
1. No menu lateral, clique no ícone de engrenagem (Configuração)
2. Role até "Seus apps" e clique no ícone "</>" (Web)
3. Register app (dê um nome se quiser)
4. Copie o objeto `firebaseConfig` gerado

### 3. Configure o Código

Abra o arquivo `public/js/firebase-config.js` e substitua os valores:

```javascript
const firebaseConfig = {
    apiKey: "SUA_API_KEY_AQUI",
    authDomain: "seu-projeto.firebaseapp.com",
    projectId: "seu-projeto",
    storageBucket: "seu-projeto.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123"
};
```

### 4. Configure o Projeto ID

Abra o arquivo `.firebaserc` e substitua:

```json
{
  "projects": {
    "default": "seu-projeto-aqui"
  }
}
```

---

## 🖥️ Comandos para Desenvolvimento

### Iniciar servidor local
```bash
firebase serve
```
Acesse: http://localhost:5000

### Deploy (publicar na web)
```bash
firebase deploy
```

---

## 🔒 Regras de Segurança (Firestore)

Para desenvolvimento (sem autenticação), use:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if true;
    }
  }
}
```

Para produção, substitua `if true` por regras de autenticação.

---

## 📊 Estrutura de Dados Firestore

```
users/
└── default_user/
    ├── config/
    │   ├── metaDiaria: 90
    │   ├── retencaoBonus: 0
    │   └── retencaoBase: 0.5
    ├── daily_history/
    │   └── "2026-05-12": 120
    └── modules/
        └── "1715500000000": { id, nome, nivel, concluido, ... }
```

---

## 🎯 Funcionalidades

- ✅ Meta diária de estudo (em minutos)
- ✅ Registro de minutos estudados por dia
- ✅ Consistência semanal (últimos 7 dias)
- ✅ Módulos de estudo (criar, listar, concluir)
- ✅ Sistema de retenção e nível global
- ✅ Simular teste de proficiência
- ✅ Persistência em nuvem (Firestore)
- ✅ Interface moderna com glassmorphism

---

## 🐛 Troubleshooting

### Erro: "Failed to load resource"
- Verifique se os caminhos dos arquivos JS/CSS estão corretos no index.html

### Erro: "PERMISSION_DENIED" no Firestore
- Verifique as regras do Firestore (veja acima)

### Erro: "Firebase app not initialized"
- Verifique se o firebase-config.js está sendo carregado antes dos outros scripts

---

## 📝 Notas

- Sem autenticação: os dados são públicos (qualquer um pode ver/editar)
- Para adicionar autenticação: será necessário criar sistema de login
- Dados offline: o Firestore funciona offline (sincroniza quando online)

---

Feito com ❤️ por SkillForge Pro