---
description: -- (Comentário) (Transact-SQL)
title: -- (Comentário) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c45b673424fd20defd40d2b62fab19cded05cbca
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128330"
---
# <a name="---comment-transact-sql"></a>-- (Comentário) (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Indica texto fornecido pelo usuário. Os comentários podem ser inseridos em uma linha separada, aninhados no final de uma linha de comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] ou em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. O servidor não avalia o comentário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- text_of_comment  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *text_of_comment*  
 É a cadeia de caracteres que contém o texto do comentário.  
  
## <a name="remarks"></a>Comentários  
Use dois hifens ( **--** ) para comentários de uma linha ou aninhados. Os comentários inseridos com **--** são encerrados por uma nova linha, que é especificada com um caractere de retorno de carro (U + 000A), caractere de alimentação de linha (U + 000D) ou uma combinação dos dois. Não há comprimento máximo para comentários. A tabela a seguir lista os atalhos do teclado que podem ser usados para comentar ou remover comentários do texto.
  
|Ação|Standard|  
|------------|--------------|  
|Transformar o texto selecionado em um comentário|CTRL+K, CTRL+C|  
|Remover comentário do texto selecionado|CTRL+K, CTRL+U|  
  
 Para obter mais informações sobre atalhos de teclado, consulte [Atalhos de teclado do SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md).  
  
 Para comentários de várias linhas, consulte [Barra "/" e asterisco &#40;bloco de comentário&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/slash-star-comment-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa os caracteres de comentário --.  
  
```sql  
-- Choose the AdventureWorks2012 database.  
USE AdventureWorks2012;  
GO  
-- Choose all columns and all rows from the Address table.  
SELECT *  
FROM Person.Address  
ORDER BY PostalCode ASC; -- We do not have to specify ASC because   
-- that is the default.  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Linguagem de controle de fluxo &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  
