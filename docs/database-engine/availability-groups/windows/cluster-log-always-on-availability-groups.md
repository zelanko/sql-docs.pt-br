---
title: Gerar e analisar CLUSTER.LOG para grupos de disponibilidade
description: 'Descreve como gerar e analisar o log do cluster de um grupo de disponibilidade Always On. '
ms.custom: seo-lt-2019
ms.date: 06/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a9e3c1-2a5f-4b98-a424-0ffc15d312cf
author: rothja
ms.author: jroth
ms.openlocfilehash: 4b0cd86318c4ff884ba31fed56e31202c70990ff
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896122"
---
# <a name="generate-and-analyze-the-clusterlog-for-an-always-on-availability-group"></a>Gerar e analisar o CLUSTER.LOG de um grupo de disponibilidade Always On
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Como um recurso de cluster de failover, há interações externas entre o SQL Server, o cluster do serviço WSFC (Cluster de Failover do Windows Server) e o DLL de recurso do SQL Server (hadrres.dll), que não pode ser monitorado no SQL Server. O log do WSFC, CLUSTER.LOG, pode diagnosticar problemas no cluster WSFC ou na DLL de recurso do SQL Server. 
  
## <a name="generate-cluster-log"></a>Gerar o log do cluster  
 Você pode gerar os logs do cluster de duas maneiras:  
  
1.  Use o comando `cluster /log /g` no prompt de comando. Este comando gera os logs do cluster no diretório \windows\cluster\reports em cada nó do WSFC. A vantagem desse método é que você pode especificar o nível de detalhe dos logs gerados usando a opção `/level`. A desvantagem é que você não pode especificar o diretório de destino para os logs de cluster gerados. Para obter mais informações, veja [Como criar o cluster.log no Clustering de failover do Windows Server 2008](https://techcommunity.microsoft.com/t5/failover-clustering/how-to-create-the-cluster-log-in-windows-server-2008-failover/ba-p/371283).  
  
2.  Use o cmdlet [Get-ClusterLog](https://technet.microsoft.com/library/ee461045.aspx) do PowerShell. A vantagem desse método é que você pode gerar o log do cluster em todos os nós em um diretório de destino do nó em que você executa o cmdlet. A desvantagem é que você não pode especificar o nível de detalhes dos logs gerados.  
  
 Os seguintes comandos do PowerShell geram os logs do cluster de todos os nós de cluster nos últimos 15 minutos, colocando-os no diretório atual. Execute os comandos em uma janela do PowerShell com privilégios de administrador.  
  
```powershell  
Import-Module FailoverClusters   
Get-ClusterLog -TimeSpan 15 -Destination .  
```  
  
## <a name="always-on-log-verbosity"></a>Detalhes de log do Always On  
 Você pode aumentar o nível de detalhes dos logs no CLUSTER.LOG de um grupo de disponibilidade. Para modificar o nível de detalhes, siga as etapas abaixo:  
  
1.  No menu **Iniciar**, abra o **Gerenciador de Cluster de Failover**.  
  
2.  Expanda o cluster e o nó **Serviços e aplicativos** e clique no nome do grupo de disponibilidade.  
  
3.  No painel de detalhes, clique o com botão direito do mouse no recurso do grupo de disponibilidade e clique em **Propriedades**.  
  
4.  Clique no guia **Propriedades**.  
  
5.  Modificar a propriedade **VerboseLogging**. Por padrão, a **VerboseLogging** é definida como `0`, que relata informações, avisos e erros. A **VerboseLogging** pode ser definida de `0` para `2`.  
  
6.  Clique em **OK**.  
  
7.  Clique com o botão direito do mouse no recurso do grupo de disponibilidade novamente e clique em **Colocar este recurso offline**.  
  
8.  Clique com o botão direito do mouse no recurso do grupo de disponibilidade novamente e clique em **Colocar este recurso online**.  
  
## <a name="availability-group-resource-events"></a>Eventos de recurso do grupo de disponibilidade  
 A tabela abaixo mostra os diferentes tipos de eventos que você pode ver no CLUSTER.LOG e que pertencem ao recurso do grupo de disponibilidade. Para obter mais informações sobre o RHS (Subsistema de Hospedagem de Recursos) e o RCM (Monitor de Controle de Recursos) no WSFC, veja [RHS (Subsistema de Hospedagem de Recursos) nos Clusters de Failover do Windows Server 2008](https://blogs.technet.com/b/askcore/archive/2009/11/23/resource-hosting-subsystem-rhs-in-windows-server-2008-failover-clusters.aspx).  
  
|Identificador|Fonte|Exemplo do CLUSTER.LOG|  
|----------------|------------|------------------------------|  
|Mensagens prefixadas com `[RES]` e `[hadrag]`|hadrres.dll (DLL de recurso do Always On)|00002cc4.00001264::2011/08/05-13:47:42.543 INFO [RES] Grupo de Disponibilidade do SQL Server \<ag>: `[hadrag]` Solicitação offline.<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.558 ERR [RES] Grupo de Disponibilidade do SQL Server \<ag>: `[hadrag]` Thread de Concessão encerrado<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.605 INFO [RES] Grupo de Disponibilidade do SQL Server \<ag>: `[hadrag]` Instrução SQL livre<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.902 INFO [RES] Grupo de Disponibilidade do SQL Server \<ag>: `[hadrag]` Desconectar do SQL Server|  
|Mensagens prefixadas com `[RHS]`|RHS.EXE (Subsistema de Hospedagem de Recursos, processo de host do hadrres.dll)|00000c40.00000a34::2011/08/10-18:42:29.498 INFO  [RHS] O recurso ag ficou offline. RHS está prestes a relatar o status do recurso para o RCM.|  
|Mensagens prefixadas com `[RCM]`|Monitor de controle de recursos (Serviço de cluster)|000011d0.00000f80::2011/08/05-13:47:42.480 INFO [RCM] rcm::RcmGroup::Move: Colocando o grupo 'ag' offline primeiro...<br /><br /> 000011d0.00000f80::2011/08/05-13:47:42.496 INFO  [RCM] TransitionToState(ag) Online-->OfflineCallIssued.|  
|RcmApi/ClusAPI|Uma chamada à API, o que significa basicamente que o SQL Server está solicitando a ação|000011d0.00000f80::2011/08/05-13:47:42.465 INFO  [RCM] rcm::RcmApi::MoveGroup: (ag, 2)|  
  
## <a name="debug-always-on-resource-dll-in-isolation"></a>Depurar DLL de recurso do Always On em isolamento  
 É uma melhor prática de depuração para configurar o cluster para executar a DLL de recurso do Always On (hadrres.dll) em isolamento de outras DLLs de recurso. Por padrão, o cluster WSFC executa todas as DLLs de recurso em uma única instância do rhs.exe. Isso faz com que todos os recursos do cluster compartilhem a mesma instância do rhs.exe. Quando você tenta depurar o hadrres.dll com um depurador, fazer uma pausa em um ponto de interrupção poderá fazer com que outros recursos que compartilham a instância do rhs.exe também sejam colocados em pausa. Além disso, quando você executa vários grupos de disponibilidade no mesmo cluster, a mesma configuração poderá fazer com que todos os grupos de disponibilidade sejam colocados em pausa ao fazer uma pausa em um ponto de interrupção para depurar um grupo de disponibilidade.  
  
 Para isolar um grupo de disponibilidade das outras DLLs de recurso de cluster, incluindo outros grupos de disponibilidade, faça o seguinte para executar o hadrres.dll dentro de um processo separado do rhs.exe:  
  
1.  Abra o **Editor do Registro** e navegue para a seguinte chave: HKEY_LOCAL_MACHINE\Cluster\Resources. Esta chave contém as chaves de todos os recursos, cada um com um GUID diferente.  
  
2.  Localizar a chave do recurso que contém um valor **Name** que corresponde ao nome do grupo de disponibilidade.  
  
3.  Alterar o valor **SeparateMonitor** para **1**.  
  
4.  Reinicie o serviço em cluster do grupo de disponibilidade no cluster WSFC.  
  
  
