---
title: "Habilitar um banco de dados para replicação (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c7ef152a590558e5831b36bed7f5736186e64fa1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>Habilitar um banco de dados para replicação (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Um banco de dados está implicitamente habilitado para replicação quando um membro da função de servidor fixa **sysadmin** cria uma publicação no Assistente para Novas Publicações. Um membro da função de servidor fixa **sysadmin** também pode habilitar um banco de dados explicitamente para replicação, assim, um membro da função de banco de dados fixa **db_owner** pode criar uma ou mais publicações naquele banco de dados. Para habilitar um banco de dados explicitamente, use a página **Bancos de Dados de Publicação** da caixa de diálogo **Propriedades do Publicador – \<Publisher>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
### <a name="to-enable-a-database-for-replication"></a>Para habilitar um banco de dados para replicação  
  
1.  Na página **Bancos de Dados de Publicação** da caixa de diálogo **Propriedades do Publicador – \<Publisher>**, selecione a caixa de seleção **Transacional** e/ou **Mesclagem** para cada banco de dados que deseja replicar. Selecione **Transacional** para habilitar o banco de dados para replicação de instantâneo.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
