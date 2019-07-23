---
title: Descarregar a carga de trabalho somente leitura na réplica secundária de um grupo de disponibilidade
description: Saiba mais sobre o descarregamento de consultas e relatórios somente leitura para uma réplica secundária de um grupo de disponibilidade Always On no SQL Server.
ms.custom: seodec18
ms.date: 06/06/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- readable secondary replicas
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 78f3f81a-066a-4fff-b023-7725ff874fdf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9608383d132dbb670d8a852101dd074d4f285a79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991662"
---
# <a name="offload-read-only-workload-to-secondary-replica-of-an-always-on-availability-group"></a>Descarregar a carga de trabalho somente leitura na réplica secundária de um grupo de disponibilidade Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Os recursos secundários ativos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] incluem suporte para acesso somente leitura para uma ou mais réplicas secundárias (*réplicas secundárias legíveis*). Uma réplica secundária legível pode estar no modo de disponibilidade de confirmação síncrona ou no modo de disponibilidade de confirmação assíncrona. Uma réplica secundária legível permite acesso somente leitura a todos os seus bancos de dados secundários. No entanto, os bancos de dados secundários legíveis não são definidos como somente leitura. Eles são dinâmicos. Um banco de dados secundário determinado muda conforme as alterações nos dados do banco de dados primário correspondente são aplicadas ao banco de dados secundário. Para uma réplica secundária típica, os dados, incluindo tabelas com otimização de memória durável, nos bancos de dados secundários estão quase em tempo real. Além disso, os índices de texto completo são sincronizados com os bancos de dados secundários. Em muitas circunstâncias, a latência de dados entre um banco de dados primário e o banco de dados secundário correspondente é de somente alguns segundos.  
  
 Configurações de segurança que ocorrem nos bancos de dados primários para os bancos de dados secundários são permitidas. Isso inclui os usuários, as funções de banco de dados e de aplicativos junto com suas permissões respectivas e a TDE (criptografia de dados transparente), se habilitada no banco de dados primário.  
  
> [!NOTE]  
>  Embora não seja possível gravar dados em bancos de dados secundários, é possível gravar em bancos de dados de leitura e gravação na instância de servidor que hospeda a réplica secundária, incluindo bancos de dados de usuário e do sistema, como **tempdb**.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] também dá suporte ao reencaminhamento de solicitações de conexão de intenção de leitura para uma réplica secundária legível (*roteamento somente leitura*). Para obter informações sobre roteamento somente leitura, veja [Usando um ouvinte para de conectar a uma réplica secundária somente leitura (roteamento somente leitura)](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary).  
  
##  <a name="bkmk_Benefits"></a> Benefícios  
 Direcionar conexões somente leitura a réplicas secundárias legíveis tem os seguintes benefícios:  
  
-   Descarrega suas cargas de trabalho somente leitura secundárias de sua réplica primária, o que conserva seus recursos para cargas de trabalho críticas. Se você tiver missão carga de trabalho de leitura crítica ou que não possa tolerar latência, execute-a na primária.  
  
-   Melhora seu retorno de investimento para os sistemas que hospedam réplicas secundárias legíveis.  
  
 Além disso, secundárias legíveis fornecem suporte robusto para operações somente leitura, como segue:  
  
-   Estatísticas temporárias automáticas sobre o banco de dados secundário legível otimizam as consultas somente leitura em tabelas baseadas em disco. Para tabelas com otimização de memória, as estatísticas ausentes são criadas automaticamente. Porém, não há nenhuma atualização automática de estatísticas obsoletas. Você precisará atualizar manualmente as estatísticas na réplica primária. Para obter informações, veja [Estatísticas para bancos de dados somente leitura](#Read-OnlyStats), mais adiante neste tópico.  
  
-   As cargas de trabalho somente leitura para tabelas baseadas em disco usam o controle de versão de linha para remover a contenção de bloqueio nos bancos de dados secundários. Todas as consultas executadas nos bancos de dados secundários são mapeadas automaticamente para o nível de transação de isolamento de instantâneo, até mesmo quando outros níveis de isolamento de transação são definidos explicitamente. Além disso, todas as dicas de bloqueio são ignoradas. Isso elimina a contenção do leitor/gravador.  
  
-   As cargas de trabalho somente leitura para tabelas duráveis com otimização de memória acessam os dados exatamente da mesma forma que são acessadas no banco de dados primário, usando procedimentos armazenados nativos ou interoperabilidade de SQL com as mesmas restrições de nível de isolamento da transação (veja [Níveis de isolamento no mecanismo de banco de dados](https://msdn.microsoft.com/8ac7780b-5147-420b-a539-4eb556e908a7)). A carga de trabalho de relatório ou as consultas somente leitura que são executadas na réplica primária podem ser executadas na réplica secundária sem exigir nenhuma alteração. Da mesma maneira, uma carga de trabalho de relatório ou as consultas somente leitura que são executadas em uma réplica secundária podem ser executadas na réplica primária sem exigir nenhuma alteração.  De maneira semelhante a tabelas baseadas em disco, todas as consultas executadas nos bancos de dados secundários são mapeadas automaticamente para o nível de transação de isolamento de instantâneo, até mesmo quando outros níveis de isolamento de transação são definidos explicitamente.  
  
-   As operações DML são permitidas em variáveis de tabela para os tipos baseados em disco e em tabela com otimização de memória na réplica secundária.  
  
##  <a name="bkmk_Prerequisites"></a> Pré-requisitos para o grupo de disponibilidade  
  
-   **Réplicas secundárias legíveis (obrigatório)**  
  
     O administrador de banco de dados precisa configurar uma ou mais réplicas de forma que, ao ser executado sob a função secundária, eles permitem todas as conexões (apenas para acesso somente leitura) ou apenas conexões de intenção de leitura.  
  
    > [!NOTE]  
    >  Como opção, o administrador de banco de dados pode configurar qualquer réplica de disponibilidade para excluir conexões somente leitura ao executar sob a função primária.  
  
     Para obter informações, veja [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md).  
  
-   **Ouvinte de grupo de disponibilidade**  
  
     Para dar suporte ao roteamento somente leitura, um grupo de disponibilidade deve ter um [ouvinte do grupo de disponibilidade](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md). O cliente somente leitura deve direcionar suas solicitações de conexão para este ouvinte e a cadeia de conexão do cliente deve especificar a intenção do aplicativo como "somente leitura." Ou seja, elas devem ser *solicitações de conexão de intenção de leitura*.  
  
-   **Roteamento somente leitura**  
  
     *Roteamento somente leitura* refere-se à capacidade de o SQL Server encaminhar solicitações de conexão de intenção de leitura, que são direcionadas para um ouvinte do grupo de disponibilidade, para uma réplica secundária legível disponível. Os pré-requisitos para roteamento somente leitura são os seguintes:  
  
    -   Para dar suporte a roteamento somente leitura, uma réplica secundária legível exigirá uma URL de roteamento somente leitura. Esta URL só entra em vigor quando a réplica local estiver sendo executada sob a função secundária. A URL do roteamento somente leitura deve ser especificada réplica por réplica, quando necessário. Cada URL de roteamento somente leitura é usada para solicitações de conexão de intenção de leitura para uma réplica secundária legível específica. Normalmente, toda réplica secundária legível é atribuída uma URL de roteamento somente leitura.  
  
    -   Cada réplica de disponibilidade que deve dar suporte a roteamento somente leitura quando é a réplica primária exige uma lista de roteamento somente leitura. Uma determinada lista de roteamento somente leitura só entra em vigor quando a réplica local estiver sendo executada em uma função primária. Essa lista deve ser especificada réplica por réplica, quando necessário. Normalmente, cada lista de roteamento somente leitura deveria conter todas as URLs de roteamento somente leitura, com a URL da réplica local no final da lista.  
  
        > [!NOTE]  
        >  Solicitações de conexão de intenção de leitura podem ter balanceamento de carga entre réplicas. Para obter mais informações, veja [Configurar o balanceamento de carga entre réplicas somente leitura](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).  
  
     Para obter informações, veja [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md).  
  
> [!NOTE]  
>  Para obter informações sobre ouvintes do grupo de disponibilidade e mais informações sobre roteamento somente leitura, veja [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativos &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).  
  
##  <a name="bkmk_LimitationsRestrictions"></a> Limitações e restrições  
 Algumas operações não têm suporte total, como segue:  
  
-   Assim que uma réplica legível é habilitada para leitura, pode começar a aceitar conexões para seus bancos de dados secundários. Porém, se houver transações ativas em um banco de dados primário, as versões de linha não estarão completamente disponíveis no banco de dados secundário correspondente. As transações ativas que existiam na réplica primária quando a réplica secundária foi configurada devem ser confirmadas ou revertidas. Até que esse processo termine, o mapeamento do nível de isolamento da transação no banco de dados secundário ficará incompleto e as consultas serão bloqueadas temporariamente.  
  
    > [!WARNING]  
    >  Executar transações demoradas tem um impacto no número de linhas com versão mantidas para tabelas baseadas em disco e com otimização de memória.  
  
-   Em um banco de dados secundário com tabelas com otimização de memória, embora as versões de linha sempre sejam geradas para tabelas com otimização de memória, as consultas serão bloqueadas até que todas as transações ativas que existiam na réplica primária quando a réplica secundária foi habilitada para leitura sejam concluídas. Isso garante que as tabelas baseadas em disco e com otimização de memória estejam disponíveis para a carga de trabalho do relatório e as consultas somente leitura ao mesmo tempo.  
  
-   Não há suporte para o controle de alterações e a captura de dados de alterações em bancos de dados secundários que pertencem a uma réplica secundária legível:  
  
    -   O controle de alterações é desabilitado explicitamente em bancos de dados secundários.  
  
    -   A Captura de Dados de Alterações não pode ser habilitado apenas em um banco de dados de réplica secundária. A Captura de Dados de Alterações pode ser habilitada no banco de dados de réplica primária e as alterações podem ser lidas em tabelas de CDC usando as funções do banco de dados de réplica secundária.  
  
-   Como as operações de leitura são mapeadas para nível de transação de isolamento de instantâneo, a limpeza de registros fantasmas na réplica primária pode ser bloqueada por transações em uma ou mais réplicas secundárias. A tarefa de limpeza de registro fantasma limpará automaticamente os registros fantasmas para tabelas baseadas em disco na réplica primária quando eles não forem mais necessários nas réplicas secundárias.  Isso é similar ao que acontece quando você executa transações na réplica primária. Em caso extremo no banco de dados secundário, você precisará eliminar consultas de leitura de longa execução que bloqueiam a limpeza fantasma. Observe que a limpeza fantasma pode ser bloqueada se a réplica secundária for desconectada ou quando a movimentação de dados for suspensa no banco de dados secundário. Este estado também impede truncamento de logs. Portanto, se este estado persistir, recomendaremos que você remova este banco de dados secundário do grupo de disponibilidade. Não há nenhum problema de limpeza de registro fantasma com tabelas com otimização de memória porque as versões de linha são mantidas na memória e são independentes das versões de linha na réplica primária.  
  
-   A operação DBCC SHRINKFILE em arquivos que contêm tabelas baseadas em disco poderá falhar na réplica primária se o arquivo contiver registros fantasmas que ainda são necessários em uma réplica secundária.  
  
-   A partir do [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], as réplicas secundárias legíveis podem permanecer online mesmo quando a réplica primária estiver offline devido à ação do usuário ou a uma falha. No entanto, o roteamento somente leitura não funciona nessa situação porque o ouvinte do grupo de disponibilidade está offline também. Os clientes devem se conectar diretamente às réplicas secundárias somente leitura para cargas de trabalho somente leitura.  
  
> [!NOTE]  
>  Se você consultar a exibição de gerenciamento dinâmico [sys.dm_db_index_physical_stats](../../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) em uma instância de servidor que está hospedando uma réplica secundária legível, poderá encontrar um problema de bloqueio REDO. Isso ocorre porque essa exibição de gerenciamento dinâmico adquire um bloqueio IS na exibição ou tabela de usuário especificada, que pode bloquear solicitações por um thread REDO para um bloqueio X na exibição ou tabela de usuário.  
  
##  <a name="bkmk_Performance"></a> Considerações sobre desempenho  
 Esta seção aborda várias considerações sobre desempenho de bancos de dados secundários legíveis  
  
 **Nesta seção:**  
  
-   [Latência de dados](#DataLatency)  
  
-   [Impacto da carga de trabalho somente leitura](#ReadOnlyWorkloadImpact)  
  
-   [Indexação](#bkmk_Indexing)  
  
-   [Estatísticas para bancos de dados somente leitura](#Read-OnlyStats)  
  
###  <a name="DataLatency"></a> Latência de dados  
 A implementação do acesso somente leitura a réplicas secundárias será útil se as suas cargas de trabalho somente leitura puderem tolerar certa latência de dados. Nas situações em que a latência de dados é inaceitável, considere executar cargas de trabalho somente leitura na réplica primária.  
  
 A réplica primária envia registros de log de alterações no banco de dados primário para as réplicas secundárias. Em cada banco de dados secundário, um thread de restauração dedicado aplica os registros de log. Em um banco de dados secundário de acesso de leitura, uma determinada alteração de dados não aparece nos resultados da consulta até que o registro de log que contém a alteração seja aplicado ao banco de dados secundário e a transação seja confirmada no banco de dados primário.  
  
 Isso significa que há alguma latência, normalmente apenas uma questão de segundos, entre as réplicas primárias e secundárias. No entanto, em casos incomuns, como quando problemas de rede reduzem a taxa de transferência, a latência pode se tornar significativa. A latência aumenta quando ocorrem gargalos de E/S e quando a movimentação de dados é suspensa. Para monitorar a movimentação de dados suspensa, você pode usar o [Painel AlwaysOn](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md) ou a exibição de gerenciamento dinâmico [sys.dm_hadr_database_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) .  
  
####  <a name="bkmk_LatencyWithInMemOLTP"></a> Latência de dados em banco de dados com tabelas com otimização de memória  
 No [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], havia considerações especiais relativas à latência de dados em secundárias ativas – confira [[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Secundárias ativas: Réplicas secundárias legíveis](https://technet.microsoft.com/library/ff878253(v=sql.120).aspx). A partir do [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] , não há considerações especiais em relação à latência de dados em tabelas com otimização de memória. A latência de dados esperada para tabelas com otimização de memória é comparável à latência para tabelas baseadas em disco.  
  
###  <a name="ReadOnlyWorkloadImpact"></a> Impacto da carga de trabalho somente leitura  
 Ao configurar uma réplica secundária para acesso somente leitura, suas cargas de trabalho somente leitura nos bancos de dados secundários consumirão recursos do sistema, como CPU e E/S (para tabelas baseadas em disco) de threads de restauração, especialmente se as cargas de trabalho somente leitura (para tabelas baseadas em disco) consumirem muitos recursos de E/S. Não há nenhum impacto de E/S ao acessar tabelas com otimização de memória porque todas as linhas residem na memória.  
  
 Além disso, as cargas de trabalho somente leitura nas réplicas secundárias podem bloquear alterações de DDL (linguagem de definição de dados) aplicadas por meio de registros de log.  
  
-   Mesmo que as operações de leitura não usem bloqueios compartilhados devido ao controle de versão de linha, essas operações usam bloqueios de estabilidade de esquema (Sch-S), o que pode bloquear operações de refazer que estejam aplicando alterações DDL. As operações de DDL incluem tabelas ALTER/DROP e exibições, mas não DROP ou ALTER de procedimentos armazenados. Portanto, por exemplo, se você descartar uma tabela com base em disco ou com otimização de memória, no primário. Quando o thread REDO processa o registro de log para descartar a tabela, ele deve adquirir um bloqueio de SCH_M na tabela e pode ser bloqueado por uma consulta em execução que acessa a tabela.  Esse é o mesmo comportamento na réplica primária exceto que o descarte da tabela é feito como parte de uma sessão de usuário e não para o thread REDO.  
  
-   Há um bloqueio adicional de tabelas com otimização de memória. Um descarte do procedimento armazenado nativo pode fazer o thread REDO ser bloqueado se houver uma execução simultânea do procedimento armazenado nativo na réplica secundária. Esse é o mesmo comportamento na réplica primária exceto que o descarte do procedimento armazenado é feito como parte de uma sessão de usuário e não para o thread REDO.  
  
 Fique atento às práticas recomendadas referentes à criação de consultas e use-as nos bancos de dados secundários. Por exemplo, agende consultas de longa execução, como agregações de dados durante horários de baixa atividade.  
  
> [!NOTE]  
>  Se um thread de restauração estiver bloqueado por consultas em uma réplica secundária, o XEvent **sqlserver.lock_redo_blocked** será gerado.  
  
###  <a name="bkmk_Indexing"></a> Indexação  
 Para otimizar cargas de trabalho somente leitura nas réplicas secundárias legíveis, talvez você queira criar índices nas tabelas nos bancos de dados secundários. Como você não pode fazer alterações de esquema ou de dados nos bancos de dados secundários, crie índices nos bancos de dados primários e permita que as alterações sejam transferidas para o banco de dados secundário por meio do processo de refazer.  
  
 Para monitorar a atividade de uso de índice em uma réplica secundária, consulte as colunas **user_seeks**, **user_scans**e **user_lookups** da exibição de gerenciamento dinâmico [sys.dm_db_index_usage_stats](../../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md) .  
  
###  <a name="Read-OnlyStats"></a> Estatísticas para bancos de dados somente leitura  
 As estatísticas em colunas de tabelas e exibições indexadas são usadas para otimizar os planos da consulta. Para grupos de disponibilidade, as estatísticas que são criadas e mantidas nos bancos de dados primários são automaticamente persistidas nos bancos de dados secundários como parte da aplicação dos registros dos logs de transação. No entanto, a carga de trabalho somente leitura nos bancos de dados secundários talvez precise de estatísticas diferentes daquelas criadas nos bancos de dados primários. No entanto, como os bancos de dados secundários são restritos ao acesso somente leitura, não é possível criar estatísticas nos bancos de dados secundários.  
  
 Para resolver esse problema, a réplica secundária cria e mantém estatísticas temporárias para bancos de dados secundários em **tempdb**. O sufixo _readonly_database_statistic é anexado ao nome das estatísticas temporárias para diferenciá-las das permanentes que persistem do banco de dados primário.  
  
 Somente o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode criar e atualizar estatísticas temporárias. No entanto, você pode excluir estatísticas temporárias e monitorar suas propriedades usando as mesmas ferramentas que você utiliza para estatísticas permanentes:  
  
-   Exclua estatísticas temporárias usando a instrução [DROP STATISTICS](../../../t-sql/statements/drop-statistics-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
-   Para monitorar as estatísticas, use as exibições de catálogo **sys.stats** e **sys.stats_columns** . **sys_stats** inclui uma coluna, **is_temporary**, para indicar quais estatísticas são permanentes e quais são temporárias.  
  
 Não há suporte para a atualização automática de estatísticas para tabelas com otimização de memória na réplica primária ou secundária. Você deve monitorar o desempenho de consulta e os planos na réplica secundária e atualizar manualmente as estatísticas na réplica primária quando necessário. No entanto, as estatísticas ausentes são criadas automaticamente na réplica primária e secundária.  
  
 Para obter mais informações sobre estatísticas do SQL Server, veja [Estatísticas](../../../relational-databases/statistics/statistics.md).  
  
 **Nesta seção:**  
  
-   [Estatísticas permanentes obsoletas em bancos de dados secundários](#StalePermStats)  
  
-   [Limitações e restrições](#StatsLimitationsRestrictions)  
  
####  <a name="StalePermStats"></a> Estatísticas permanentes obsoletas em bancos de dados secundários  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] detecta quando as estatísticas permanentes em um banco de dados secundário estão obsoletas. Mas alterações não podem ser feitas nas estatísticas permanentes, exceto por alterações no banco de dados primário. Para a otimização das consultas, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cria estatísticas temporárias para tabelas baseadas em disco no banco de dados secundário e usa essas estatísticas em vez das estatísticas permanentes obsoletas.  
  
 Quando as estatísticas permanentes são atualizadas no banco de dados primário, elas persistem automaticamente no banco de dados secundário. Em seguida, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa as estatísticas permanentes atualizadas, que são mais atuais que as estatísticas temporárias.  
  
 Se o grupo de disponibilidade passar por failover, as estatísticas temporárias serão excluídas em todas as réplicas secundárias.  
  
####  <a name="StatsLimitationsRestrictions"></a> Limitações e restrições  
  
-   Como as estatísticas temporárias são armazenadas em **tempdb**, uma reinicialização do serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] faz com que todas as estatísticas temporárias desapareçam.  
  
-   O sufixo _readonly_database_statistic fica reservado para estatísticas geradas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Você não pode usar esse sufixo na criação de estatísticas em um banco de dados primário. Para obter mais informações, consulte [Statistics](../../../relational-databases/statistics/statistics.md).  
  
##  <a name="bkmk_AccessInMemTables"></a> Acessando tabelas com otimização de memória em uma réplica secundária  
 Os níveis de isolamento de transação que podem ser usados com tabelas com otimização de memória em uma réplica secundária são os mesmos que na réplica primária. A recomendação é definir o nível de isolamento no nível de sessão como READ COMMITTED e definir a opção no nível de banco de dados MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT como ON. Por exemplo:  
  
```sql  
ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
GO  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
GO  
SELECT SUM(UnitPrice*OrderQty)   
FROM Sales.SalesOrderDetail_inmem  
GO  
  
```  
  
##  <a name="bkmk_CapacityPlanning"></a> Considerações sobre o planejamento de capacidade  
  
-   No caso de tabelas baseadas em disco, as réplicas secundárias legíveis podem exigir espaço no **tempdb** por duas razões:  
  
    -   O nível de isolamento do instantâneo copia as versões de linha no **tempdb**.  
  
    -   As estatísticas temporárias para bancos de dados secundários são criadas e mantidas no **tempdb**. As estatísticas temporárias podem causar um leve aumento no tamanho do **tempdb**. Para obter informações, veja [Estatísticas para bancos de dados somente leitura](#Read-OnlyStats), mais adiante nesta seção.  
  
-   Quando você configura o acesso de leitura para uma ou mais réplicas secundárias, os bancos de dados primários adicionam 14 bytes de sobrecarga nas linhas de dados excluídas, modificadas ou inseridas para armazenar ponteiros para versões de linha nos bancos de dados secundários para tabelas baseadas em disco. Essa sobrecarga de 14 bytes transferida aos bancos de dados secundários. Como a sobrecarga de 14 bytes é adicionada a linhas de dados, podem ocorrer divisões de página.  
  
     Os dados de versão de linha não são gerados pelos bancos de dados primários. Em vez disso, os bancos de dados secundários geram as versões de linha. No entanto, o controle de versão de linha aumenta o armazenamento de dados nos bancos de dados primários e secundários.  
  
     A adição dos dados de versão de linha depende do isolamento de instantâneo ou da configuração de nível de isolamento do instantâneo (RCSI) confirmada por leitura no banco de dados primário. A tabela abaixo descreve o comportamento do controle de versão em um banco de dados secundário legível em configurações diferentes para tabelas baseadas em disco.  
  
    |Réplica secundária legível?|O isolamento do instantâneo ou nível RCSI está habilitado?|Banco de dados primário|Banco de dados secundário|  
    |---------------------------------|-----------------------------------------------|----------------------|------------------------|  
    |Não|Não|Nenhuma versão de linha ou sobrecarga de 14 bytes|Nenhuma versão de linha ou sobrecarga de 14 bytes|  
    |Não|Sim|Versões de linha e sobrecarga de 14 bytes|Nenhuma versão de linha, mas sobrecarga de 14 bytes|  
    |Sim|Não|Nenhuma versão de linha, mas sobrecarga de 14 bytes|Versões de linha e sobrecarga de 14 bytes|  
    |Sim|Sim|Versões de linha e sobrecarga de 14 bytes|Versões de linha e sobrecarga de 14 bytes|  
  
##  <a name="bkmk_RelatedTasks"></a> Tarefas relacionadas  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
-   [Exibir as propriedades da réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Blog da equipe do Always On do SQL Server: o blog oficial da equipe do Always On do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativos &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [Estatísticas](../../../relational-databases/statistics/statistics.md)  
  
  
