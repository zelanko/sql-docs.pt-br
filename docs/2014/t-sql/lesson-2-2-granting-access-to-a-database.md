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
ms.topic: article
helpviewer_keywords:
- database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
caps.latest.revision: 11
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2fb1db5b03e7379052e006c6c68d8cf1efd5404b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012408"
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
  
  