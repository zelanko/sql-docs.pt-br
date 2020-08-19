---
description: DROP SEQUENCE (Transact-SQL)
title: DROP SEQUENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SEQUENCE
- DROP_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SEQUENCE statement
- sequence number object, dropping
ms.assetid: c25772d3-61af-4aa7-b58b-a6f67a793e3d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7c880111b104abc2de1b1d4d6c8f3cc3e672ef91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444583"
---
# <a name="drop-sequence-transact-sql"></a>DROP SEQUENCE (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Remove um objeto de sequência do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DROP SEQUENCE [ IF EXISTS ] { database_name.schema_name.sequence_name | schema_name.sequence_name | sequence_name } [ ,...n ]  
 [ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *IF EXISTS*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Remove condicionalmente a sequência somente se ela já existe.  
  
 *database_name*  
 É o nome do banco de dados no qual o objeto de sequência foi criado.  
  
 *schema_name*  
 É o nome do esquema ao qual o objeto de sequência pertence.  
  
 *sequence_name*  
 É o nome da sequência a ser removida. O tipo é **sysname**.  
  
## <a name="remarks"></a>Comentários  
 Depois de gerar um número, um objeto de sequência não tem nenhuma relação contínua com o número que gerou; portanto, o objeto de sequência pode ser removido, embora o número gerado ainda esteja em uso.  
  
 Um objeto de sequência pode ser removido enquanto é referenciado por um procedimento armazenado, ou pode ser disparado, pois não é associado ao esquema. Um objeto de sequência não poderá ser removido se for referenciado como um valor padrão em uma tabela. A mensagem de erro listará o objeto que referencia a sequência.  
  
 Para listar todos os objetos de sequência no banco de dados, execute a instrução a seguir.  
  
```  
SELECT sch.name + '.' + seq.name AS [Sequence schema and name]   
    FROM sys.sequences AS seq  
    JOIN sys.schemas AS sch  
        ON seq.schema_id = sch.schema_id ;  
GO  
```  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ou CONTROL no esquema.  
  
### <a name="audit"></a>Audit  
 Para auditar **DROP SEQUENCE**, monitore **SCHEMA_OBJECT_CHANGE_GROUP**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove do banco de dados atual um objeto de sequência denominado `CountBy1`.  
  
```  
DROP SEQUENCE CountBy1 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
