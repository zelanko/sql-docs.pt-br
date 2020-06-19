---
title: Usar o Assistente para Fazer Failover de Grupo de Disponibilidade (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.failoverwizard.progress.f1
- sql12.swb.failoverwizard.f1
- sql12.swb.failoverwizard.selectnewprimary.f1
- sql12.swb.failoverwizard.confirmdataloss.f1
- sql12.swb.failoverwizard.connecttoreplicas.f1
helpviewer_keywords:
- failover [SQL Server], failover
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], configuring
ms.assetid: 4a602584-63e4-4322-aafc-5d715b82b834
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b13d15da19194e1715ba45a4b5d12e3f74a1d395
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936237"
---
# <a name="use-the-fail-over-availability-group-wizard-sql-server-management-studio"></a>Usar o Assistente para Grupo de Disponibilidade de Failover (SQL Server Management Studio)
  Este tópico descreve como fazer um failover manual planejado ou um failover manual forçado (failover forçado) em um grupo de disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Um grupo de disponibilidade faz failover no nível de uma réplica de disponibilidade. Se você fizer failover em uma réplica secundária no estado SYNCHRONIZED, o assistente fará um failover manual planejado (sem perda de dados). Se você fizer failover em uma réplica secundária no estado UNSYNCHRONIZED ou NOT SYNCHRONIZING, o assistente executará um failover manual forçado, também conhecido como *failover forçado* (com possível perda de dados). As duas formas de failover manual fazem a transição da réplica secundária à qual você está conectado para a função primária. Um failover manual planejado faz a transição da réplica primária antiga para a função secundária. Após um failover forçado, quando a réplica primária antiga ficar online, ela fará a transição para a função secundária.  
  


  
-   **[!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]Pages**  
  
     [Página Selecionar Nova Réplica Primária](#SelectNewPrimaryReplica) (posteriormente neste tópico)  
  
     [Página Conectar à Réplica](#ConnectToReplica) (posteriormente neste tópico)  
  
     [Página Confirmar Potencial Perda de Dados](#ConfirmPotentialDataLoss) (posteriormente neste tópico)  
  
     [Página de resumo &#40;assistentes do grupo de disponibilidade AlwaysOn&#41;](summary-page-always-on-availability-group-wizards.md)  
  
     [Página de progresso &#40;assistentes do grupo de disponibilidade AlwaysOn&#41;](progress-page-always-on-availability-group-wizards.md)  
  
     [Página de resultados &#40;assistentes do grupo de disponibilidade AlwaysOn&#41;](results-page-always-on-availability-group-wizards.md)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
 Antes de seu primeiro failover manual planejado, consulte a seção "Antes de começar" em [Executar um failover manual planejado de um grupo de disponibilidade &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md).  
  
 Antes do primeiro failover forçado, consulte as seções "Antes de começar" e "Acompanhamento: tarefas essenciais depois de um failover forçado" em [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Um comando de failover é retornado assim que a réplica secundária de destino aceitar o comando. No entanto, a recuperação de banco de dados ocorre de forma assíncrona depois que o grupo de disponibilidade terminar o failover.  
  
-   A consistência do banco de dados entre bancos de dados dentro do grupo de disponibilidade não é mantida no failover.  
  
    > [!NOTE]  
    >  Não há suporte para transações entre bancos de dados e transações distribuídas no [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obter mais informações, consulte [Transações envolvendo todos os bancos de dados sem suporte para espelhamento de banco de dados ou Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](transactions-always-on-availability-and-database-mirroring.md).  
  
###  <a name="prerequisites-for-using-the-failover-availability-group-wizard"></a><a name="Prerequisites"></a>Pré-requisitos para usar o assistente de grupo de disponibilidade de failover  
  
-   Você deve estar conectado à instância de servidor que hospeda uma réplica de disponibilidade atualmente disponível.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para usar o Assistente de Grupo de Disponibilidade de Failover**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda uma réplica secundária do grupo de disponibilidade que precisa passar por failover e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Para iniciar o Assistente de Grupo de Disponibilidade de Failover, clique com o botão direito do mouse no grupo de disponibilidade que passará por failover e selecione **Failover**.  
  
4.  As informações apresentadas pela página **Introdução** variarão de acordo com a elegibilidade de qualquer réplica secundária para um failover planejado. Se esta página informar "**Faça um failover planejado para este grupo de disponibilidade**", você poderá fazer o failover do grupo de disponibilidade sem perda de dados.  
  
5.  Na página **Selecionar Nova Réplica Primária** , você pode exibir o status da réplica primária atual e do quórum WSFC, antes de escolher a réplica secundária que se tornará a nova réplica primária (o *destino de failover*). Em um failover manual planejado, selecione uma réplica secundária cujo valor de **Prontidão de Failover** é "**Sem perda de dados**". Em um failover forçado, para todos os destinos possíveis de failover, este valor será "**Perda de dados, Avisos (***#***)**", em que *#* indica o número de avisos que existem para uma réplica secundária específica. Para exibir os avisos de um destino de failover específico, clique em seu valor de "Prontidão de Failover".  
  
     Para obter mais informações, consulte [Página Selecionar Nova Réplica Primária](#SelectNewPrimaryReplica), posteriormente neste tópico.  
  
6.  Na página **Conectar à Réplica** , conecte-se ao destino de failover. Para obter mais informações, consulte [Página Conectar à Réplica](#ConnectToReplica), posteriormente neste tópico.  
  
7.  Se você estiver executando um failover forçado, o assistente exibirá a página **Confirmar Potencial Perda de Dados** . Para continuar com o failover, você deve selecionar **Clique aqui para confirmar o failover com potencial perda de dados**. Para obter mais informações, consulte[Página Confirmar Potencial Perda de Dados](#ConfirmPotentialDataLoss), posteriormente neste tópico.  
  
8.  Na página **Resumo** , revise as implicações do failover na réplica secundária selecionada.  
  
     Se você estiver satisfeito com suas seleções, opcionalmente, clique em **script** para criar um script das etapas que o assistente executará. Em seguida, para fazer failover do grupo de disponibilidade na réplica secundária selecionada, clique em **Concluir**.  
  
9. A página **Progresso** exibe o progresso do failover do grupo de disponibilidade.  
  
10. Quando a operação de failover terminar, a página **Resultados** exibirá o resultado. Quando o assistente for concluído, clique em **Fechar** para sair.  
  
     Para obter mais informações, consulte [Página Resultados &#40;Assistentes do Grupo de Disponibilidade AlwaysOn&#41;](results-page-always-on-availability-group-wizards.md).  
  
11. Após um failover forçado, consulte a seção “Acompanhamento: após um failover forçado” em [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).  
  
## <a name="help-for-pages-that-are-exclusive-to-this-wizard"></a>Ajuda para páginas que são exclusivas deste assistente  
 Esta seção descreve as páginas que são exclusivas do [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)].  
  
 
  
 As outras páginas deste assistente compartilham a ajuda com um ou mais dos outros assistentes de grupos de disponibilidade AlwaysOn e são documentadas em tópicos de ajuda F1 separados.  
  
###  <a name="select-new-primary-replica-page"></a><a name="SelectNewPrimaryReplica"></a>Página Selecionar nova réplica primária  
 Esta seção descreve as opções da página **Selecionar Nova Réplica primária** . Use esta página para selecionar a réplica secundária (destino de failover) na qual o grupo de disponibilidade fará o failover. Essa réplica se tornará a nova réplica primária.  
  
#### <a name="page-options"></a>Opções da página  
 **Réplica Primária Atual**  
 Exibe o nome da réplica primária atual, caso ela esteja online.  
  
 **Status da Réplica Primária**  
 Exibe o status da réplica primária atual, caso ela esteja online.  
  
 **Status do Quorum**  
 Exibe o status do quorum WSFC da réplica de disponibilidade:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Quorum normal**|O cluster foi iniciado com quorum normal.|  
|**Quorum forçado**|O cluster foi iniciado com quorum forçado.|  
|**Quorum desconhecido**|O status de quorum do cluster não está disponível.|  
|**Não aplicável**|O nó que hospeda a réplica de disponibilidade não tem quorum.|  
  
 Para obter mais informações, consulte [configuração de modos de quorum WSFC e votação &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md).  
  
 **Escolha uma nova réplica primária**  
 Use esta grade para selecionar uma réplica secundária para se tornar a nova réplica primária. As colunas desta grade são as seguintes:  
  
 **Instância do servidor**  
 Exibe o nome de uma instância de servidor que hospeda uma réplica secundária.  
  
 **Modo de disponibilidade**  
 Exibe o modo de disponibilidade da instância de servidor:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Confirmação síncrona**|No modo de confirmação síncrona, antes de confirmar transações, uma réplica primária de confirmação síncrona espera que uma réplica secundária de confirmação síncrona confirme que concluiu a proteção do log. O modo de confirmação síncrona garante que, quando um determinado banco de dados secundário é sincronizado com o banco de dados primário, as transações confirmadas sejam totalmente protegidas.|  
|**Confirmação assíncrona**|No modo de confirmação assíncrona, a réplica primária confirma as transações sem esperar a confirmação de que uma réplica secundária de confirmação assíncrona protegeu o log. O modo de confirmação assíncrona minimiza a latência de transações nos bancos de dados secundários, mas permite que elas atrasem os bancos de dados primários, possibilitando a perda de dados.|  
  
 Para obter mais informações, consulte [modos de disponibilidade (grupos de disponibilidade AlwaysOn)](availability-modes-always-on-availability-groups.md).  
  
 **Modo de Failover**  
 Exibe o modo de failover da instância de servidor:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Automática**|Uma réplica secundária configurada para failover automático também oferece suporte a failover manual planejado sempre que a réplica secundária é sincronizada com a réplica primária.|  
|**Manual**|Existem dois tipos de failover manual: planejado (sem perda de dados) e forçado (com possível perda de dados). Em uma réplica secundária específica, há suporte para somente um desses tipos, dependendo do modo de disponibilidade e, no modo de confirmação síncrono, o estado de sincronização da réplica secundária. Para determinar qual forma de failover manual tem suporte em uma determinada réplica secundária, consulte a coluna **Prontidão de Failover** desta grade.|  
  
 Para obter mais informações, consulte [Failover e modos de failover &#40;Grupos de Disponibilidade AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md).  
  
 **Prontidão de failover**  
 Exibe a prontidão de failover da réplica secundária:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Sem perda de dados**|Há suporte para esta réplica secundária no failover planejado. Este valor só ocorre quando uma réplica secundária no modo de confirmação síncrona está sincronizada com a réplica primária.|  
|**Perda de dados, avisos (** *#* **)**|Há suporte para esta réplica secundária no failover forçado (com possível perda de dados). Este valor ocorre sempre que a réplica secundária não está sincronizada com a réplica primária. Clique no link de avisos de perda de dados referente às informações sobre a possível perda de dados.|  
  
 **Atualizar**  
 Clique para atualizar a grade.  
  
 **Cancelar**  
 Clique para cancelar o assistente. Na página **Selecionar Nova Réplica Primária** , o cancelamento do assistente faz com que ele seja fechado sem executar nenhuma ação.  
  
###  <a name="confirm-potential-data-loss-page"></a><a name="ConfirmPotentialDataLoss"></a>Página confirmar potencial perda de dados  
 Esta seção descreve as opções da página **Confirmar Potencial Perda de dados** , que será exibida somente se você estiver executando um failover forçado. Este tópico é usado apenas pelo [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]. Use esta página para indicar se você está disposto a arriscar uma possível perda de dados para forçar o failover do grupo de disponibilidade.  
  
#### <a name="confirm-potential-data-loss-options"></a>Opções da página Confirmar Potencial Perda de Dados  
 Se a réplica secundária selecionada não estiver sincronizada com a réplica primária, o assistente exibirá um aviso informando que o failover nesta réplica secundária poderá causar perda de dados em um ou mais bancos de dados.  
  
 **Clique aqui para confirmar o failover com perda de dados potencial.**  
 Se você estiver disposto a arriscar a perda de dados para disponibilizar os bancos de dados deste grupo de disponibilidade para os usuários, clique nesta caixa de seleção. Se você não estiver disposto a arriscar a perda de dados, clique em **Anterior** para retornar à página **Selecionar Nova Réplica primária** ou em **Cancelar** para sair do assistente sem fazer failover do grupo de disponibilidade.  
  
 **Cancelar**  
 Clique para cancelar o assistente. Na página **Confirmar Potencial Perda de Dados** , o cancelamento do assistente faz com que ele seja fechado sem executar nenhuma ação.  
  
###  <a name="connect-to-replica-page"></a><a name="ConnectToReplica"></a>Página conectar à réplica  
 Esta seção descreve as opções da página **Conectar à Réplica** do [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]. Esta página só será exibida se você não estiver conectado à réplica secundária de destino. Use esta página para se conectar à réplica secundária que você selecionou como a nova réplica primária.  
  
#### <a name="page-options"></a>Opções da página  
 **Colunas da grade:**  
 **Instância do servidor**  
 Exibe o nome da instância de servidor que hospedará a réplica de disponibilidade.  
  
 **Conectado como**  
 Exibe a conta conectada à instância de servidor, após o estabelecimento da conexão. Se essa coluna exibir "**Não Conectada**" para uma determinada instância de servidor, será necessário clicar no botão **Conectar** .  
  
 **Connect**  
 Clique se essa instância de servidor estiver sendo executada sob uma conta diferente da de outras instâncias de servidor às quais você precisa se conectar.  
  
 **Cancelar**  
 Clique para cancelar o assistente. Na página **Conectar a Réplica** , o cancelamento do assistente faz com que ele seja fechado sem executar nenhuma ação.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Modos de disponibilidade (Grupos de Disponibilidade AlwaysOn)](availability-modes-always-on-availability-groups.md)   
 [Failover e modos de failover &#40;Grupos de Disponibilidade AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [Executar um failover manual planejado de um grupo de disponibilidade &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)   
 [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)   
 [Recuperação de desastres do WSFC por meio de quorum forçado &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
  
