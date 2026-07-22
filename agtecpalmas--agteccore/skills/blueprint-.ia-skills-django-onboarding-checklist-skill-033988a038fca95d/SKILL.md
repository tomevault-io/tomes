---
name: django-onboarding-checklist
description: Realizar checklist de validação inicial de um novo projeto Django gerado pelo template CookieCutter. Verificar configuração de INSTALLED_APPS, AUTH_USER_MODEL, banco de dados, variáveis de ambiente, migrations pendentes e conformidade com as regras do .ia/. Usar quando um novo projeto for gerado a partir do template ou quando houver necessidade de validar a saúde inicial do projeto. Use when this capability is needed.
metadata:
  author: AgtecPalmas
---

# Objetivo

Validar que o projeto Django gerado pelo template está corretamente configurado e pronto para uso. Este checklist deve ser executado pelo agente de IA ao atuar em um novo projeto gerado por este template.

# Fluxo

## 1. Verificações obrigatórias

Executar as seguintes verificações na ordem indicada:

### 1.1. Estrutura de apps

Confirmar que `INSTALLED_APPS` em `settings.py` contém:
- `django.contrib.auth` (built-in)
- `django.contrib.contenttypes` (built-in)
- `rest_framework` (DRF)
- Apps próprios do projeto

### 1.2. Modelo de usuário

Verificar `AUTH_USER_MODEL` em `settings.py`:
- Se não declarado: usar padrão `django.contrib.auth.User`
- Se declarado: confirmar que aponta para um modelo válido

### 1.3. Configurações de banco

Verificar `DATABASES` em `settings.py`:
- Confirmar engine PostgreSQL
- Verificar variáveis de ambiente para conexão
- Confirmar que `pgvector` ou extensões necessárias estão disponíveis se aplicável

### 1.4. Variáveis de ambiente

Verificar `.env.example`:
- Contém todas as variáveis obrigatórias declaradas
- Nenhuma credencial real está hardcoded

### 1.5. Migrations

Verificar estado de migrations:
```bash
rtk python manage.py showmigrations
```
- Confirmar que não há migrations pendentes não aplicadas
- Se houver, documentar

### 1.6. Conformidade com .ia/

Verificar que o projeto segue as regras documentadas:
- Estrutura de apps em monólito modular
- Uso de `core.Base` para models com soft-delete
- Separação entre views e serviços (regras de negócio em services.py)

## 2. Checklist de validação

Marcar cada item como `OK`, `FALHA` ou `N/A`:

| Item | Status | Observação |
|------|--------|------------|
| INSTALLED_APPS correto | | |
| AUTH_USER_MODEL configurado | | |
| DATABASES com PostgreSQL | | |
| .env.example existente e completo | | |
| Migrations aplicadas | | |
| Soft-delete via core.Base | | |
| Separation of concerns (views vs services) | | |
| Type hints em services/helpers | | |
| Testes configurados | | |

## 3. Reporte de hallazgos

Se qualquer item estiver como `FALHA`:
1. Documentar o finding
2. Propor resolução
3. Se aplicável, abrir task de correção

# Regras obrigatórias

- Não alterar código-fonte durante o checklist — apenas ler e reportar
- Marcar itens como `N/A` apenas se não forem aplicáveis ao projeto específico
- Reportar findings mesmo se o projeto parecer funcional — hallazgos menores evitam problemas futuros

# Checklist de qualidade

- Todos os 9 itens de verificação foram marcados
- Findings de `FALHA` têm proposta de resolução
- O checklist foi executado e o resultado foi documentado

# Referências locais

- `.ia/docs/architecture/overview.md`
- `.ia/docs/architecture/system-architecture.md`
- `.ia/docs/architecture/modules.md`
- `.ia/docs/guides/constraints.md`
- `.ia/docs/guides/patterns.md`

---
> Source: [AgtecPalmas/AgtecCore](https://github.com/AgtecPalmas/AgtecCore) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
