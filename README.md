# Scheduling Service

# Agenda e Disponibilidade

Domínio responsável por gerenciar os horários de atendimento dos profissionais e determinar quais períodos podem ser disponibilizados para agendamento no **Marketplace para Serviços de Beleza**.

## 1. Visão geral

O domínio Agenda e Disponibilidade permite que profissionais configurem seus horários de atendimento, visualizem sua agenda e bloqueiem períodos nos quais não poderão receber clientes.

A partir dessas informações, o sistema determina os horários disponíveis para cada serviço, considerando sua duração e os compromissos existentes.

Seu principal objetivo é garantir uma gestão organizada da agenda, evitando conflitos e disponibilizando informações confiáveis para o processo de agendamento.

## 2. Objetivos

- Permitir a configuração dos dias e horários de atendimento.
- Permitir a consulta da agenda do profissional.
- Permitir o bloqueio de períodos específicos.
- Calcular a disponibilidade considerando a duração dos serviços.
- Impedir a disponibilização de horários incompatíveis com compromissos existentes.
- Fornecer informações de disponibilidade ao domínio de Agendamentos.

## 3. Escopo funcional

### 3.1 Configuração de horários

O profissional poderá definir os dias da semana e os horários em que está disponível para atender clientes.

O sistema deverá validar os intervalos informados e utilizar essas configurações como base para calcular a disponibilidade.

### 3.2 Consulta da agenda

O profissional poderá consultar sua agenda por data, identificando:

- Horários disponíveis.
- Horários ocupados por agendamentos.
- Períodos bloqueados.

As informações exibidas deverão refletir os registros válidos da agenda.

### 3.3 Bloqueio de horários

O profissional poderá bloquear períodos para compromissos pessoais, pausas ou outras atividades.

Os períodos bloqueados não poderão ser oferecidos para novos agendamentos.

Caso um bloqueio ou uma alteração de disponibilidade entre em conflito com um agendamento existente, o sistema deverá informar o conflito e impedir uma alteração incompatível sem tratamento explícito.

### 3.4 Consulta de disponibilidade

O sistema deverá disponibilizar os horários compatíveis com a contratação de um serviço, considerando:

- Os dias e horários de atendimento do profissional.
- Os períodos bloqueados.
- Os agendamentos existentes.
- A duração do serviço selecionado.
- A inexistência de conflitos no intervalo solicitado.

A disponibilidade consultada representa uma possibilidade de agendamento. A reserva efetiva e sua confirmação são responsabilidades do domínio de Agendamentos.

## 4. Histórias de usuário

| ID | História | Prioridade |
|---|---|---|
| US-AGE-01 | Como profissional, quero definir meus dias e horários de atendimento para informar quando posso receber clientes. | Must |
| US-AGE-02 | Como profissional, quero visualizar meus horários disponíveis e ocupados para organizar meus atendimentos. | Must |
| US-AGE-03 | Como profissional, quero bloquear períodos da minha agenda para reservar tempo para outras atividades. | Must |
| US-AGE-04 | Como cliente, quero consultar os horários disponíveis de um profissional para determinado serviço para escolher um momento conveniente. | Must |
| US-AGE-05 | Como profissional, quero que a duração dos serviços seja considerada na agenda para evitar sobreposição entre atendimentos. | Must |
| US-AGE-06 | Como profissional, quero que o sistema valide alterações na agenda para evitar conflitos com compromissos existentes. | Must |

## 5. Regras de negócio

| ID | Regra |
|---|---|
| RB-07 | Um mesmo horário não poderá ser reservado simultaneamente para atendimentos incompatíveis. |
| RB-08 | Um agendamento somente poderá ocorrer dentro da disponibilidade válida do profissional. |
| RB-09 | A duração do serviço deverá ocupar o período correspondente na agenda. |
| RB-10 | O cancelamento deverá liberar o horário quando aplicável. |
| RB-11 | Alterações na disponibilidade não poderão criar conflitos silenciosos com agendamentos existentes. |

### Regras complementares

- Horários bloqueados ou ocupados não deverão ser apresentados como livres.
- A duração completa do serviço deverá caber no intervalo disponível.
- A disponibilidade deverá ser validada novamente no momento da tentativa de reserva, evitando que uma consulta anterior seja considerada garantia de disponibilidade.
- Alterações na agenda deverão preservar a integridade dos agendamentos existentes.
- O cancelamento e a liberação efetiva do horário deverão respeitar o estado do agendamento e as regras da plataforma.

## 6. Relação com outros domínios

Este domínio integra o núcleo operacional do marketplace e depende de informações mantidas por outros domínios.

| Domínio | Relação |
|---|---|
| Identidade e Acesso | Identifica o profissional autorizado a administrar a própria agenda. |
| Perfis e Profissionais | Fornece a identificação e a situação do profissional. |
| Catálogo de Serviços | Fornece a duração do serviço necessária para calcular os intervalos disponíveis. |
| Agendamentos | Consulta a disponibilidade e informa os compromissos que ocupam a agenda. |

### Fluxo simplificado

1. O profissional configura seus horários de atendimento.
2. O profissional cadastra bloqueios quando necessário.
3. O sistema considera os agendamentos existentes.
4. O cliente consulta a disponibilidade para um serviço.
5. O domínio de Agendamentos valida novamente o horário escolhido antes de registrar a reserva.
6. Após a criação, alteração ou cancelamento de um agendamento, a disponibilidade é atualizada conforme as regras aplicáveis.

## 7. Critérios de aceitação gerais

O domínio será considerado funcional quando:

- O profissional conseguir configurar seus horários de atendimento.
- O profissional conseguir consultar a própria agenda.
- O profissional conseguir bloquear períodos válidos.
- O sistema identificar horários ocupados e bloqueados.
- A duração do serviço for considerada no cálculo da disponibilidade.
- O sistema impedir conflitos incompatíveis.
- Alterações na agenda não sobrescreverem silenciosamente agendamentos existentes.
- O domínio de Agendamentos conseguir consultar e validar a disponibilidade.

## 8. Fora do escopo

Não são responsabilidades diretas deste domínio:

- Cadastro e autenticação de usuários.
- Cadastro e manutenção dos perfis profissionais.
- Cadastro e manutenção de serviços, preços e durações.
- Criação e gerenciamento completo do ciclo de vida dos agendamentos.
- Processamento de pagamentos e reembolsos.
- Notificações aos clientes e profissionais.
- Indicadores financeiros e relatórios avançados.

Essas funcionalidades pertencem a outros domínios, embora possam utilizar ou fornecer informações necessárias à agenda.

## 9. Decisões pendentes

Antes da implementação, deverão ser definidos:

- A antecedência mínima permitida para agendamentos.
- O período máximo futuro que poderá ser consultado.
- A granularidade dos horários oferecidos, como intervalos de 5, 10, 15 ou 30 minutos.
- O tratamento de pausas e intervalos dentro do expediente.
- As regras para alterações de disponibilidade que afetem agendamentos futuros.
- O comportamento da agenda diante de cancelamentos e não comparecimentos.
- O fuso horário utilizado para armazenar e apresentar os horários.
- A estratégia técnica para evitar reservas concorrentes do mesmo período.

Essas decisões devem ser registradas como regras de negócio ou decisões arquiteturais, conforme sua natureza.

## 10. Organização e implementação

A implementação deverá manter separadas as regras de disponibilidade e os mecanismos utilizados para persistir, consultar ou expor os dados.

Independentemente da tecnologia adotada, o domínio deverá preservar a consistência dos horários e evitar que consultas desatualizadas resultem em reservas incompatíveis.

A organização interna do código, as interfaces de integração, os modelos de persistência e os endpoints deverão ser definidos durante o planejamento técnico do repositório.

## 11. Objetivo da entrega

Ao concluir este domínio, a plataforma deverá possuir uma base confiável para gerenciar a disponibilidade dos profissionais e permitir que o domínio de Agendamentos ofereça horários compatíveis com a agenda e a duração dos serviços.

**Resultado esperado:** profissionais organizam seus horários, clientes consultam disponibilidades válidas e o sistema protege a integridade da agenda.