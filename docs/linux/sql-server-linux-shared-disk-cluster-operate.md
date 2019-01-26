---
title: Operar a instância de cluster de failover – SQL Server no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: e84fc2a6032e5886c4d82d630dc36a5bde338ed1
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044502"
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>Operar a instância de cluster de failover – SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como operar uma instância de cluster de failover (FCI) do SQL Server no Linux. Se você não tiver criado um FCI do SQL Server no Linux, consulte [configurar instância de cluster de failover – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure.md). 

## <a name="failover"></a>Failover

Failover para FCIs é semelhante a um cluster de failover do Windows Server (WSFC). Se o nó de cluster que hospeda a FCI sofrer algum tipo de falha, a FCI automaticamente deve executar failover para outro nó. Ao contrário de um WSFC, não há nenhuma maneira de definir proprietários preferenciais, para que o Pacemaker seleciona o nó que será o novo host para a FCI.

Há vezes, que talvez você queira executar manualmente a FCI para outro nó. O processo não é igual ao FCIs em um WSFC. Em um WSFC, você deve fazer failover recursos no nível de função. No Pacemaker, você escolhe um recurso para mover e supondo que todas as restrições estão corretas, tudo será movido também. 

A forma de failover depende da distribuição do Linux. Siga as instruções para a sua distribuição do linux.

- [Ubuntu ou RHEL](#rhelFailover)
- [SLES](#slesFailover)

## <a name = "#rhelFailover"></a> Failover manual (Ubuntu ou RHEL)

Para executar um failover manual, onn Red Hat Enterprise Linux (RHEL) ou em servidores Ubuntu execute as etapas a seguir.
1.  Emita o seguinte comando: 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName > é o nome de recurso do Pacemaker para o FCI do SQL Server.

   \<NewHostNode > é o nome do nó de cluster que você deseja hospedar a FCI. 

   Você não terá qualquer confirmação.

2.  Durante um failover manual, Pacemaker cria uma restrição de local do recurso que foi escolhido para mover manualmente. Para ver essa restrição, execute `sudo pcs constraint`.

3.  Após o failover estiver concluído, remova a restrição emitindo `sudo pcs resource clear <FCIResourceName>`. 

\<FCIResourceName > é o nome de recursos Pacemaker para a FCI. 

## <a name = "#slesFailover"></a> Failover manual (SLES)


No Suse Linux Enterprise Server (SLES), use o `migrate` um FCI do SQL Server de comando para executar failover manual. Por exemplo:

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName > é o nome de recursos para a instância de cluster de failover. 

\<NewHostNode > é o nome do novo host de destino. 


<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

--->

## <a name="next-steps"></a>Próximas etapas

- [Configurar a instância de cluster de failover – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
