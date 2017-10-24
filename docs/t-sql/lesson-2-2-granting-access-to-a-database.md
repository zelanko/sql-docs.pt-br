---
title: Concedendo acesso a um banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 30de5de3d238905802e80d433c2df7deaf058929
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-2---granting-access-to-a-database"></a>Lição 2-2-conceder acesso a um banco de dados
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
  
  
  

