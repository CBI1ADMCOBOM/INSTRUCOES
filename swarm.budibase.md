# COBOM Hub - Informativo de Utilização das Ferramentas

Documento oficial de orientação para uso dos aplicativos internos do COBOM.

## Sumário

- [1. Visão Geral](#1-visão-geral)
- [2. Acesso Rápido](#2-acesso-rápido)
- [3. Aplicativo: Controle de Viaturas](#3-aplicativo-controle-de-viaturas)
- [4. Aplicativo: Atendimento em Modo de Contingência](#4-aplicativo-atendimento-em-modo-de-contingência)
- [5. Aplicativo: GeoLoc193](#5-aplicativo-geoloc193)

---

## 1. Visão Geral

Estão disponíveis para uso interno no COBOM três aplicativos:

1. **Controle de Viaturas**  
Ferramenta para uso dos Controladores com objetivo de realizar a gestão completa da frota de viaturas de serviço sob seu controle.

2. **Atendimento em modo de Contingência**  
Sistema interno offline que os bombeiros do COBOM poderão utilizar para cadastrar e controlar ocorrências nas situações em que o SIOPM esteja inoperante.

3. **GeoLoc193**  
Ferramenta para os atendentes obterem a localização do solicitante em tempo real durante o atendimento, quando não for possível pela ligação.

---

## 2. Acesso Rápido

- Entrada principal: `https://cobom.cbi1.org`
- Aplicativo Controle de Viaturas: `https://cobom.cbi1.org/apps/controle-viaturas`
- Aplicativo Contingência Atendente: `https://cobom.cbi1.org/apps/contingencia-atendente`
- Aplicativo Contingência Controlador: `https://cobom.cbi1.org/apps/contingencia-controlador`
- Aplicativo GeoLoc193 para o Atendente: `https://cobom.cbi1.org/apps/geoloc193/atendente`
- Aplicativo GeoLoc193 para o Solicitante: `https://sos193.org`

Requisito de acesso:
- Estas ferramentas rodam em rede interna do COBOM, portanto sem dependência de internet e sem exposição para o público externo. exceto o https://sos193.org que é dominio público e precisa ser acessado pelo solicitante para compartilhar a localização da ocorrência.

---

## 3. Aplicativo: Controle de Viaturas

### 3.1 Objetivo

Permitir ao Controlador manter visão operacional e atualização em tempo real das viaturas sob seu GB, com rastreabilidade das ações.

### 3.2 Quando usar

- Início de turno para conferência das Estações e VIaturas
- Durante o atendimento para atualização de status de viaturas
- Troca de turno para passagem de situação operacional

### 3.3 Instruções de Uso

1. **Acesso ao sistema**
- Entrar no Workspace (`cobom.cbi1.org`).
- Realizar login conforme as credenciais de cada controlador (disponível na supervisão)
- Clicar em **Controle de Viaturas**.

2. **Login e validação de perfil**
- Confirmar no topo da tela se o usuário logado está correto.
- Verificar se o perfil está com permissão operacional (edição) quando necessário.

3. **Configuração inicial do turno**
- Selecionar o **GB** correto.
- Identificar o **Controlador (RE)** ativo no turno.
- Confirmar que painel e filtros foram atualizados para a área correta.

4. **Navegação principal**
- Usar busca por prefixo, estação, cidade ou texto livre.
- Aplicar filtros por status, modalidade e critérios operacionais.
- Abrir cards de estação e viaturas para detalhamento.

5. **Funções operacionais disponíveis**
- Atualizar status da viatura (ex.: disponível, local, QTI, regressando, reserva, baixado).
- Registrar e editar observações operacionais.
- Atualizar `QSA Rádio` e `QSA Zello`.
- Marcar teste realizado.
- Indicar DEJEM quando aplicável.
- Transferir viatura entre estações.
- Ativar ou desativar viatura na estação.
- Configurar e desfazer revezamento.
- Inserir, editar e consultar anotações de serviço.
- Consultar logs para rastreabilidade de ações.

6. **Rotina durante o atendimento**
- Atualizar status imediatamente após cada mudança operacional.
- Evitar backlog de atualização para o fim do turno.
- Registrar somente observações objetivas e úteis ao próximo operador.

7. **Finalização do uso**
- Revisar pendências de viaturas sem status coerente.
- Conferir se houve registro das principais ocorrências do turno.
- Garantir que troca de controlador (se houver) foi realizada.
- Encerrar sessão conforme protocolo local.

### 3.4 Resultado esperado

- Painel atualizado com situação real da frota
- Histórico confiável para auditoria e continuidade entre turnos

---

## 4. Aplicativo: Atendimento em Modo de Contingência

### 4.1 Objetivo

Garantir continuidade do cadastro e controle de ocorrências quando o SIOPM estiver indisponível.

### 4.2 Quando usar

- Indisponibilidade total do SIOPM
- Instabilidade prolongada com impacto no atendimento
- Procedimento determinado pelo comando operacional

### 4.3 Instruções de Uso

1. **Acesso ao sistema**
- Entrar no Workspace (`/workspace`).
- Clicar em **Contingência**.
- Em caso de redirecionamento, efetuar login e retornar ao app.

2. **Validação antes de iniciar**
- Confirmar com a chefia/controle que o cenário é de contingência ativa.
- Confirmar operador responsável no turno.

3. **Abertura de ocorrência**
- Clicar em **Nova Ocorrência**.
- Preencher os campos mínimos obrigatórios:
  - identificação do chamado;
  - local/endereço;
  - natureza;
  - horário de abertura;
  - dados do solicitante quando disponíveis.

4. **Gestão da ocorrência em andamento**
- Registrar despacho de recursos.
- Atualizar horários relevantes (saída, chegada, desfecho).
- Registrar evolução do atendimento com objetividade.
- Atualizar situação da ocorrência (aberta, em atendimento, finalizada).

5. **Funções disponíveis no app**
- Criar ocorrência.
- Editar dados da ocorrência em andamento.
- Atualizar status operacional da ocorrência.
- Inserir observações cronológicas.
- Consultar ocorrências abertas e encerradas durante o período de contingência.

6. **Encerramento de ocorrência**
- Registrar desfecho final.
- Confirmar campos obrigatórios de fechamento.
- Salvar e validar se a ocorrência foi listada como finalizada.

7. **Finalização do uso no fim da contingência**
- Revisar se todas as ocorrências abertas foram tratadas corretamente.
- Consolidar registros conforme protocolo da unidade para retorno ao SIOPM.
- Encerrar sessão.

### 4.4 Resultado esperado

- Nenhuma ocorrência crítica sem registro
- Continuidade operacional do COBOM durante falha do sistema principal

---

## 5. Aplicativo: GeoLoc193

### 5.1 Objetivo

Apoiar o atendente na obtenção de localização do solicitante em tempo real, especialmente quando o endereço não puder ser confirmado por voz.

### 5.2 Quando usar

- Solicitante sem referência clara de endereço
- Situações de pânico, desorientação ou risco iminente
- Queda de qualidade da ligação com dificuldade de compreensão

### 5.3 Instruções de Uso

1. **Acesso ao sistema**
- Entrar no Workspace (`cobom.cbi1.org`).
- Abrir o aplicativo **GeoLoc193**.
- Se necessário, autenticar com usuário no seguinte padrão: usuário => pa101@cbi1.org senha => atendentepa101 .

2. **Preparação do atendimento**
- Manter chamada ativa com o solicitante.
- Confirmar nome e algum dado mínimo de validação.
- Informar que será feito procedimento de compartilhamento de localização para agilizar o socorro.

3. **Coleta da localização**
- Acionar o fluxo de localização no app.
- Orientar o solicitante a concluir a autorização de compartilhamento acessando no seu navegador a pagina sos193.org.
- Aguardar atualização do ponto no mapa.

4. **Validação da posição obtida**
- Confirmar com o solicitante pontos de referência próximos.
- Verificar coerência da posição no mapa com o relato da ocorrência.
- Quando houver divergência, repetir validação antes do despacho final.

5. **Funções disponíveis no app**
- Obter posição em tempo real do solicitante.
- Visualizar ponto em mapa para apoio ao despacho.
- Apoiar confirmação de rota/referência para equipes em campo.

6. **Uso integrado ao atendimento**
- Repassar localização validada ao operador de despacho.
- Registrar no atendimento que a localização foi obtida via GeoLoc193.
- Manter atualização caso o solicitante esteja em deslocamento.

7. **Finalização do uso**
- Confirmar que a localização final foi transmitida com sucesso.
- Encerrar o fluxo da sessão de localização.
- Encerrar sessão do sistema ao fim do turno, conforme protocolo local.

### 5.4 Resultado esperado

- Redução do tempo de localização da vítima/solicitante
- Maior assertividade no despacho de recursos

---

Última atualização: abril/2026.
