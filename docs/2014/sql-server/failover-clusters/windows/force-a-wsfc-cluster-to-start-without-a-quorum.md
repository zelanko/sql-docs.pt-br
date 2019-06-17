---
title: Forçar um cluster WSFC a iniciar sem um quorum | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: 4a121375-7424-4444-b876-baefa8fe9015
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 674f6f53610c8bf864aba5a2b5c7310c10f969c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049479"
---
# <a name="force-a-wsfc-cluster-to-start-without-a-quorum"></a>Forçar um cluster WSFC para iniciar sem um quorum
  Este tópico descreve como forçar um nó de cluster WSFC (Windows Server Failover Clustering) a iniciar sem um quorum.  Talvez isso seja necessário na recuperação de desastre e em cenários com várias sub-redes para recuperar dados e restabelecer totalmente a alta disponibilidade para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e instâncias de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Antes de iniciar:**  [Recomendações](#Recommendations), [segurança](#Security)  
  
-   **Para forçar um cluster a iniciar sem um quorum usando:**  [Usando o Gerenciador de Cluster de Failover](#FailoverClusterManagerProcedure), [usando o Powershell](#PowerShellProcedure), [usando Net.exe](#CommandPromptProcedure)  
  
-   **Acompanhar:**  [Acompanhar: Depois de forçar o Cluster a iniciar sem um Quorum](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de iniciar  
  
###  <a name="Recommendations"></a> Recomendações  
 Exceto nas ocasiões em que houver instruções explícitas, os procedimentos neste tópico deverão funcionar se você executá-los de qualquer nó no cluster WSFC.  No entanto, é possível obter resultados melhores e evitar problemas de rede, executando essas etapas a partir do nó que você pretende forçar a iniciar sem um quorum.  
  
###  <a name="Security"></a> Segurança  
 O usuário deve ser uma conta de domínio que seja membro do grupo Administradores local em cada nó do cluster WSFC.  
  
##  <a name="FailoverClusterManagerProcedure"></a> Usando o Gerenciador de Cluster de Failover  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>Para forçar um cluster a iniciar sem um quorum  
  
1.  Abra um Gerenciador de Cluster de Failover e conecte-se ao nó de cluster que você deseja forçar online.  
  
2.  No painel **Ações**, clique em **Forçar Início do Cluster** e em **Sim – Forçar a inicialização do cluster**.  
  
3.  No painel esquerdo, na árvore **Gerenciador de Cluster de Failover** , clique no nome do cluster.  
  
4.  No painel de resumo, confirme se o atual **configuração de Quorum** valor é:  **Aviso: Cluster está em execução no estado ForceQuorum**.  
  
##  <a name="PowerShellProcedure"></a> Usando o Powershell  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>Para forçar um cluster a iniciar sem um quorum  
  
1.  Inicie um Windows PowerShell elevado via **Executar como Administrador**.  
  
2.  Importe o módulo `FailoverClusters` para habilitar commandlets de cluster.  
  
3.  Use `Stop-ClusterNode` para assegurar que o serviço de cluster seja interrompido.  
  
4.  Use `Start-ClusterNode` com `-FixQuorum` para forçar o serviço de cluster a ser iniciado.  
  
5.  Use `Get-ClusterNode` com `-Propery NodeWieght = 1` para definir o valor que garanta que o nó é um membro votante do quorum.  
  
6.  Gere as propriedades de nó de cluster em um formato legível.  
  
### <a name="example-powershell"></a>Exemplo (Powershell)  
 O exemplo a seguir força o serviço de cluster de nó AlwaysOnSrv02 a iniciar sem um quorum, define o `NodeWeight = 1`e enumera o status de nó de cluster a partir do nó recém-forçado.  
  
```powershell  
Import-Module FailoverClusters  
  
$node = "AlwaysOnSrv02"  
Stop-ClusterNode -Name $node  
Start-ClusterNode -Name $node -FixQuorum  
  
(Get-ClusterNode $node).NodeWeight = 1  
  
$nodes = Get-ClusterNode -Cluster $node  
$nodes | Format-Table -property NodeName, State, NodeWeight  
  
```  
  
##  <a name="CommandPromptProcedure"></a> Usando Net.exe  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>Para forçar um cluster a iniciar sem um quorum  
  
1.  Use a Área de Trabalho Remota para se conectar ao nó de cluster que você deseja forçar online.  
  
2.  Inicie um Prompt de Comando elevado via **Executar como Administrador**.  
  
3.  Use **net.exe** para assegurar que o serviço de cluster local seja interrompido.  
  
4.  Use **net.exe** com `/forcequorum` para forçar o início do serviço de cluster local.  
  
### <a name="example-netexe"></a>Exemplo (Net.exe)  
 O exemplo a seguir força um serviço de cluster de nó a iniciar sem um quorum, define o `NodeWeight = 1`e enumera o status de nó de cluster a partir do nó recém-forçado.  
  
```ms-dos  
net.exe stop clussvc  
net.exe start clussvc /forcequorum  
```  
  
##  <a name="FollowUp"></a> Acompanhamento: Depois de forçar o Cluster a iniciar sem um Quorum  
  
-   Você deve reavaliar e reconfigurar valores de NodeWeight para construir corretamente um novo quorum antes de colocar os outros nós online novamente. Caso contrário, o cluster talvez fique offline novamente.  
  
     Para obter mais informações, veja [Configuração de modos de quorum WSFC e votação &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md).  
  
-   Os procedimentos neste tópico constituem apenas uma etapa para a colocação do cluster WSFC online novamente se uma falha de quorum não planejada por ocorrer.  Talvez você também queira executar etapas adicionais para impedir que outros nós de cluster WSFC interfiram na nova configuração do quorum.  
  
-   Outros recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , como [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], espelhamento de banco de dados e envio de logs, também podem exigir ações subsequentes para recuperar dados e restabelecer totalmente a alta disponibilidade.  
  
     **Para obter mais informações, consulte:**  
  
     [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
     [Forçar serviço em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)  
  
     [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](../../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Exibir eventos e logs de um cluster de failover](https://technet.microsoft.com/en-us/library/cc772342\(WS.10\).aspx)  
  
-   [Cluster de failover Get-ClusterLog do cmdlet](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Consulte também  
 [Recuperação de desastres do WSFC por meio de quorum forçado &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)   
 [Definir configurações de NodeWeight de quorum de cluster](configure-cluster-quorum-nodeweight-settings.md)   
 [Cmdlets de cluster de failover no Windows PowerShell listados por foco de tarefa](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
