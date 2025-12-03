# 📌 Requisitos – Oportunidades de Automação

# **1ª Frente — Monitoramento de Inconsistências do Cartão de Ponto**

## **Regras de Negócio**
- Não executar se o período estiver em “bloqueio/fechamento”.
- Só processar CCUs cuja situação esteja válida para operação.
- Solicitações com “Tipo de inconsistência = Não registrado” e “Status = Pendente” devem ser analisadas.
- Regras de aceite/recusa devem seguir faixas de horários pré-estabelecidas.
- Ajustes em lote aplicados apenas quando horários forem “00:00”.

## **Validações Necessárias**
- Validar integridade da planilha e padronização das colunas.
- Validar períodos cruzando planilha × data do ponto.
- Validar matrícula e consistência de dados capturados.
- Validar campos da API: centro de custo, período, horários, tipo de inconsistência.
- Conferir se há dados suficientes para processar antes de iniciar.

## **Saídas Esperadas**
- Log detalhado do ciclo.
- Registro no banco de dados dos dados capturados.
- Atualizações realizadas no ponto (Aceite/Recusa).
- Ajustes em lote processados.
- Alertas de exceção documentados.

## **Critérios de Sucesso**
- Processo concluído sem intervenção humana ≥ 90%.
- Zero erros de atualização indevida no sistema.
- Ajustes em lote executados sempre que aplicáveis.
- Logs completos para auditoria.

---

# **2ª Frente — Atestados**

## **Regras de Negócio**
- Atestados devem ser classificados por tipo (Médico, ASO, Defesa Civil, etc.).
- Identificação automática via IA.
- Validação de CID obrigatória conforme escopo.
- Lançamentos duplicados devem ser removidos antes de incluir novo.
- Protocolo deve ser registrado no atendimento Nexti.

## **Validações Necessárias**
- Validação da autenticidade e leitura do documento via IA.
- Identificação correta da matrícula (existe risco de duplicidade).
- Verificação se existe lançamento prévio.
- Conferência dos campos antes de gravar nos sistemas.
- Conferência de datas, CID e carga horária.

## **Saídas Esperadas**
- Lançamento registrado corretamente no Nexti.
- Registro de protocolo e observações padronizadas.
- Histórico atualizado no banco de dados.
- Retorno automatizado ao colaborador.

## **Critérios de Sucesso**
- 100% dos atestados processados dentro do SLA diário.
- Zero divergências entre os sistemas.
- IA identificando corretamente ≥ 95% dos campos obrigatórios.
- Redução significativa do tempo de atendimento.

