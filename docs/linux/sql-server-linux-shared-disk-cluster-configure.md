---
title: Configurar o cluster de disco compartilhado para o SQL Server no Linux | Microsoft Docs
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 92b4cb2500d4fd8a1643488593c40e97b1ff6454
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---

# <a name="shared-disk-cluster-for-sql-server-on-linux"></a>Cluster de discos compartilhados para o SQL Server no Linux

Você pode configurar um cluster de alta disponibilidade de armazenamento compartilhado com Linux para permitir que a instância do SQL Server para failover de um nó para outro. Em um cluster típico de dois ou mais servidores estão conectados ao armazenamento compartilhado. Os servidores são os nós do cluster. Clusters de failover fornecem proteção no nível da instância para melhorar o tempo de recuperação, para permitir que o SQL Server para realizar failover entre dois ou mais nós. Etapas de configuração dependem a distribuição de Linux e soluções de cluster. A tabela a seguir identifica as etapas específicas para soluções de cluster validado.  

|Distribuição |Tópico 
|----- |-----
|**Red Hat Enterprise Linux com o complemento HA** |[Configurar](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operar](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server com o complemento HA** |[Configurar](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>Próximas etapas


