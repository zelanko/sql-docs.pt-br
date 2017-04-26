---
title: "Recuperação de desastre do WSFC por meio de quorum forçado (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: 6cefdc18-899e-410c-9ae4-d6080f724046
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f79077825cabd60fa12cd906ff375d149b29a7d3
ms.lasthandoff: 04/11/2017

---
# <a name="wsfc-disaster-recovery-through-forced-quorum-sql-server"></a>Recuperação de desastres WSFC por meio de quorum forçado (SQL Server)
  A falha de quorum normalmente é causada por um desastre sistêmico ou uma falha de comunicações persistente que envolve vários nós no cluster WSFC.  A intervenção manual é necessária para a recuperação de uma falha de quorum.  
  
-   **Before you start:**  [Prerequisites](#Prerequisites), [Security](#Security)  
  
-   **WSFC Disaster Recovery through the Forced Quorum Procedure** [WSFC Disaster Recovery through the Forced Quorum Procedure](#Main)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Antes de iniciar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 O Procedimento de Quorum Forçado supõe que um quorum íntegro existia antes da falha de quorum.  
  
> [!WARNING]  
>  O usuário deve estar bem-informado sobre os conceitos e as interações do Windows Server Failover Clustering, Modelos de Quorum do WSFC, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]e a configuração de implantação específica do ambiente.  
>   
>  Para obter mais informações, veja:  [WSFC (Clustering de Failover do Windows Server) com SQL Server](http://msdn.microsoft.com/library/hh270278\(v=SQL.110\).aspx), [Configuração de modos de quorum WSFC e votação (SQL Server)](http://msdn.microsoft.com/library/hh270280\(v=SQL.110\).aspx)  
  
###  <a name="Security"></a> Segurança  
 O usuário deve ser uma conta de domínio que seja membro do grupo Administradores local em cada nó do cluster WSFC.  
  
##  <a name="Main"></a> Recuperação de desastres WSFC por meio do procedimento de quorum forçado  
 Lembre-se de que a falha de quorum deixa offline todos os serviços clusterizados, instâncias do SQL Server e [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]no cluster WSFC, pois o cluster, conforme configurado, não pode garantir tolerância a falhas no nível de nó.  Uma falha de quorum significa que os nós de votação íntegros no cluster WSFC não atendem mais ao modelo de quorum. Alguns nós podem ter falhado totalmente e outros podem ter apenas desligado o serviço WSFC e, nesse caso, são íntegros, exceto pela perda da capacidade de comunicação com um quorum.  
  
 Para colocar o cluster WSFC novamente online, corrija a causa raiz da falha de quorum na configuração existente, recupere os bancos de dados afetados quando necessário e, se desejar, reconfigure os nós restantes no cluster WSFC para refletir a topologia de cluster sobrevivente.  
  
 Você pode usar o procedimento *quorum forçado* em um nó de cluster WSFC para substituir o controle de segurança que colocou o cluster offline.  Isso indica efetivamente ao cluster que deve suspender as verificações de votação de quorum e permite que você coloque os recursos de cluster WSFC e SQL Server novamente online, em quaisquer nós no cluster.  
  
 Esse tipo de processo de recuperação de desastres deve incluir as seguintes etapas:  
  
#### <a name="to-recover-from-quorum-failure"></a>Para recuperar de falha de quorum:  
  
1.  **Determine o escopo da falha.** Identifique quais grupos de disponibilidade ou instâncias do SQL Server estão sem resposta, quais nós de cluster estão online e disponíveis para uso pós-desastre, e examine os logs de eventos do Windows e os logs do sistema SQL Server.  Quando for prático, você deve preservar dados forenses e os logs do sistema para análise futura.  
  
    > [!TIP]  
    >  Em uma instância responsiva do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], você pode obter informações sobre a integridade de grupos de disponibilidade que possuam uma réplica de disponibilidade na instância de servidor local consultando a DMV (exibição de gerenciamento dinâmico) [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md) .  
  
2.  **Inicie o cluster WSFC usando o quorum forçado em um único nó.** Identifique um nó com um número mínimo de falhas de componente, que não seja o desligamento do serviço de cluster WSFC.  Verifique se este nó pode se comunicar com a maioria dos demais nós.  
  
     Neste nó, force manualmente o cluster a ficar online usando o procedimento de quorum forçado.  Para minimizar a potencial perda de dados, selecione um nó recém-hospedado em uma réplica primária de grupo de disponibilidade.  
  
     Para obter mais informações, consulte:  [Forçar um Cluster WSFC a Iniciar Sem um Quorum](http://msdn.microsoft.com/library/hh270275\(v=SQL.110\).aspx)  
  
    > [!NOTE]  
    >  A configuração de quorum forçada tem um efeito amplo no cluster de bloquear verificações de quorum até que o cluster WSFC lógico alcance uma maioria de votos e automaticamente passe para um modo de operação de quorum normal.  
  
3.  **Inicie normalmente o serviço WSFC em cada nó íntegro, um de cada vez.** Você não precisará especificar a opção de quorum forçado quando iniciar o serviço de cluster nos outros nós.  
  
     Como o serviço WSFC em cada nó volta a ficar online, ele negocia com os outros nós íntegros para sincronizar o novo estado de configuração do cluster.  Lembre-se de fazer isso em um nó de cada vez para impedir que situações de competição em potencial resolvam o último estado conhecido do cluster.  
  
    > [!WARNING]  
    >  Verifique se cada nó iniciado pode se comunicar com os outros nós recém-colocados online.  Considere a desabilitação do serviço WSFC nos outros nós.  Caso contrário, você corre o risco de criar mais de um conjunto de nó de quorum; este é um cenário de separação. Se seus resultados na etapa 1 forem precisos, isso não deve ocorrer.  
  
4.  **Aplique o novo modo de quorum e a configuração de voto de nó.** Se forçar o quorum reiniciar com êxito todos os nós no cluster e a causa raiz da falha do quorum for corrigida, não serão necessárias alterações no modo de quorum original e na configuração de voto de nó.  
  
     Caso contrário, você deve avaliar o nó de cluster recém-recuperado e a topologia de réplica de disponibilidade, e alterar o modo de quorum e as atribuições de voto para cada nó conforme apropriado. Nós não recuperados devem ser definidos como offline ou ter seu nó definido como zero.  
  
    > [!TIP]  
    >  Neste momento, os nós e as instâncias do SQL Server no cluster podem parecer terem voltado à operação normal.  Entretanto, talvez ainda não exista um quorum íntegro.  Usando o Gerenciador de Cluster de Failover ou o Painel AlwaysOn no SQL Server Management Studio ou os DMVs apropriados, verifique se um quorum foi restaurado.  
  
5.  **Recupere réplicas de banco de dados de grupo de disponibilidade, conforme necessário.** Bancos de dados de grupo de não disponibilidade devem se recuperados e voltar a ficar online por si próprios, como parte do processo normal de inicialização do SQL Server.  
  
     Você pode minimizar a perda de dados em potencial e o tempo de recuperação para as réplicas de grupo de disponibilidade, colocando-os novamente online nesta sequência: réplica primária, réplicas secundárias síncronas, réplicas secundárias assíncronas.  
  
6.  **Repare ou substitua componentes com falha e revalide o cluster.** Agora que você se recuperou do desastre inicial e da falha de quorum, deve reparar ou substituir os nós com falhas e ajustar as configurações de WSFC e AlwaysOn relacionadas adequadamente.  Isso pode incluir a remoção de réplicas de grupo de disponibilidade, mesclando nós do cluster ou simplificando e reinstalando o software em um nó.  
  
     Você deve reparar ou remover todas as réplicas de disponibilidade com falha.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não truncará o log de transação após o último ponto conhecido da réplica de disponibilidade mais afastada.   Se uma réplica com falha não for reparada ou removida do grupo de disponibilidade, os logs de transação crescerão e você correrá o risco de ficar sem espaço de log de transação nas outras réplicas.  
  
    > [!NOTE]  
    >  Se você executar o Assistente para validar a configuração do WSFC, quando um ouvinte do grupo de disponibilidade existir no cluster WSFC, o assistente gerará a mensagem de aviso incorreto a seguir:  
    >   
    >  “A propriedade RegisterAllProviderIP para nome de rede 'Name:<network_name>' é definida como 1. Para a configuração do cluster atual, este valor deve ser definido como 0.”  
    >   
    >  Ignore esta mensagem.  
  
7.  **Repita a etapa 4 conforme necessário.** A meta é restabelecer o nível apropriado de tolerância a falhas e a alta disponibilidade para operações íntegras.  
  
8.  **Conduza a análise de RPO/RTO.** Você deve analisar logs de sistema do SQL Server, carimbos de data/hora de bancos de dados e logs de eventos do Windows para determinar a causa raiz da falha e para documentar as experiências reais de ponto de recuperação e de tempo de recuperação.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Forçar um Cluster WSFC a Iniciar Sem um Quorum](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Exibir configurações de NodeWeight de quorum de cluster](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)  
  
-   [Definir configurações de NodeWeight de quorum de cluster](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)  
  
-   [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Exibir eventos e logs de um cluster de failover](http://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Cluster de failover Get-ClusterLog do cmdlet](http://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Consulte também  
 [WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  
