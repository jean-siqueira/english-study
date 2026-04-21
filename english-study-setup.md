# 🎯 English Study Directory — Setup Completo

## 1. ESTRUTURA DE DIRETÓRIOS

```
~/english-study/
│
├── anki/
│   ├── exports/          # Exportações do Anki (.apkg, .txt)
│   └── analysis/         # Análises dos seus cards (erros frequentes, etc.)
│
├── journal/              # Diário de estudos diário (Obsidian)
│   ├── daily/            # Uma nota por dia (YYYY-MM-DD.md)
│   └── weekly/           # Resumo semanal (YYYY-WXX.md)
│
├── corrections/          # Textos corrigidos pelo assistente
│   ├── writings/         # Seus textos originais
│   └── feedback/         # Feedback e versão corrigida
│
├── vocabulary/           # Vocabulário novo descoberto
│   ├── by-topic/         # Agrupado por tema (work, daily, etc.)
│   └── new-cards.md      # Fila de cards a adicionar no Anki
│
├── progress/
│   ├── tracker.md        # Registro diário de métricas
│   └── milestones.md     # Marcos alcançados
│
└── README.md             # Visão geral do projeto
```

---

## 2. SCRIPT DE SETUP (rode no terminal)

```bash
# Criar estrutura de diretórios
mkdir -p ~/english-study/{anki/{exports,analysis},journal/{daily,weekly},corrections/{writings,feedback},vocabulary/by-topic,progress}

# Entrar no diretório
cd ~/english-study

# Inicializar repositório Git
git init

# Criar .gitignore
cat > .gitignore << 'EOF'
*.apkg
*.anki2
*.anki21
.obsidian/workspace
.obsidian/workspace.json
.obsidian/cache
*.log
EOF

# Criar README inicial
cat > README.md << 'EOF'
# English Study Journal

**Started:** $(date +%Y-%m-%d)
**Goal:** Fluency for work/career
**Method:** Mairo Vergara (CIMV) + Anki + Daily output practice

## Current Status
- Anki cards: ~3000
- Backlog: reducing
- Daily study: 30 min

## Routine
| Block     | Time   | Activity              |
|-----------|--------|-----------------------|
| Anki      | 10 min | Spaced repetition     |
| Listening | 10 min | CIMV / podcasts       |
| Output    | 10 min | Writing / speaking    |
EOF

# Criar tracker de progresso
cat > progress/tracker.md << 'EOF'
# Progress Tracker

| Date | Anki Cards | Study Time | Streak | Notes |
|------|-----------|------------|--------|-------|
| YYYY-MM-DD | 0 | 0 min | 1 | First day back! |
EOF

# Criar arquivo de milestones
cat > progress/milestones.md << 'EOF'
# Milestones 🏆

- [ ] 7 days streak
- [ ] 30 days streak
- [ ] Anki backlog zerado
- [ ] Primeiro texto corrigido sem erros graves
- [ ] Primeira conversa de trabalho em inglês
- [ ] Assistir 1 episódio de série sem legendas
- [ ] Participar de reunião em inglês com confiança
EOF

# Criar template de nota diária
mkdir -p journal/templates
cat > journal/templates/daily-template.md << 'EOF'
# Daily Log — {{date}}

## ✅ Today's session
- **Anki cards reviewed:** 
- **Study time:** 
- **Streak:** 

## 📖 What I studied
- 

## 🆕 New vocabulary
- 

## ✍️ Output (writing/speaking practice)


## 🔁 Send to assistant for correction?
- [ ] Yes
- [ ] No

## 💬 Notes / Reflections

EOF

# Primeiro commit
git add .
git commit -m "feat: initialize english study directory"

echo "✅ Diretório criado com sucesso em ~/english-study"
echo "👉 Agora abra a pasta no Obsidian como vault!"
```

---

## 3. CONFIGURAR OBSIDIAN

1. Abra o Obsidian
2. **Open folder as vault** → selecione `~/english-study`
3. Instale os plugins recomendados:
   - **Calendar** — visualizar dias de estudo
   - **Dataview** — gerar relatórios automáticos do tracker
   - **Templater** — usar o template de nota diária automaticamente

### Query Dataview para ver seu progresso (cole em qualquer nota):
```dataview
TABLE anki-cards AS "Anki", study-time AS "Tempo", streak AS "Streak"
FROM "journal/daily"
SORT file.name DESC
LIMIT 7
```

---

## 4. EXPORTAR ANKI PARA ANÁLISE

Para eu analisar seus cards, exporte assim:

1. No Anki: **File → Export**
2. Escolha: **Notes in Plain Text (.txt)**
3. Marque: **Include tags**
4. Salve em: `~/english-study/anki/exports/`
5. Me envie o arquivo aqui no chat

---

## 5. PROMPT DO ASSISTENTE (use no início de cada conversa)

Cole este prompt quando iniciar uma nova sessão comigo:

```
You are my English learning assistant. Here is my context:

**Profile:**
- Level: Intermediate (understand well, but freeze when speaking/writing)
- Goal: Fluency for work and career
- Method: Mairo Vergara (CIMV) + Anki spaced repetition
- Daily time: 30 minutes
- Tools: Anki (~3000 cards), Obsidian vault at ~/english-study, Git versioning

**My current focus:**
- Reducing Anki backlog (was 314 cards overdue)
- Building daily study streak
- Developing active output (writing and speaking)

**What I need from you today:**
[FILL IN: e.g. "correct my writing", "simulate a work meeting", 
"create new Anki cards", "analyze my export", "conversation practice"]

**Today's metrics (optional):**
- Anki cards reviewed: 
- Streak day: 
- Study time: 
```

---

## 6. GIT — COMANDOS DO DIA A DIA

```bash
# Ao final de cada sessão de estudo:
cd ~/english-study
git add .
git commit -m "study: day $(date +%Y-%m-%d) — X cards, Y min"

# Ver histórico de commits (= histórico de estudos)
git log --oneline

# Ver quantos dias você commitou no mês
git log --after="2025-03-01" --oneline | wc -l
```

> 💡 **Dica:** cada commit vira uma prova concreta do seu progresso. Depois de 30 dias, rode `git log --oneline` e veja sua consistência visualmente.

---

## 7. FLUXO SEMANAL RECOMENDADO

```
Segunda a Sexta:
  → Abrir Obsidian → criar nota do dia com template
  → Anki (10 min)
  → Mairo / listening (10 min)  
  → Escrever output e colar aqui pra correção (10 min)
  → Preencher tracker.md
  → git commit

Domingo:
  → Criar nota semanal em journal/weekly/
  → Exportar Anki e me enviar para análise
  → Revisar milestones alcançados
  → Planejar foco da semana seguinte
```
