---
title: "DDL com suporte para módulos T-SQL compilados nativamente | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6468568f12555425cb038ce6293f8777e0a3689
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="supported-ddl-for-natively-compiled-t-sql-modules"></a>DDL com suporte para módulos T-SQL compilados nativamente
  Este tópico lista as construções DDL com suporte para módulos T-SQL compilados nativamente, como procedimentos armazenados, UDFs escalares, TVFs embutidos e gatilhos.  
  
 Para obter informações sobre os recursos e a área de superfície do T-SQL que pode ser usada como parte dos módulos compilados de modo nativo do T-SQL, veja [Recursos com suporte para módulos T-SQL compilados de modo nativo](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
 Para obter informações sobre construções sem suporte, veja [Construções do Transact-SQL sem suporte pelo OLTP in-memory](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
 Há suporte para o seguinte:  
  
-   [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
-   [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
-   [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
-   Instruções [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md) e INSERT SELECT  
  
-   SCHEMABINDING e BEGIN ATOMIC (necessário para procedimentos armazenados compilados nativamente)  
  
     Para saber mais, consulte [Creating Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md).  
  
-   NATIVE_COMPILATION  
  
     Para saber mais, consulte [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md).  
  
-   Parâmetros e variáveis podem ser declarados como NOT NULL (disponível somente para módulos compilados nativamente: procedimentos armazenados compilados nativamente e funções compiladas nativamente, escalares e definidas pelo usuário).  
  
-   Parâmetros com valor de tabela.  
  
     Para obter mais informações, veja [Usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
-   EXECUTE AS OWNER, SELF, CALLER e usuário.  
  
-   Permissões GRANT e DENY em tabelas e procedimentos.  
  
     Para obter mais informações, veja [Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md) e [Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
