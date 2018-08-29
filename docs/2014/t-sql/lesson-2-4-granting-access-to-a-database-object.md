---
title: Concedendo acesso a um objeto de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- granting access to database objects
ms.assetid: a44d9bbf-f58e-4734-b7f4-eb3b492b777b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ca5d79ff168234a069a0afe321573e0c83d10dad
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43017911"
---
# <a name="granting-access-to-a-database-object"></a>concedendo acesso a um objeto de banco de dados
  Como administrador, você pode executar SELECT na tabela **Produtos** e na exibição **vw_Names**, além de executar o procedimento **pr_Names**; no entanto, Marina não pode. Para conceder as permissões necessárias à Mary, use a instrução GRANT.  
  
### <a name="procedure-title"></a>Título do procedimento  
  
1.  Execute a instrução a seguir para conceder a `Mary` a permissão `EXECUTE` para o procedimento armazenado `pr_Names` .  
  
    ```  
    GRANT EXECUTE ON pr_Names TO Mary;  
    GO  
    ```  
  
 Nesse cenário, Mary pode acessar apenas a tabela **Products** usando o procedimento armazenado. Para que Mary possa executar a instrução SELECT na exibição, você também deve executar `GRANT SELECT ON vw_Names TO Mary`. Para remover acesso a objetos de banco de dados, use a instrução REVOKE.  
  
> [!NOTE]  
>  Se a tabela, a exibição e o procedimento armazenado não pertencerem ao mesmo esquema, a concessão de permissões ficará mais complexa.  
  
## <a name="about-grant"></a>Sobre GRANT  
 É preciso ter permissão EXECUTE para executar um procedimento armazenado. É preciso ter permissões SELECT, INSERT, UPDATE e DELETE para acessar e alterar dados. A instrução GRANT também é usada para outras permissões, como permissão para criar tabelas.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Resumo: configurar permissões em objetos de banco de dados](lesson-2-5-summary-configuring-permissions-on-database-objects.md)  
  
## <a name="see-also"></a>Consulte também  
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [REVOGAR &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)  
  
  
