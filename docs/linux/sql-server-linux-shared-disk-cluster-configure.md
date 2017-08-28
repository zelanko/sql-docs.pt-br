---
title: Configurar o cluster de disco compartilhado para o SQL Server no Linux | Microsoft Docs
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/23/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: b6e6cc415b01c6021a4ba7c52433543dc58a4452
ms.contentlocale: pt-br
ms.lasthandoff: 08/28/2017

---
# <a name="shared-disk-cluster-for-sql-server-on-linux"></a>Cluster de discos compartilhados para o SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Você pode configurar um cluster de alta disponibilidade de armazenamento compartilhado com Linux para permitir que a instância do SQL Server para failover de um nó para outro. Em um cluster típico de dois ou mais servidores estão conectados ao armazenamento compartilhado. Os servidores são os nós do cluster. Clusters de failover fornecem proteção no nível da instância para melhorar o tempo de recuperação, para permitir que o SQL Server para realizar failover entre dois ou mais nós. Etapas de configuração dependem a distribuição de Linux e soluções de cluster. A tabela a seguir identifica as etapas específicas para soluções de cluster validado.  

|Distribuição |Tópico 
|----- |-----
|**Red Hat Enterprise Linux com o complemento HA** |[Configurar](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operar](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server com o complemento HA** |[Configurar](sql-server-linux-shared-disk-cluster-sles-configure.md)

