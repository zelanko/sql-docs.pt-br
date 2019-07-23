---
title: Habilitar um banco de dados para replicação (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b70b52951bd5da8abe16d3276d8608ff37f4924e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128265"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>Habilitar um banco de dados para replicação (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
Um banco de dados está implicitamente habilitado para replicação quando um membro da função do servidor fixa **sysadmin** cria uma publicação no Assistente para Novas Publicações. Um membro da função de servidor fixa **sysadmin** também pode habilitar um banco de dados explicitamente para replicação, assim, um membro da função de banco de dados fixa **db_owner** pode criar uma ou mais publicações naquele banco de dados. Para habilitar um banco de dados explicitamente, use a página **Bancos de Dados de Publicação** da caixa de diálogo **Propriedades do Publicador – \<Publisher>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
## <a name="using-sql-server-management-studio-ssms"></a>Usando o SSMS (SQL Server Management Studio)
  
1.  Na página **Bancos de Dados de Publicação** da caixa de diálogo **Propriedades do Publicador – \<Publisher>** , selecione a caixa de seleção **Transacional** e/ou **Mesclagem** para cada banco de dados que deseja replicar. Selecione **Transacional** para habilitar o banco de dados para replicação de instantâneo.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
## <a name="using-transact-sql-t-sql"></a>Usar o Transact-SQL (T-SQL)
Você pode habilitar um banco de dados para replicação com o seguinte código do Transact-SQL: 

```sql
USE master
EXEC sp_replicationdboption @dbname = 'AdventureWorks2017',
@optname = 'publish',
@value = 'true'
GO
```

Para desabilitar a publicação, defina o @value='false'. 
