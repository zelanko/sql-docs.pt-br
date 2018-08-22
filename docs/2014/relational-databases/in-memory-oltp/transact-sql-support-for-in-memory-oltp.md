---
title: Suporte ao Transact-SQL para OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83a6cbab37e328110287b286d70a1c31cc26a36a
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392471"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>Suporte ao Transact-SQL para OLTP na memória
  Você pode acessar tabelas com otimização de memória usando qualquer consulta de Transact-SQL ou operação DML (SELEÇÃO, INSERÇÃO, ATUALIZAÇÃO ou EXCLUSÃO), lotes ad hoc e os módulos SQL, como procedimentos armazenados, funções com valor de tabela, funções escalares, gatilhos e exibições. Para obter mais informações, consulte [acessando tabelas usando Transact-SQL interpretado](accessing-memory-optimized-tables-using-interpreted-transact-sql.md).  
  
 Os procedimentos armazenados que só fazem referência a tabelas com otimização de memória podem ser compilados nativamente em código de computador e fornecem tipicamente melhorias de desempenho sobre procedimentos armazenados interpretados (baseados em disco). Para acesso otimizado a tabelas com otimização de memória, use procedimentos armazenados compilados. Para saber mais, veja [Procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md).  
  
 Ao criar e modificar objetos de banco de dados (instruções DDL), as instruções a seguir são modificadas:  
  
-   [Opções de grupo de arquivos e alterar o arquivo de banco de dados &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options) (consulte `MEMORY_OPTIMIZED_DATA`)  
  
-   [Criar banco de dados &#40;SQL Server Transact-SQL&#41; ](/sql/t-sql/statements/create-database-sql-server-transact-sql) (consulte `MEMORY_OPTIMIZED_DATA`)  
  
-   [CREATE PROCEDURE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-procedure-transact-sql) (consulte `NATIVE_COMPILATION`, `SCHEMABINDING`, `EXECUTE AS`, e `BEGIN ATOMIC`)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-table-transact-sql) (consulte `MEMORY_OPTIMIZED`, `DURABILITY`, `BUCKET_COUNT`, `INDEX`, e `HASH`)  
  
-   [Criar tipo de &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-type-transact-sql) (consulte `MEMORY_OPTIMIZED`, `BUCKET_COUNT`, `INDEX`, e `HASH`)  
  
-   [DECLARAR @local_variable &#40;Transact-SQL&#41; ](/sql/t-sql/language-elements/declare-local-variable-transact-sql) (consulte `NULL`  |  `NOT NULL`)  
  
 As tabelas com otimização de memória suportam restrições `PRIMARY KEY` e `NOT NULL`. Para obter informações sobre como implementar restrições sem suporte, consulte [migrando Check e Foreign Key Constraints](../../database-engine/migrating-check-and-foreign-key-constraints.md).  
  
 Para obter informações sobre os recursos sem suporte, veja [Construções do Transact-SQL sem suporte pelo OLTP in-memory](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Tipos de dados com suporte](supported-data-types-for-in-memory-oltp.md)  
  
-   [Acessando tabelas com otimização de memória usando Transact-SQL interpretado](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)  
  
-   [Exibições do sistema, procedimentos armazenados, tipos de espera e DMVs para OLTP in-memory](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](in-memory-oltp-in-memory-optimization.md)   
 [Problemas de migração para procedimentos armazenados compilados nativamente](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Recursos com suporte do SQL Server](unsupported-sql-server-features-for-in-memory-oltp.md)   
 [Procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md)  
  
  
