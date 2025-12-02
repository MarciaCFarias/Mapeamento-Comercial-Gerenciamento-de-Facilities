# **Processos – TO BE**

## **Fluxo TO BE – Visão Geral das Duas Frentes**
O processo robotizado contempla duas frentes principais:

---

# **1ª Frente — Monitoramento de Inconsistências no Cartão de Ponto (TO BE)**

## **1. Detalhamento do Fluxo TO BE**

### **1.1 Verificar Período de Execução**
- Acessar parâmetros de calendário (DE/PARA ou sistema).
- Verificar se o período está em “bloqueio/fechamento”.
- **Se bloqueado:** registrar em banco de dados + log.
- **Se não bloqueado:** seguir para captura da planilha de Faturamento.

### **1.2 Acessar Planilha de Faturamento**
- Acessar diretório no Google Drive.
- Abrir planilha “Faturamento AA/AA”.
- Selecionar aba do mês vigente.
- Padronizar nomenclaturas das abas e diretórios.

### **1.3 Capturar Dados**
- Período, Situação e Observações.
- Validar se existe dado para processamento:
  - **Se houver:** seguir para Monitorar Cartão de Ponto.
  - **Se não houver:** registrar log e encerrar.

### **1.4 Monitorar Cartão de Ponto**

#### **Acessar Sistema via API**
- Acessar espelho de ponto via integração API.
- Verificar necessidade de matrícula para captura de PDF (ponto de atenção).

#### **Consultar Colaboradores**
- Filtrar solicitações via API:
  - Centro de Custo  
  - Período  
  - Tipo de Inconsistência = *Não registrado*  
  - Status Ajuste = *Pendente*

#### **Validar Dados**
- Validar horas, intervalos, regras de aceite e recusa.
- Confirmar ranges específicos para horários.

#### **Atualizar Ponto (Aceite/Recusa)**
- Via API, registrar aceite ou recusa.
- Incluir observações padronizadas.
- Preparar para verificação de horários específicos.

#### **Verificar Horários Específicos**
- Identificar horários = “00:00”.
- Enviar para etapa de Ajuste em Lote.

#### **Ajustar Horários em Lote**
- Via API, ajustar todos os pontos com horários específicos.

---

# **2ª Frente — Atestados (TO BE)**

## **2. Detalhamento do Fluxo TO BE**

### **2.1 Acessar Sistema e Identificar Atestados**
- Via API do Sistema, acessar área de atendimento de Atestados.
- Receber anexos enviados pelo colaborador.

### **2.2 Leitura via IA**
- IA identificará:
  - Tipo de atestado  
  - Datas  
  - CID  
  - Observações do médico  
  - Horário  
  - Protocolos
- Atenção: documentos sensíveis → processamento PRD requer segurança e regras específicas.

### **2.3 Atualizar Ponto dos Atestados**

#### **Acessar Sistema do Ponto**
- Verificar se já existe lançamento.
- Identificar possíveis duplicidades de matrícula entre empresas.

#### **Acessar Sistema de Cadastro do Colaborador**
- Filtrar dados do colaborador.
- Excluir lançamentos anteriores (quando aplicável).

#### **Realizar Novo Lançamento**
- Incluir informações validadas no Nexti.
- Registrar CID conforme regras internas.
- Preencher observações padronizadas.
- Informar protocolo gerado.

#### **Retornar Atendimento**
- Finalizar atendimento via sistema Nexti.

---

# **Melhorias Identificadas no Processo**
- Padronização dos campos da planilha de faturamento.
- Execução **totalmente diária** (incluindo fins de semana).
- Automatização via API reduz falhas manuais e elimina retrabalho.
- IA para extração e classificação de atestados.
- Logs automáticos e rastreáveis para auditoria.
- Redução de risco de inconsistências por validações automáticas.
- Controle centralizado em banco de dados do robô.

---

# **Pontos de Atenção / Exceções**
- Necessidade de **liberação de credenciais** para acesso via API em ambiente PRD.
- Bloqueio mensal do sistema pode impedir atualização do ponto.
- Matrículas duplicadas entre empresas diferentes (impacto nas validações).
- Variedade de tipos de atestados: Médico, ASO, Defesa Civil.
- Dependência da documentação das APIs (ainda pendente pelo cliente).
- Custos das APIs são responsabilidade do cliente.
- Processos sensíveis tratados por IA devem seguir normas de segurança.

---

# **Quadro de KPI – Indicadores Sugeridos**

| KPI | Descrição | Periodicidade | Objetivo |
|-----|-----------|---------------|----------|
| **Tempo Médio de Processamento do Ciclo** | Tempo total para concluir monitoramento e ajustes | Diário | Reduzir 30–50% pós-RPA |
| **% de Solicitações Processadas sem Intervenção Humana** | Automação efetiva do processo | Diário | Atingir > 90% |
| **Taxa de Erros Identificados pela Validação Automática** | Inconsistências detectadas pelo robô | Diário | Monitorar qualidade do ponto |
| **Tempo Médio de Atendimento de Atestados** | Desde recebimento até atualização | Diário | Reduzir em 60% |
| **Volume Diário de Ajustes/Atestados Processados** | Para monitorar capacidade | Diário | Indicador de carga operacional |
| **Taxa de Reprocessamento** | Casos que precisaram ser refeitos | Semanal | Atingir < 5% |

---

# **Observações Gerais**
- Todas as premissas técnicas devem ser validadas pela **Arquitetura** antes do desenvolvimento.
- A documentação detalhada dos campos das APIs dos sistemas é imprescindível.
- A IA deve ser específica e treinada para documentos sensíveis (compliance).
- O processo mapeado considera execução no ambiente de produção desde o desenvolvimento (PRD).

