---
title: Concedendo acesso a um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8a4d07c99cfe060962842e7d13bafe121c731cf8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37204498"
---
# <a name="granting-access-to-a-database"></a>concedendo acesso a um banco de dados
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
 [Criar exibições e procedimentos armazenados](lesson-2-3-creating-views-and-stored-procedures.md)  
  
  
