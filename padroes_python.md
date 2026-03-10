# 📌 ISSUE #4 — Configurar Padrões de Código Python

> 🎯 **Objetivo:** Instalar e configurar as 3 ferramentas de qualidade de código do backend Python, garantindo que todo código escrito siga os mesmos padrões, evite erros e seja legível.

---

## 🧠 Conceito: Por que precisamos dessas ferramentas?

Imagine que você abre o projeto daqui 6 meses para fazer manutenção. Sem padrões, o código fica assim:

```python
# SEM padrões — bagunça total 😱
def calcular(x,y,z):
    resultado=x+y+z
    return resultado
import os  # import no lugar errado
def outra_funcao( a,b ):
    return a*b
```

```python
# COM padrões — limpo e profissional 😎
import os

def calcular(x: int, y: int, z: int) -> int:
    resultado = x + y + z
    return resultado

def outra_funcao(a: int, b: int) -> int:
    return a * b
```

---

## 🛠️ As 3 Ferramentas

| Ferramenta | O que faz | Analogia simples |
|---|---|---|
| **ruff** | Encontra problemas no código | "Revisor que aponta erros" |
| **black** | Formata o código automaticamente | "Arruma a casa sozinho" |
| **mypy** | Verifica se os tipos de dados estão corretos | "Confere se você passou string onde esperava número" |

---

## 📁 Onde ficam os arquivos de configuração?

Todas as configurações Python ficam dentro de `services/api/`. A estrutura que vamos criar:

```
services/api/
├── pyproject.toml    ← configuração central (ruff + black + mypy)
└── ...
```

> 💡 **O que é `pyproject.toml`?** É o arquivo padrão moderno do Python para centralizar todas as configurações de ferramentas em um único lugar. Substitui vários arquivos separados (`setup.cfg`, `.flake8`, `mypy.ini`, etc.).

---

## ✅ Tasks Detalhadas — Passo a Passo

---

### ☑️ Tasks 1, 2 e 3 — Criar o `pyproject.toml`

Este é o arquivo mais importante desta issue. Ele configura o `ruff`, o `black` e o `mypy` de uma só vez.

Crie o arquivo em `services/api/pyproject.toml`:

```toml name=services/api/pyproject.toml
# ============================================================
# NutriSaaS — services/api/pyproject.toml
# Configuração central de ferramentas Python
# ============================================================

[tool.ruff]
# Versão mínima do Python alvo
target-version = "py311"

# Tamanho máximo de linha (mesmo do black)
line-length = 88

# Diretórios a ignorar
exclude = [
    ".git",
    ".venv",
    "__pycache__",
    "alembic/versions/",
    "build",
    "dist",
]

[tool.ruff.lint]
# Regras ativas:
# E = erros de estilo (pycodestyle)
# F = erros lógicos (pyflakes)
# I = ordenação de imports (isort)
# N = convenções de nomenclatura (pep8-naming)
# UP = sugestões de modernização (pyupgrade)
# B = bugs comuns (flake8-bugbear)
# S = segurança básica (flake8-bandit)
# ANN = type annotations obrigatórias
select = ["E", "F", "I", "N", "UP", "B", "S", "ANN"]

# Regras ignoradas (com justificativa)
ignore = [
    "ANN101", # Não exigir anotação de tipo em 'self'
    "ANN102", # Não exigir anotação de tipo em 'cls'
    "S101",   # Permitir uso de 'assert' em testes
    "B008",   # Permitir chamadas de função em default args (padrão FastAPI)
]

# Regras que podem ser corrigidas automaticamente
fixable = ["ALL"]

[tool.ruff.lint.per-file-ignores]
# Em arquivos de teste, relaxar algumas regras
"tests/**/*.py" = ["S101", "ANN", "N802"]
# No arquivo de migrations do alembic, ignorar tudo
"alembic/**/*.py" = ["ALL"]

[tool.ruff.lint.isort]
# Organização de imports: stdlib → third-party → local
known-first-party = ["app"]
force-sort-within-sections = true

# ============================================================
# BLACK — Formatador de código
# ============================================================
[tool.black]
target-version = ["py311"]
line-length = 88
# Strings em aspas duplas (padrão black)
skip-string-normalization = false
# Arquivos a ignorar
exclude = '''
/(
    \.git
  | \.venv
  | __pycache__
  | alembic/versions
  | build
  | dist
)/
'''

# ============================================================
# MYPY — Verificador de tipos estáticos
# ============================================================
[tool.mypy]
python_version = "3.11"

# Rigor de verificação
strict = false           # não usar strict total (muito restritivo no início)
disallow_untyped_defs = true      # funções precisam ter type hints
disallow_incomplete_defs = true   # type hints precisam ser completos
check_untyped_defs = true         # verifica funções sem anotação também
no_implicit_optional = true       # força Optional[X] explícito
warn_return_any = true            # avisa quando retorno é 'Any'
warn_unused_ignores = true        # avisa sobre '# type: ignore' desnecessários
warn_unreachable = true           # avisa sobre código inacessível

# Diretório raiz da aplicação
mypy_path = "."

# Módulos sem stubs de tipo (ignorar erros de import)
[[tool.mypy.overrides]]
module = [
    "aio_pika.*",
    "alembic.*",
    "chatwoot.*",
]
ignore_missing_imports = true

# ============================================================
# PYTEST — Configuração de testes
# ============================================================
[tool.pytest.ini_options]
testpaths = ["tests"]
asyncio_mode = "auto"
python_files = ["test_*.py", "*_test.py"]
python_classes = ["Test*"]
python_functions = ["test_*"]
# Mostrar prints durante testes com -s
addopts = "-v --tb=short"

# ============================================================
# COVERAGE — Cobertura de testes
# ============================================================
[tool.coverage.run]
source = ["app"]
omit = [
    "tests/*",
    "alembic/*",
    "*/__init__.py",
]

[tool.coverage.report]
# Falhar se cobertura cair abaixo de 80%
fail_under = 80
show_missing = true
```

---

### ☑️ Task 4 — Criar o `requirements-dev.txt`

As ferramentas de qualidade só são usadas no **desenvolvimento** — não precisam ir para produção. Crie este arquivo em `services/api/requirements-dev.txt`:

```text name=services/api/requirements-dev.txt
# ============================================================
# NutriSaaS — Dependências de Desenvolvimento
# NÃO instalar em produção
# ============================================================

# Linting e formatação
ruff==0.4.4
black==24.4.2

# Type checking
mypy==1.10.0

# Stubs de tipos para bibliotecas comuns
types-redis==4.6.0.20240417
types-requests==2.32.0.20240521

# Testes
pytest==8.2.1
pytest-asyncio==0.23.7
pytest-cov==5.0.0
httpx==0.27.0           # cliente HTTP para testes da API FastAPI

# Pre-commit
pre-commit==3.7.1
```

---

### ☑️ Task 4 — Configurar o pre-commit hook de lint e format

Crie o arquivo `.pre-commit-config.yaml` na **raiz do projeto** (não dentro de `services/api/`):

```yaml name=.pre-commit-config.yaml
# ============================================================
# NutriSaaS — Pre-commit Hooks
# Roda automaticamente antes de cada git commit
# ============================================================
# Instalação: pip install pre-commit && pre-commit install
# Executar manualmente: pre-commit run --all-files
# ============================================================

repos:
  # Hooks básicos de qualidade de arquivo
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.6.0
    hooks:
      - id: trailing-whitespace       # Remove espaços no final das linhas
      - id: end-of-file-fixer         # Garante linha vazia no final
      - id: check-yaml                # Valida sintaxe de arquivos YAML
      - id: check-json                # Valida sintaxe de arquivos JSON
      - id: check-toml                # Valida sintaxe de arquivos TOML
      - id: check-merge-conflict      # Bloqueia commit com markers de merge conflict
      - id: check-added-large-files   # Bloqueia arquivos grandes (>500KB)
        args: ['--maxkb=500']
      - id: detect-private-key        # Detecta chaves privadas acidentais

  # Ruff — linting Python (muito mais rápido que flake8)
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.4.4
    hooks:
      - id: ruff
        args: [--fix]                 # Corrige automaticamente o que for possível
        files: ^services/api/
      - id: ruff-format               # Também formata (substitui black no pre-commit)
        files: ^services/api/

  # Black — formatação Python (garantia extra)
  - repo: https://github.com/psf/black
    rev: 24.4.2
    hooks:
      - id: black
        language_version: python3.11
        files: ^services/api/
```

---

## 🖥️ Como instalar e usar no dia a dia

Execute estes comandos no terminal, dentro de `services/api/`:

```bash
# 1. Crie e ative o ambiente virtual Python
python -m venv .venv

# No Mac/Linux:
source .venv/bin/activate

# No Windows:
.venv\Scripts\activate

# 2. Instale as dependências de desenvolvimento
pip install -r requirements-dev.txt

# 3. Volte para a raiz do projeto e instale o pre-commit
cd ../..
pip install pre-commit
pre-commit install
# ✅ Agora o pre-commit vai rodar automaticamente em todo git commit!
```

### Comandos para rodar manualmente:

```bash
# Verificar problemas no código Python
cd services/api
ruff check .

# Corrigir automaticamente o que o ruff consegue
ruff check . --fix

# Formatar o código com black
black .

# Verificar tipos com mypy
mypy app/

# Rodar todos os pre-commit hooks em todos os arquivos
cd ../..
pre-commit run --all-files
```

---

## 🧪 Testando que funciona

Crie um arquivo de teste temporário para ver as ferramentas em ação:

```python name=services/api/test_qualidade.py
# Arquivo temporário para testar as ferramentas
# (apague depois de testar!)

import os  # import não utilizado — ruff vai reclamar!

def soma(a,b):  # sem espaços e sem type hints — ruff e mypy vão reclamar!
    return a+b
```

```bash
# Ruff vai encontrar os problemas:
cd services/api
ruff check test_qualidade.py
# Output esperado:
# test_qualidade.py:3:8: F401 [*] `os` imported but unused
# test_qualidade.py:5:1: ANN201 Missing return type annotation
# test_qualidade.py:5:10: ANN001 Missing type annotation for function argument `a`
# ...

# Black vai reformatar:
black test_qualidade.py

# Apague o arquivo de teste:
rm test_qualidade.py
```

---

## 📋 Checklist Final da Issue #4

```
⬜ pyproject.toml criado em services/api/
⬜ requirements-dev.txt criado em services/api/
⬜ .pre-commit-config.yaml criado na raiz do projeto
⬜ Ambiente virtual criado (.venv) — não vai para o Git!
⬜ pre-commit instalado e hooks ativos
⬜ ruff, black e mypy instalados e testados
⬜ Commit: feat(tooling): configura ruff, black e mypy para Python
```

---

## 🎯 Fluxo completo desta issue

```
services/api/
├── pyproject.toml          ← CRIAR (configura ruff + black + mypy)
├── requirements-dev.txt    ← CRIAR (dependências de dev)
└── .venv/                  ← CRIAR localmente (no .gitignore!)

.pre-commit-config.yaml     ← CRIAR na raiz do projeto
```

---

> 💡 **Dica importante:** O arquivo `.venv/` **nunca** vai para o Git — está no `.gitignore` que criamos. Cada desenvolvedor cria o seu próprio ambiente local.
