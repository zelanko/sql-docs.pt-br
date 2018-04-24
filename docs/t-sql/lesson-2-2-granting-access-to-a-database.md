---
title: Concedendo acesso a um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9f478eb25f7dd6be99a9576831a704fc4f9f1854
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-2-2---granting-access-to-a-database"></a>Lição 2-2: Concedendo acesso a um banco de dados
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
Mary agora tem acesso a esta instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas não tem permissão para acessar os bancos de dados. Ela não tem acesso nem mesmo ao seu banco de dados padrão **TestData** até que você a autorize como usuária de um banco de dados.  
  
Para conceder acesso à Mary, alterne para o banco de dados **TestData** e, em seguida, use a instrução CREATE USER para mapear o logon dela para um usuário nomeado Mary.  
  
### <a name="to-create-a-user-in-a-database"></a>Para criar um usuário em um banco de dados  
  
1.  Digite e execute as instruções a seguir (substituindo `computer_name` pelo nome de seu computador) para conceder acesso à `Mary` ao banco de dados `TestData` .  
  
    ```  
    USE [TestData];  
    GO  
  
    CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
    GO  
  
    ```  
  
    Agora, Mary tem acesso ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e ao banco de dados `TestData` .  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[criando exibições e procedimentos armazenados](../t-sql/lesson-2-3-creating-views-and-stored-procedures.md)  
  
  
  
