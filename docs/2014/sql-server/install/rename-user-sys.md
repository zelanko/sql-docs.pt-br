---
title: Renomear usuário sys | Microsoft Docs
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
- sys user names [SQL Server]
ms.assetid: d622d646-83e4-4b6f-9a21-77b301af04b5
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 959eb9877fa4b73ff9bd307019976a05514b8f8f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008832"
---
# <a name="rename-user-sys"></a>Renomear usuário sys
  O Supervisor de Atualização detectou o nome de usuário **sys** em um banco de dados. Esse nome é reservado. Renomeie o usuário antes de atualizar. Se isso não for feito, o banco de dados ficará em estado suspeito após o processo de atualização e não estará disponível até que banco de dados fique online novamente.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 O usuário **sys** é reservado.  
  
## <a name="corrective-action"></a>Ação corretiva  
  
### <a name="before-upgrade-procedure"></a>Antes do procedimento de atualização  
 Antes da atualização, faça o seguinte em cada banco de dados que contém o usuário **sys**:  
  
1.  Crie um usuário novo.  
  
2.  Use as instruções a seguir para exibir todas as permissões que são concedidas pelo usuário **sys** e ao usuário **sys**.  
  
    ```  
    -- Return permissions granted by user sys.  
    SELECT * FROM sysprotects WHERE grantor = USER_ID('sys')  
    -- Return permissions granted to user sys.  
    SELECT * FROM sysprotects WHERE uid = USER_ID('sys')  
    ```  
  
3.  Para transferir a propriedade de todos os objetos do **sys** para o novo usuário, use **sp_changeobjectowner**.  
  
4.  Descarte o usuário **sys**.  
  
5.  Para restaurar as permissões originais capturadas na etapa 2, use a cláusula AS *new_user* da instrução GRANT.  
  
6.  Modifique os scripts para referenciarem o novo usuário. Por exemplo, os scripts que contêm instruções como `SELECT * FROM sys.my`_`table` devem ser alterados para `SELECT * FROM new_user.my_table`.  
  
### <a name="after-upgrade-procedure"></a>Depois do procedimento de atualização  
 Se o usuário **sys** não foi renomeado antes da atualização, faça o seguinte:  
  
1.  Execute a instrução `ALTER DATABASE db_name SET ONLINE`. O banco de dados estará no modo SINGLE_USER.  
  
2.  Siga todas as etapas da seção Antes do procedimento de atualização.  
  
3.  Execute a instrução `ALTER DATABASE db_name SET MULTI_USER`.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
