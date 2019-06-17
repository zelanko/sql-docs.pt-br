---
title: Monitorando o espelhamento de banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring [SQL Server], database mirroring
- database mirroring [SQL Server], monitoring
ms.assetid: a7b1b9b0-7c19-4acc-9de3-3a7c5e70694d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 23c8c3c76b881f342f56490e5722a0ae641464ac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62755364"
---
# <a name="monitoring-database-mirroring-sql-server"></a>Monitorando o espelhamento de banco de dados (SQL Server)
  Esta seção apresenta o Monitor de Espelhamento de Banco de Dados e os procedimentos armazenados do sistema **sp_dbmmonitor** , explica como funciona o monitoramento de espelhamento de banco de dados (incluindo o **Trabalho de Monitor de Espelhamento de Banco de Dados)** e resume as informações sobre as sessões de espelhamento de banco de dados que podem ser monitoradas. Além disso, esta seção apresenta como definir limites de avisos para um conjunto de eventos de espelhamento de banco de dados predefinido e como configurar alertas em qualquer evento de espelhamento de banco de dados.  
  
 Você pode monitorar um banco de dados espelho durante uma sessão de espelhamento para verificar se e como os dados estão fluindo. Para definir e gerenciar o monitoramento de um ou mais dos bancos de dados espelhados em uma instância do servidor, você pode usar o Monitor de Espelhamento de Banco de Dados ou os procedimentos armazenados do sistema **sp_dbmmonitor** .  
  
 Um trabalho de monitoramento de espelhamento de banco de dados, **Trabalho do Monitor de Espelhamento de Banco de Dados**, opera em segundo plano, independentemente do Monitor de Espelhamento de Banco de Dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent chama o **Trabalho do Monitor de Espelhamento de Banco de Dados** em intervalos regulares, o padrão é uma por minuto, e o trabalho chama um procedimento armazenado que atualiza o status do espelhamento. Se você utilizar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para iniciar uma sessão de monitoramento, o **Trabalho do Monitor de Espelhamento de Banco de Dados** será criado automaticamente. Porém, se você usar somente ALTER DATABASE *<database_name>* SET PARTNER para iniciar o espelhamento, deverá criar o trabalho executando um procedimento armazenado.  
  
 **Neste tópico:**  
  
-   [Monitorando status de espelhamento](#MonitoringStatus)  
  
-   [Fontes adicionais de informação sobre um banco de dados espelho](#AdditionalSources)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="MonitoringStatus"></a> Monitorando status de espelhamento  
 Para configurar e gerenciar monitoramento para um ou mais dos bancos de dados espelhados em uma instância do servidor, você pode usar o Monitor de Espelhamento de Banco de Dados ou os procedimentos armazenados do sistema **dbmmonitor** . Você pode monitorar um banco de dados espelho durante uma sessão de espelhamento para verificar se e como os dados estão fluindo.  
  
 O monitoramento de um banco de dados espelho lhe permite, especificamente:  
  
-   Verificar se o espelhamento está funcionando.  
  
     O status básico inclui saber se as duas instâncias do servidor estão ativas, os servidores estão conectados, e se o log está sendo movimentado do principal para o espelhado.  
  
-   Determinar se o banco de dados espelho está acompanhando o banco de dados principal.  
  
     Durante o modo de alto desempenho, um servidor principal pode desenvolver um acúmulo de registros de log não enviados que ainda precisam ser enviados do servidor principal para o servidor espelho. Além disso, em qualquer modo operacional, o servidor espelho pode desenvolver um acúmulo de registros de log não restaurado que foram gravados no arquivo de log mas que ainda precisam ser restaurados no banco de dados espelho.  
  
-   Determinar quantos dados serão perdidos quando a instância de servidor principal ficar indisponível durante o modo de alto desempenho.  
  
     Você pode determinar perda de dados verificando a quantidade de log de transações não enviada (se houver) e o intervalo de tempo nos quais as transações perdidas estavam confirmadas no servidor principal.  
  
-   Comparar o desempenho atual com o desempenho passado.  
  
     No caso de problemas, um administrador de banco de dados pode exibir um histórico do desempenho de espelhamento para ajudar na compreensão do estado atual. A verificação do histórico pode permitir ao usuário detectar tendências em desempenho, identificando padrões de problemas de desempenho (como horas do dia em que a rede está lenta ou que o número de comandos que entram no log é muito grande).  
  
-   Diagnosticar a causa de fluxo reduzido de dados entre parceiros de espelhamento.  
  
-   Definir limites de aviso em métrica chave de desempenho.  
  
     Se uma nova linha de status contém um valor que excede um limite, um evento informativo é enviado ao log de eventos do Windows. Um administrador de sistema pode, então, configurar alertas manualmente com base nesses eventos. Para obter mais informações, veja [Usar os limites de aviso e alertas em métricas de desempenho de espelhamento &#40;SQL Server&#41;](use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
###  <a name="tools_for_monitoring_dbm_status"></a> Ferramentas para monitoramento de status de espelhamento de banco de dados  
 O status de espelhamento pode ser monitorado usando o Monitor de Espelhamento de Banco de Dados ou o procedimento armazenado do sistema **sp_dbmmonitorresults** . Essas ferramentas podem ser usadas para monitorar o espelhamento de banco de dados em qualquer banco de dados espelho na instância do servidor local, por ambos os administradores do Sistema, ou seja, membros da função de servidor fixa **sysadmin** e pelo usuário que foi adicionado à função do banco de dados fixa **dbm_monitor** no banco de dados **msdb** por um administrador do sistema. Ao usar qualquer uma das ferramentas, um administrador de sistema pode atualizar manualmente o status de espelhamento.  
  
> [!NOTE]  
>  Administradores de sistema podem também configurar e exibir limites de aviso para métricas de desempenho chave. Para obter mais informações, veja [Usar os limites de aviso e alertas em métricas de desempenho de espelhamento &#40;SQL Server&#41;](use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
-   Monitor de Espelhamento de Banco de Dados  
  
     O Monitor de Espelhamento de Banco de Dados é uma ferramenta de interface gráfica do usuário que permite aos administradores de sistema exibir e atualizar status e configurar limites de aviso em várias métricas de desempenho chave. O Monitor de Espelhamento de Banco de Dados também pode ser usado por membros da função fixa do banco de dados **dbm_monitor** para exibir a linha mais recente da tabela de status de espelhamento, embora não seja possível atualizar o status da tabela.  
  
     O monitor exibe o status, inclusive a métrica de desempenho, para um banco de dados selecionado na página com guias **Status** . O conteúdo desta página vem das duas instâncias de servidor principal e espelho. A página é preenchida de forma assíncrona conforme o status é coletado através de conexões separadas às instâncias de servidor principal e espelho. O monitor tenta atualizar a tabela de status a intervalos de 30 segundos. A atualização só terá sucesso se a tabela não for atualizada dentro de 15 segundos e o usuário for um membro da função de servidor fixa **sysadmin** . Para obter um resumo das informações relatadas na página **Status** , consulte [Status exibido pelo Monitor de Espelhamento de Banco de Dados](#perf_metrics_of_dbm_monitor), posteriormente neste tópico.  
  
     Para uma introdução à interface do Monitor de Espelhamento de Banco de Dados, consulte [Database Mirroring Monitor Overview](database-mirroring-monitor-overview.md). Para obter informações sobre como iniciar o Monitor de Espelhamento de Banco de Dados, veja [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md).  
  
-   Procedimentos armazenados do sistema  
  
     Também é possível recuperar ou atualizar o status atual executando o procedimento armazenado do sistema **sp_dbmmonitorresults** . Outros procedimentos armazenados de dbmmonitor lhe permitem definir o monitoramento, alterar os parâmetros de monitoramento, exibir o período de atualização atual e ignorar monitoramento na instância do servidor.  
  
     A tabela a seguir apresenta os procedimentos armazenados para administrar e usar o monitoramento de espelhamento de banco de dados independentemente do Monitor de Espelhamento de Banco de Dados.  
  
    |Procedimento|Descrição|  
    |---------------|-----------------|  
    |[sp_dbmmonitoraddmonitoring](/sql/relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql)|Cria uma tarefa que atualiza periodicamente as informações de status para cada banco de dados espelho na instância do servidor.|  
    |[sp_dbmmonitorchangemonitoring](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql)|Altera o valor de um parâmetro de monitoração de espelhamento de banco de dados.|  
    |[sp_dbmmonitorhelpmonitoring](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql)|Retorna o período de atualização atual.|  
    |[sp_dbmmonitorresults](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql)|Retorna linhas de status para um banco de dados monitorado e lhe permite escolher se o procedimento obtém o último status antecipadamente.|  
    |[sp_dbmmonitordropmonitoring](/sql/relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql)|Interrompe e exclui a tarefa de monitoramento de espelhamento para todos os bancos de dados na instância do servidor.|  
  
     Os procedimentos armazenados do sistema **dbmmonitor** podem ser usados como complemento do Monitor de Espelhamento de Banco de Dados. Por exemplo, mesmo que o monitoramento tenha sido configurado usando o **sp_dbmmonitoraddmonitoring**, o Monitor de Espelhamento de Banco de Dados poderá ser usado para exibir o status.  
  
### <a name="how-monitoring-works"></a>Como monitorar trabalhos  
 Essa seção apresenta a tabela de status de espelhamento de banco de dados, o trabalho de monitor de espelhamento de banco de dados e o monitor, como os usuários podem monitorar o status de espelhamento de banco de dados e como o trabalho de monitoramento pode ser descartado.  
  
#### <a name="database-mirroring-status-table"></a>Tabela de status de espelhamento de banco de dados  
 O status de espelhamento de banco de dados é armazenado em uma tabela de status de espelhamento de banco de dados interna, não documentada, no banco de dados **msdb** . Essa tabela de status é criada automaticamente na primeira vez em que o status de espelhamento é atualizado na instância de servidor.  
  
 A tabela de status pode ser atualizada automática ou manualmente por um administrador de sistema, com um intervalo de atualização mínimo de 15 segundos. O mínimo de 15 segundos evita que instâncias de servidor sejam sobrecarregadas com solicitações de status.  
  
 A tabela de status é automaticamente atualizada tanto pelo Monitor de Espelhamento de Banco de Dados quanto pelo trabalho de monitor de espelhamento de banco de dados, se estiverem sendo executados. O**Trabalho de Monitor de Espelhamento de Banco de Dados** atualiza a tabela a cada minuto, por padrão (um administrador do sistema pode especificar um período de atualização de 1 a 120 minutos). O Monitor de Espelhamento de Banco de Dados, ao contrário, atualiza a tabela automaticamente a cada 30 segundos. Para essas atualizações, o **Trabalho de Monitor de Espelhamento de Banco de Dados** e o Monitor de Espelhamento de Banco de Dados chamam **sp_dbmmonitorupdate**.  
  
 Na primeira vez que o **sp_dbmmonitorupdate** é executado, ele cria a tabela de **status de espelhamento de banco de dados** e a função de banco de dados fixa **dbm_monitor** no banco de dados **msdb** . Normalmente,**sp_dbmmonitorupdate** atualiza o status de espelhamento inserindo uma nova linha na tabela de status para cada banco de dados espelho na instância de servidor; para obter mais informações, veja “Tabela de status de espelhamento de banco de dados”, mais adiante neste tópico. Esse procedimento também avalia a métrica de desempenho nas linhas novas e faz o truncamento de linhas mais antigas do que o período de retenção atual (o padrão é 7 dias). Para obter mais informações, veja [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql).  
  
> [!NOTE]  
>  A menos que o Monitor de Espelhamento de Banco de Dados esteja sendo usado no momento por um membro da função de servidor fixa **sysadmin** , a tabela de status só será automaticamente atualizada se o **Trabalho de Monitor de Espelhamento de Banco de Dados** existir e se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent estiver sendo executado.  
  
#### <a name="database-mirroring-monitor-job"></a>Trabalho do Monitor de Espelhamento de Banco de Dados  
 O trabalho de monitor de espelhamento de banco de dados, **Trabalho de Monitor de Espelhamento de Banco de Dados**, opera independentemente do Monitor de Espelhamento de Banco de Dados. O**Trabalho de Monitor de Espelhamento de Banco de Dados** será criado automaticamente somente se [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] for usado para iniciar uma sessão de espelhamento. Se os comandos ALTER DATABASE *database_name* SET PARTNER forem sempre usados para iniciar um espelhamento, o trabalho só existirá se o administrador de sistema executar o procedimento armazenado **sp_dbmmonitoraddmonitoring** .  
  
 Depois que o **Trabalho de Monitor de Espelhamento de Banco de Dados** for criado, e supondo-se que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esteja sendo executado, o trabalho será chamado a cada minuto, por padrão. Em seguida, o trabalho chama o procedimento armazenado do sistema **sp_dbmmonitorupdate** .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent chama o **Trabalho de Monitor de Espelhamento de Banco de Dados** a cada minuto, por padrão, e o trabalho chama **sp_dbmmonitorupdate** para atualizar a tabela de status. Administradores do sistema podem alterar o período de atualização usando o procedimento armazenado do sistema **sp_dbmmonitorchangemonitoring** e podem exibir o período de atualização atual usando o procedimento armazenado do sistema **sp_dbmmonitorchangemonitoring** . Para obter mais informações, veja [sp_dbmmonitoraddmonitoring &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql) e [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql).  
  
#### <a name="monitoring-database-mirroring-status-by-system-administrators"></a>Monitorando status de espelhamento de banco de dados (por Administradores de sistema)  
 Membros da função de servidor fixa **sysadmin** podem exibir e atualizar a tabela de status  
  
-   Usando o Monitor de Espelhamento de Banco de Dados  
  
     Ao usar o Monitor de Espelhamento de Banco de Dados, um administrador de sistema pode atualizar manualmente a página **Status** , a árvore de navegação ou a página **Histórico** . Isso também atualiza a tabela de status, a menos que ela já tenha sido atualizada nos 15 segundos anteriores.  
  
     Para exibir o histórico de status de espelhamento em determinada instância de servidor, o administrador do sistema também pode clicar no botão **Histórico** de uma instância de servidor (na página **Status** ). O histórico é exibido na caixa de diálogo **Histórico do Espelhamento de Banco de Dados** . Ali, o administrador de sistema pode exibir algumas ou todas as linhas na tabela de status da instância de servidor.  
  
     Para obter mais informações sobre a métrica de página **Status** , consulte Métrica de Desempenho, exibida pelo "Monitor de Espelhamento de Banco de Dados," mais adiante neste tópico.  
  
-   Usando **sp_dbmmonitorresults**  
  
     Administradores do sistema podem usar o procedimento armazenado do sistema **sp_dbmmonitorresults** para exibir e, opcionalmente, atualizar a tabela de status, caso não tenha sido atualizada nos 15 segundos anteriores. Esse procedimento chama o procedimento **sp_dbmmonitorupdate** e retorna uma ou mais linhas do histórico, dependendo da quantidade solicitada na chamada de procedimento. Para obter informações sobre o status em seu conjunto de resultados, veja [sp_dbmmonitorresults &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql).  
  
#### <a name="monitoring-database-mirroring-status-by-dbmmonitor-members"></a>Monitorando o status de espelhamento de banco de dados (por membros dbm_monitor)  
 Conforme mencionado, na primeira vez que **sp_dbmmonitorupdate** é executado, ele cria a função de banco de dados fixa **dbm_monitor** no banco de dados **msdb** . Membros da função de banco de dados fixa **dbm_monitor** podem exibir o status de espelhamento existente usando o Monitor de Espelhamento de Banco de Dados ou o procedimento armazenado **sp_dbmmonitorresults** . Esses usuários, porém, não podem atualizar a tabela de status. Para saber a idade do status exibido, um usuário pode examinar os horários nos rótulos **Log principal (***\<time>***)** e **Log espelhado (***\<time>***)** na página **Status**.  
  
 Membros da função de banco de dados fixa **dbm_monitor** dependem do **Trabalho de Monitor de Espelhamento de Banco de Dados** para atualizar a tabela de status em intervalos regulares. Se o trabalho não existir ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent for interrompido, o status se tornará cada vez mais obsoleto e poderá deixar de refletir a configuração da sessão de espelhamento. Por exemplo, depois de um failover, poderá parecer que os parceiros compartilham a mesma função, principal ou espelhada ou o servidor principal atual poderá ser mostrado como o espelho e o servidor espelhado atual como o principal.  
  
#### <a name="dropping-the-database-mirroring-monitor-job"></a>Descartando o Trabalho de Monitor de Espelhamento de Banco de Dados  
 O trabalho de monitor de espelhamento de banco de dados, **Trabalho de Monitor de Espelhamento de Banco de Dados**, permanece até que seja descartado. O trabalho de monitoramento deve ser gerenciado pelo administrador de sistema. Para remover o **Trabalho de Monitor de Espelhamento de Banco de Dados**, use **sp_dbmmonitordropmonitoring**. Para obter mais informações, veja [sp_dbmmonitordropmonitoring &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql).  
  
###  <a name="perf_metrics_of_dbm_monitor"></a> Status exibido pelo Monitor de Espelhamento de Banco de Dados  
 A página **Status** do Monitor de Espelhamento de Banco de Dados descreve os parceiros, e também o estado da sessão de espelhamento. O status inclui métrica de desempenho como o estado de log de transações, além de outras informações, com o objetivo de ajudar o cálculo atual da hora exigida para completar um failover e o potencial de perda de dados, se a sessão não for sincronizada. Além disso, a página **Status** exibe status e informações em geral sobre a sessão de espelhamento.  
  
> [!NOTE]  
>  Para obter uma introdução do Monitor de Espelhamento de Banco de Dados e da página **Status** , confira [Ferramentas para monitoramento de status de espelhamento de banco de dados](#tools_for_monitoring_dbm_status), acima neste tópico.  
  
 As informações fornecidas para cada um deles é resumida nas seções a seguir.  
  
#### <a name="partners"></a>Parceiros  
 A página **Status** exibe as seguintes informações para cada um dos parceiros:  
  
-   Instância de servidor  
  
     Nome da instância de servidor cujo status é exibido na linha **Status** .  
  
-   Função atual  
  
     Função atual da instância de servidor. Os estados possíveis são:  
  
    -   Principal  
  
    -   Espelho  
  
-   Estado de espelhamento  
  
     Os estados possíveis são:  
  
    -   Unknown (desconhecido)  
  
    -   Sincronizando  
  
    -   Sincronizado  
  
    -   Suspenso  
  
    -   Desconectado  
  
-   Conexão de testemunha  
  
     Status de conexão de testemunha. Os estados possíveis são:  
  
    -   Unknown (desconhecido)  
  
    -   Conectado  
  
    -   Desconectado  
  
#### <a name="log-on-the-principal-server"></a>Efetue logon do servidor principal  
 A página **Status** exibe as seguintes informações sobre o status do log no servidor principal a partir da hora indicada:  
  
-   Log não enviado  
  
     A quantidade de log esperando na fila de envio em quilobytes (KB).  
  
-   Transação não enviada mais antiga  
  
     Idade da transação não enviada mais antiga na fila de envio. A idade dessa transação indica quantos minutos de transações ainda não foram enviados à instância de servidor espelho. Esse valor ajuda a medir o potencial de perda de dados em termos de tempo.  
  
-   Tempo para enviar o log (estimado)  
  
     Número estimado de minutos que a instância de servidor principal exige para enviar o log atualmente na fila de envio para a instância de servidor espelho com base na taxa de envio atual. A hora real para o envio do log será afetada pela taxa de transações de entrada que podem variar significativamente. Porém, o valor **Tempo para enviar o log (estimado)** pode ser útil para o cálculo, aproximado, do tempo exigido para um failover manual.  
  
-   Taxa de envio atual  
  
     Taxa à qual estão sendo enviadas transações à instância de servidor espelho em KB por segundo.  
  
-   Taxa atual de transações novas  
  
     Taxa em que as transações de entrada estão sendo inseridas no log do servidor principal, em KB por segundo. Para determinar se o espelhamento está atrasado, ativo ou atualizado, compare esse valor ao valor do **Tempo para enviar o log (estimado)** .  
  
#### <a name="log-on-the-mirror-server"></a>Efetue logon do servidor espelho  
 A página **Status** exibe as seguintes informações sobre o status do log no servidor espelho a partir da hora indicada:  
  
-   Log não restaurado  
  
     A quantidade de log esperando na fila de restauração em KB.  
  
-   Tempo para recuperar o log (estimado)  
  
     Número aproximado de minutos exigido para que o log atualmente na fila de restauração seja aplicado ao banco de dados espelho.  
  
-   Taxa atual de restauração  
  
     Taxa em que as transações estão sendo restauradas no banco de dados espelho (em KB por segundo).  
  
#### <a name="mirroring-session"></a>Sessão de espelhamento  
 Além disso, a página **Status** exibe as seguintes informações sobre a sessão de espelhamento.  
  
-   Sobrecarga de confirmação de espelhamento  
  
     Atraso médio por transação em milissegundos (pertinente apenas em modo de alta segurança). Esse atraso consiste na quantidade de sobrecarga incidente enquanto a instância do servidor principal aguarda que a instância do servidor espelho grave o registro do log da transação na fila de restauração.  
  
-   Tempo para enviar e restaurar todos os logs atuais (estimado)  
  
     Tempo estimado necessário para enviar todo o log não enviado confirmado no principal e para restaurar todo o log atualmente na fila de restauração. Essa estimativa pode ser menor do que a soma dos valores dos campos **Tempo para enviar o log (estimado)** e **Tempo para recuperar o log (estimado)** uma vez que o envio e a restauração podem operar em paralelo.  
  
-   Endereço de testemunha  
  
     Endereço de rede da instância de servidor testemunha. Para obter informações sobre o formato desse endereço, veja [Especificar um endereço de rede do servidor &#40;Espelhamento de Banco de Dados&#41;](specify-a-server-network-address-database-mirroring.md).  
  
-   Modo de operação  
  
     Modo operacional da sessão de espelhamento de banco de dados:  
  
    -   Alto desempenho (assíncrono)  
  
    -   Alta segurança sem failover automático (síncrono)  
  
    -   Alta segurança com failover automático (síncrono)  
  
##  <a name="AdditionalSources"></a> Fontes adicionais de informação sobre um banco de dados espelho  
 Além de usar os procedimentos armazenados do Monitor de Espelhamento de Banco de Dados e dbmmonitor para monitorar um banco de dados espelhado e configurar alertas em variáveis de desempenho monitoradas, o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] fornece exibições de catálogo, contadores de desempenho e notificações de eventos para espelhamento de banco de dados.  
  
 **Nesta seção:**  
  
-   [Metadados de espelhamento de banco de dados](#DbmMetadata)  
  
-   [Contadores de desempenho para espelhamento de banco de dados.](#DbmPerfCounters)  
  
-   [Notificações de eventos de espelhamento de banco de dados.](#DbmEventNotif)  
  
###  <a name="DbmMetadata"></a> Metadados de espelhamento de banco de dados  
 Cada sessão de espelhamento de banco de dados é descrita em metadados expostos pelos catálogo ou exibições de gerenciamento dinâmico seguintes:  
  
-   **sys.database_mirroring**  
  
     Essa exibição mostra os metadados de espelhamento de banco de dados de cada banco de dados espelho em uma instância de servidor. Para obter mais informações, veja [sys.database_mirroring &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql).  
  
-   **sys.database_mirroring_endpoints**  
  
     A exibição de catálogo **sys.database_mirroring_endpoints** mostra informações sobre o ponto de extremidade do espelhamento de banco de dados da instância do servidor. Para obter mais informações, veja [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql).  
  
-   **sys.database_mirroring_witnesses**  
  
     Essa exibição de catálogo mostra os metadados de espelhamento de banco de dados para cada sessão na qual uma instância de servidor é a testemunha. Para obter mais informações, veja [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses).  
  
-   **sys.dm_db_mirroring_connections**  
  
     Essa exibição de gerenciamento dinâmico retorna uma linha para cada conexão de rede de espelhamento de banco de dados.  
  
     Para obter mais informações, veja [sys.dm_db_mirroring_connections &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections).  
  
###  <a name="DbmPerfCounters"></a> Contadores de desempenho para espelhamento de banco de dados.  
 Os contadores de desempenho permitem que você monitore o desempenho de espelhamento de banco de dados. Por exemplo, você pode examinar o contador **Atraso na Transação** para verificar se o espelhamento de banco de dados está afetando o desempenho do servidor principal, você pode examinar os contadores **Fila de Restauração** e **Fila de Envio de Log** para verificar como o banco de dados espelho está se comportando em relação ao banco de dados principal. Você pode examinar o contador **Bytes de Log Enviados/s** para monitorar a quantidade de logs enviados por segundo.  
  
 No Monitor de Desempenho em qualquer um dos parceiros, os contadores de desempenho estão disponíveis no objeto de desempenho de espelhamento de banco de dados (**SQLServer:Database Mirroring**). Para obter mais informações, consulte [SQL Server, Database Mirroring Object](../../relational-databases/performance-monitor/sql-server-database-mirroring-object.md).  
  
 **Para iniciar o monitor de desempenho**  
  
-   [Iniciar o Monitor do Sistema &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
###  <a name="DbmEventNotif"></a> Notificações de eventos de espelhamento de banco de dados.  
 As notificações de evento são um tipo especial de objeto de banco de dados. As notificações de evento são executadas em resposta a uma variedade de instruções DDL (linguagem de definição de dados) Transact-SQL e eventos de Rastreamento do SQL e enviam informações sobre o servidor e eventos de banco de dados para um serviço [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
 Os seguintes eventos estão disponíveis para o espelhamento de banco de dados:  
  
-   Classe de evento**Database Mirroring State Change**  
  
     Isso indica quando o estado de espelhamento de um banco de dados espelho muda. Para obter mais informações, consulte [Database Mirroring State Change Event Class](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md).  
  
-   Classe de evento**Audit Database Mirroring Login**  
  
     Informa mensagens de auditoria relacionadas à segurança de transporte do espelhamento de banco de dados. Para obter mais informações, consulte [Audit Database Mirroring Login Event Class](../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Usar os limites de aviso e alertas em métricas de desempenho de espelhamento &#40;SQL Server&#41;](use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [Exibir o estado de um banco de dados espelhado &#40;SQL Server Management Studio&#41;](view-the-state-of-a-mirrored-database-sql-server-management-studio.md)  
  
 **Procedimentos armazenados**  
  
-   [sp_dbmmonitoraddmonitoring &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql)  
  
-   [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql)  
  
-   [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql)  
  
-   [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql)  
  
-   [sp_dbmmonitordropmonitoring &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql)  
  
-   [sp_dbmmonitorhelpalert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql)  
  
-   [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql)  
  
-   [sp_dbmmonitorresults &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql)  
  
-   [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql)  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Provedor WMI para conceitos de eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
