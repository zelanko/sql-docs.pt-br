---
title: "concedendo acesso a um objeto de banco de dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "concedendo acesso a objetos de banco de dados"
ms.assetid: a44d9bbf-f58e-4734-b7f4-eb3b492b777b
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# concedendo acesso a um objeto de banco de dados
Como administrador, você pode executar SELECT na tabela **Produtos** e na exibição **vw_Names**, além de executar o procedimento **pr_Names**; no entanto, Marina não pode. Para conceder as permissões necessárias à Mary, use a instrução GRANT.  
  
### Título do procedimento  
  
1.  Execute a instrução a seguir para conceder a `Mary` a permissão `EXECUTE` para o procedimento armazenado `pr_Names` .  
  
    ```  
    GRANT EXECUTE ON pr_Names TO Mary;  
    GO  
    ```  
  
Nesse cenário, Mary pode acessar apenas a tabela **Products** usando o procedimento armazenado. Para que Mary possa executar a instrução SELECT na exibição, você também deve executar `GRANT SELECT ON vw_Names TO Mary`. Para remover acesso a objetos de banco de dados, use a instrução REVOKE.  
  
> [!NOTE]  
> Se a tabela, a exibição e o procedimento armazenado não pertencerem ao mesmo esquema, a concessão de permissões ficará mais complexa.  
  
## Sobre GRANT  
É preciso ter permissão EXECUTE para executar um procedimento armazenado. É preciso ter permissões SELECT, INSERT, UPDATE e DELETE para acessar e alterar dados. A instrução GRANT também é usada para outras permissões, como permissão para criar tabelas.  
  
## Próxima tarefa da lição  
[resumo: configurando permissões em objetos de banco de dados](../t-sql/summary-configuring-permissions-on-database-objects.md)  
  
## Consulte também  
[GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md)  
[REVOKE &#40;Transact-SQL&#41;](../t-sql/statements/revoke-transact-sql.md)  
  
  
  
