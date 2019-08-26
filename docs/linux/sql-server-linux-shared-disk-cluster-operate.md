---
title: Operar a instância de cluster de failover – SQL Server em Linux
description: Este artigo explica como operar uma FCI (instância de cluster de failover) do SQL Server no Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: a29d1d61b628126d03458fced964bde7c92b6d68
ms.sourcegitcommit: 71b9ebb511c68e0c9cb32a860a443803d2cb58f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2019
ms.locfileid: "68032290"
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>Operar a instância de cluster de failover – SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como operar uma FCI (instância de cluster de failover) do SQL Server no Linux. Se você não tiver criado uma FCI do SQL Server no Linux, confira [Configurar uma instância de cluster de failover – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure.md). 

## <a name="failover"></a>Failover

O failover para FCIs é semelhante a um WSFC (cluster de failover do Windows Server). Se o nó de cluster que hospeda a FCI apresentar algum tipo de falha, a FCI deverá fazer o failover automaticamente para outro nó. Ao contrário de um WSFC, não há como definir proprietários preferenciais; portanto, o Pacemaker escolhe o nó que será o novo host para a FCI.

Há ocasiões em que você pode desejar fazer o failover manual da FCI para outro nó. O processo não é o mesmo que com FCIs em um WSFC. Em um WSFC, você faz failover de recursos no nível da função. No Pacemaker, você escolhe um recurso a ser movido e, supondo que todas as restrições estejam corretas, todo o resto também será movido. 

A forma de failover depende da distribuição do Linux. Siga as instruções da distribuição do Linux.

- [RHEL ou Ubuntu](#-manual-failover-rhel-or-ubuntu)
- [SLES](#-manual-failover-sles)

## <a name = "#-manual-failover-rhel-or-ubuntu"></a> Failover manual (RHEL ou Ubuntu)

Para fazer um failover manual, em servidores do RHEL (Red Hat Enterprise Linux) ou do Ubuntu, execute as etapas a seguir.
1.  Emita o seguinte comando: 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName> é o nome do recurso do Pacemaker para a FCI do SQL Server.

   \<NewHostNode> é o nome do nó de cluster no qual você deseja hospedar a FCI. 

   Você não receberá nenhuma confirmação.

2.  Durante um failover manual, o Pacemaker cria uma restrição de localização no recurso que foi escolhido para ser movido manualmente. Para ver essa restrição, execute `sudo pcs constraint`.

3.  Após a conclusão do failover, remova a restrição emitindo `sudo pcs resource clear <FCIResourceName>`. 

\<FCIResourceName> é o nome do recurso do Pacemaker para a FCI. 

## <a name = "#-manual-failover-sles"></a> Failover manual (SLES)


No SLES (SUSE Linux Enterprise Server), use o comando `migrate` para fazer failover manual de uma FCI do SQL Server. Por exemplo:

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName> é o nome do recurso para a instância de cluster de failover. 

\<NewHostNode> é o nome do novo host de destino. 


<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

--->

## <a name="next-steps"></a>Next Steps

- [Configurar a instância de cluster de failover – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
