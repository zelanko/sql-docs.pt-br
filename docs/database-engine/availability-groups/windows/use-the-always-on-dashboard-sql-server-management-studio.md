---
title: Usar o painel do grupo de disponibilidade Always On (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
- Availability Groups [SQL Server], dashboard
ms.assetid: c9ba2589-139e-42bc-99e1-94546717c64d
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: c150f329f41098755a47ebd7395ba83d6a33aaa0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66769012"
---
# <a name="use-the-always-on-availability-group-dashboard-sql-server-management-studio"></a>Usar o painel do grupo de disponibilidade Always On (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Os administradores de banco de dados usam o painel do grupo de disponibilidade Always On para obter uma visão rápida da integridade de um grupo de disponibilidade e de suas réplicas de disponibilidade e seus bancos de dados no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Alguns dos usos típicos do painel do grupo de disponibilidade são:  
  
-   Escolhendo uma réplica para um failover manual.    
-   Estimando a perda de dados se você forçar um failover.  
-   Avaliando o desempenho da sincronização de dados.   
-   Avaliando o impacto do desempenho de uma réplica secundária de confirmação síncrona 
  -  O painel fornece estados e indicadores chave de desempenho do grupo de disponibilidade, que permitem tomar decisões operacionais sobre alta disponibilidade usando os tipos de informações a seguir.  
-   Estado de acúmulo da réplica    
-   Modo e estado da sincronização   
-   Perda de dados estimada    
-   Tempo de recuperação estimado (refazer recuperação do atraso)    
-   Detalhes da réplica de banco de dados    
-   Modo e estado da sincronização    
-   Tempo para restauração do log  
  
  
## <a name="prerequisites"></a>Prerequisites  
 Conecte-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (instância de servidor) que hospeda a réplica primária ou secundária de um grupo de disponibilidade.  
  
 
### <a name="permissions"></a>Permissões  
 Requer as permissões CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION.  
  
##  <a name="to-start-the-always-on-dashboard"></a>Para iniciar o painel Always On  
  
1.  No Pesquisador de Objetos, conecte à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na qual você deseja executar o Painel AlwaysOn.  
  
2.  Expanda o nó **Alta Disponibilidade AlwaysOn** , clique com o botão direito do mouse em **Grupos de Disponibilidade** e clique em **Mostrar Painel**.  
  
##  <a name="change-always-on-dashboard-options"></a>Alterar as opções do Painel Always On  
 Você pode usar a caixa de diálogo [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]**Opções** para configurar o comportamento do Painel AlwaysOn do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para atualização e habilitação automática de uma política de AlwaysOn definida automaticamente.  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Para atualizar o painel automaticamente, na caixa de diálogo **Opções** , selecione **Ativar atualização automática**, digite o intervalo de atualização em segundos e o número de vezes que você deseja repetir a conexão.  
  
3.  Para habilitar uma política definida pelo usuário, selecione **Habilitar política AlwaysOn definida pelo usuário**.  
  
##  <a name="availability-group-summary"></a>Resumo do grupo de disponibilidade  
 A tela de grupo de disponibilidade exibe uma linha de resumo para cada grupo de disponibilidade para o qual a instância de servidor conectada hospeda uma réplica. Esse painel exibe as seguintes colunas.  
  
 **Nome do Grupo de Disponibilidade**  
 O nome de um grupo de disponibilidade para o qual a instância local hospeda uma réplica.  
  
 **Instância Primária**  
 O nome da instância do servidor que está hospedando a réplica primária do grupo de disponibilidade.  
  
 **Modo de Failover**  
 Exibe o modo de failover para o qual a réplica está configurada. Os valores possíveis do modo de failover são:  
  
-   **Automático**. Indica que uma ou mais réplicas estão em modo de failover automático.  
  
-   **Manual**. Indica que nenhuma réplica está em modo de failover automático.  
  
 **Problemas**  
 Clique no link **Problemas** para abrir documentação de solução de problemas para determinado problema. Para obter uma lista de todos os problemas da política AlwaysOn, veja [Políticas do AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md).  
  
> [!TIP]  
>  Clique nos títulos das colunas para classificar as informações de grupo de disponibilidade pelo nome do grupo de disponibilidade, a instância primária, o modo de failover ou o Problema.  
  
##  <a name="AvGroupDetails"></a> Detalhes do grupo de disponibilidade  
 As informações de detalhes a seguir são exibidas para o grupo de disponibilidade que você seleciona na tela de resumo:  
  
 **Estado do grupo de disponibilidade**  
 Exibe o estado de integridade do grupo de disponibilidade.  
  
 **Primary instance**  
 O nome da instância do servidor que está hospedando a réplica primária do grupo de disponibilidade.  
  
 **Failover mode**  
 Exibe o modo de failover para o qual a réplica está configurada. Os valores possíveis do modo de failover são:  
  
-   **Automático**. Indica que uma ou mais réplicas estão em modo de failover automático.  
  
-   **Manual**. Indica que nenhuma réplica está em modo de failover automático.  
  
 **Estado do cluster**  
 O nome e o estado do cluster onde a instância do servidor conectado e o grupo de disponibilidade são nós membros.  
  
##  <a name="AvReplicaDetails"></a> Detalhes da réplica de disponibilidade  

Quando conectada à réplica primária, a exibição **Detalhes da réplica de disponibilidade** mostra informações de todas as réplicas do grupo de disponibilidade. Quando conectada a uma réplica secundária, a exibição mostra apenas informações da réplica conectada.  

O painel **Réplica de Disponibilidade** exibe as seguintes colunas:  
  
 **Nome**  
 O nome da instância do servidor que hospeda a réplica de disponibilidade. Essa coluna é mostrada por padrão.  
  
 **Função**  
 Indica a função atual da réplica de disponibilidade, **Primária** ou **Secundária**. Para obter informações sobre as funções do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], confira [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md). Essa coluna é mostrada por padrão.  
  
 **Modo de Failover**  
 Exibe o modo de failover para o qual a réplica está configurada. Os valores possíveis do modo de failover são:  
  
-   **Automático**. Indica que uma ou mais réplicas estão em modo de failover automático.  
  
-   **Manual**. Indica que nenhuma réplica está em modo de failover automático.  
  
 **Estado da Sincronização**  
 Indica se uma réplica secundária está sincronizada no momento com a réplica primária. Essa coluna é mostrada por padrão. Os valores possíveis são:  
  
-   **Não Sincronizado**. Um ou mais bancos de dados na réplica não estão sincronizado ou ainda não foram unidos ao grupo de disponibilidade.  
  
-   **Sincronizando**. Um ou mais bancos de dados na réplica estão sendo sincronizados.  
  
-   **Sincronizado**. Todos os bancos de dados na réplica secundária são sincronizados com os bancos de dados primário correspondentes na réplica primária atual, se houver, ou na réplica primária mais recente.  
  
    > [!NOTE]  
    >  Em modo de desempenho, o banco de dados nunca está no estado sincronizado.  
  
-   **NULL**. Estado desconhecido. Este valor ocorre quando a instância do servidor local não pode se comunicar com o cluster de failover do WSFC (isto é, o nó local não faz parte do quorum do WSFC).  
  
 **Problemas**  
 Lista o nome do problema. Esse valor é mostrado por padrão. Para obter uma lista de todos os problemas da política AlwaysOn, veja [Políticas do AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md).  
  
 **Modo de Disponibilidade**  
 Indica a propriedade de réplica que você define separadamente para cada réplica de disponibilidade. Esse valor é ocultado por padrão. Os valores possíveis são:  
  
-   **Assíncrono**. A réplica secundária nunca é sincronizada com a réplica primária.  
  
-   **Synchronous**. Ao ficar em dia com o banco de dados primário, um banco de dados secundário entra nesse estado e permanece em dia, desde que a sincronização continue para o banco de dados.  
  
 **Modo de Conexão Primário**  
 Indica o modo usado para conexão à réplica primária.  Esse valor é ocultado por padrão.  
  
 **Modo de Conexão Secundário**  
 Indica o modo usado para conexão à réplica secundária.  Esse valor é ocultado por padrão.  
  
 **Estado da Conexão**  
 Indica se uma réplica secundária está conectada atualmente à réplica primária. Essa coluna é ocultada por padrão. Os valores possíveis são:  
  
-   **Desconectado**. Para uma réplica de disponibilidade remota, indica que ela está desconectada da réplica de disponibilidade local. A resposta da réplica local ao estado Desconectado depende de sua função, da seguinte forma:  
  
    -   na réplica primária, se uma réplica secundária estiver desconectada, os bancos de dados secundários serão marcados como **Não Sincronizado** na réplica primária, e a réplica primária esperará que a secundária seja reconectada.  
  
    -   Na réplica secundária, ao detectar que está desconectada, a réplica secundária tentará reconectar-se à réplica primária.  
  
-   **Connected**. Uma réplica de disponibilidade remota que está conectada atualmente à réplica local.  
  
 **Estado Operacional**  
 Indica o estado operacional atual da réplica secundária. Esse valor é ocultado por padrão. Os valores possíveis são:  
  
 **0**. Failover pendente    
 **1**. Pendente    
 **2**. Online    
 **3**. Offline   
 **4**. Falhou    
 **5**. Com falha, sem quorum  
  
 **NULL**. A réplica não é local  
  
 **Número do Último Erro de Conexão.**  
 O número do último erro de conexão.  Esse valor é ocultado por padrão.  
  
 **Descrição do Último Erro de Conexão**  
 A descrição do último erro de conexão.  Esse valor é ocultado por padrão.  
  
 **Carimbo de Data/Hora do Último Erro de Conexão**  
 O carimbo de data/hora do último erro de conexão. Esse valor é ocultado por padrão.  
  
> [!NOTE]  
>  Para obter informações sobre contadores de desempenho para réplicas de disponibilidade, veja [SQL Server, Réplica de Disponibilidade](../../../relational-databases/performance-monitor/sql-server-availability-replica.md).  
  
##  <a name="group-by-availability-group-information"></a>Agrupar por informações do grupo de disponibilidade  
 Para agrupar as informações, clique em **Agrupar por**e selecione uma das opções a seguir:  
  
-   **Réplicas de disponibilidade**    
-   **Bancos de dados de disponibilidade** 
-   **Synchronization state**  
-   **Prontidão de failover**   
-   **Problemas**  
  
 O painel que exibe as informações agrupadas exibe as seguintes colunas:  
  
 **Nome**  
 O nome do banco de dados de disponibilidade. Esse valor é mostrado por padrão.  
  
 **Réplica**  
 O nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica de disponibilidade. Esse valor é mostrado por padrão.  
  
 **Estado da Sincronização**  
 Indica se um banco de dados de disponibilidade está sincronizado no momento com a réplica primária. Esse valor é mostrado por padrão. Os possíveis estados de sincronização são:  
  
-   **Não sincronizando**:  
-   
    -   Para uma função primária, indica que o banco de dados não está pronto para sincronizar seu log de transações com os bancos de dados secundários correspondentes.   
    -   Para um banco de dados secundário, indica que o banco de dados não iniciou a sincronização de log devido a um problema de conexão, está sendo suspenso ou está passando por estados de transição durante a inicialização ou uma troca de função.  
  
-   **Sincronizando**:
- Em uma réplica primária:   
    - Em um banco de dados primário, indica que este banco de dados está pronto para aceitar uma solicitação de exame de um banco de dados secundário.  
    - Em uma réplica secundária, indica que há movimentação de dados ativa em andamento para este banco de dados secundário. 
  
  
-   **Sincronizado**: 
  
    - Para um banco de dados primário, indica se pelo menos um banco de dados secundário é sincronizado.
    - Para um banco de dados secundário, indica se o banco de dados está sincronizado com o banco de dados primário correspondente.  
  
-   **Revertendo**.  
  
     Indica a fase do processo de desfazer em que um banco de dados secundário está obtendo páginas ativamente do banco de dados primário.  
  
    > [!CAUTION]  
    >  Quando um banco de dados está no estado REVERTING, um failover forçado da réplica secundária pode deixar o banco de dados em um estado no qual não pode ser iniciado.  
  
-   **Inicializando**.  
  
     Indica a fase de desfazer em que o log de transações que exigiu que um banco de dados secundário ficasse em dia com o LSN de desfazer está sendo enviado e protegido em uma réplica secundária.  
  
    > [!CAUTION]  
    >  Quando um banco de dados está no estado INITIALIZING, um failover forçado da réplica secundária sempre deixará esse banco de dados em um estado no qual não pode ser iniciado.  
  
 **Failover Readiness**  
 Indica em qual réplica de disponibilidade pode ser feito failover com ou sem perda de dados potencial. Essa coluna é mostrada por padrão. Os valores possíveis são:  
  
-   **Perda de Dados**   
-   **Sem Perda de Dados**  
  
 **Problemas**  
 Lista o nome do problema. Essa coluna é mostrada por padrão. Os valores possíveis são:  
  
-   **Avisos**. Clique para exibir os problemas de limites e avisos.   
-   **Crítico**. Clique para exibir os problemas críticos.  
  
 Para obter uma lista de todos os problemas da política AlwaysOn, veja [Políticas do AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md).  
  
 **Suspenso**  
 Indica se o banco de dados está **Suspenso** ou **Retomado**. Esse valor é ocultado por padrão.  
  
 **Motivo da Suspensão**  
 Indica o motivo do estado de suspensão. Esse valor é ocultado por padrão.  
  
 **Perda de dados estimada (segundos)**  
 Indica a diferença de tempo do último registro de log de transação na réplica primária e na réplica secundária. Se a réplica primária falhar, todos os registros de log de transação dentro da janela de tempo serão perdidos. Esse valor é ocultado por padrão.  
  
 **Tempo de Recuperação estimado (segundos)**  
 Indica o tempo em segundos necessário para refazer o tempo de recuperação do atraso. O *tempo de recuperação do atraso* é o tempo necessário para a réplica secundária ficar em dia com a réplica primária. Esse valor é ocultado por padrão.  
  
 **Desempenho da Sincronização (segundos)**  
 Indica o tempo, em segundos, necessário para a sincronização entre as réplicas primária e a secundária. Esse valor é ocultado por padrão.  
  
 **Tamanho da Fila de Envio de Log (KB)**  
 Indica a quantidade de registros de log nos arquivos de log do banco de dados primário que não foram enviados à réplica de disponibilidade secundária. Esse valor é ocultado por padrão.  
  
 **Taxa de Envio de log (KB/segundo)**  
 Indica a taxa em KB por segundo na qual estão sendo enviados registros de log à réplica secundária. Esse valor é ocultado por padrão.  
  
 **Tamanho da Fila de Restauração (KB)**  
 Indica o número de registros de log nos arquivos de log da réplica secundária que ainda não foram refeitos. Esse valor é ocultado por padrão.  
  
 **Taxa de Restauração (KB/segundo)**  
 Indica a taxa em KB por segundo na qual os registros de log estão sendo refeitos. Esse valor é ocultado por padrão.  
  
 **Taxa de Envio do Fluxo de Arquivos (KB/s)**  
 Indica a taxa do Fluxo de Arquivos, em KB por segundo, na qual as transações estão sendo enviadas à réplica. Esse valor é ocultado por padrão.  
  
 **LSN de Fim de Log**  
 Indica o LSN (número de sequência de log) real que corresponde ao último registro de log no cache de log nas réplicas primária e secundária. Esse valor é ocultado por padrão.  
  
 **LSN de Recuperação**  
 Indica o final do log de transações antes de a réplica gravar outro novo registro de log depois da recuperação ou do failover na réplica primária. Esse valor é ocultado por padrão.  
  
 **LSN de Truncamento**  
 Indica o valor mínimo de truncamento de log para a réplica primária. Esse valor é ocultado por padrão.  
  
 **LSN da Última Confirmação**  
 Indica a LSN real que corresponde ao último registro de confirmação no log de transações. Esse valor é ocultado por padrão.  
  
 **Hora da Última Confirmação**  
 Indica a hora correspondente ao último registro de confirmação. Esse valor é ocultado por padrão.  
  
 **LSN do Último Envio**  
 Indica o ponto até o qual todos os blocos de log foram enviados pela réplica primária. Esse valor é ocultado por padrão.  
  
 **Hora do Último Envio**  
 Indica a hora em que o último bloco de log foi enviado. Esse valor é ocultado por padrão.  
  
 **LSN do Último Recebimento**  
 Indica o ponto até o qual todos os blocos de log foram recebidos pela réplica secundária que hospeda o banco de dados secundário. Esse valor é ocultado por padrão.  
  
 **Hora do Último Recebimento**  
 Indica a hora em que o identificador do bloco de log da última mensagem recebida foi lido na réplica secundária. Esse valor é ocultado por padrão.  
  
 **LSN da Última Proteção**  
 Indica o ponto até o qual todos os registros de log foram liberados para disco na réplica secundária. Esse valor é ocultado por padrão.  
  
 **Hora da Última Proteção**  
 Indica a hora em que o identificador do bloco de log foi recebido para a última LSN de proteção na réplica secundária. Esse valor é ocultado por padrão.  
  
 **LSN da Última Operação de Refazer**  
 Indica a LSN real do registro de log que foi refeito pela última vez na réplica secundária. Esse valor é ocultado por padrão.  
  
 **Hora da Última Operação de Refazer**  
 Indica a hora em que o último registro de log que foi refeito no banco de dados secundário. Esse valor é ocultado por padrão.  
 

   > [!NOTE]  
   >  A maioria dos dados baseia-se em DM hadr_database_replica_states, portanto, algumas restrições podem ser aplicadas. Para obter mais informações, veja [sys.dm_hadr_database_replica_states (Transact-SQL)](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).


## <a name="always-on-availability-group-latency-reports"></a>Relatórios de latência do grupo de disponibilidade Always On
O relatório de latência do grupo de disponibilidade é uma ferramenta interna ao painel de controle de grupo de disponibilidade e está disponível em relatórios do [SQL Server Management Studio versão 17.4](../../../ssms/download-sql-server-management-studio-ssms.md). Esse recurso fornece um relatório fácil de entender que detalha o tempo gasto durante as várias fases do processo de transporte de log. Isso fornece uma maneira de restringir a causa potencial de latência durante o processo de sincronização. 

O SQL Agent executa a coleta de dados e deve ser habilitado na réplica primária e pelo menos em uma das réplicas secundárias. Veja o relatório clicando com o botão direito do mouse no grupo de disponibilidade > Relatórios > Relatórios padrão no **Pesquisador de Objetos** do SQL Server Management Studio.  

Para obter mais informações, veja [Relatórios de latência do grupo de disponibilidade Always On](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-always-on-availability-group-latency-reports/).

## <a name="related-tasks"></a>Related Tasks  
  
-   [Usar as políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  
