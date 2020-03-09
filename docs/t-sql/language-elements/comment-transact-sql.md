---
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
ms.openlocfilehash: d7e9aaab99194646874c0823abb61100cdc524aa
ms.sourcegitcommit: 639842f0b70e8c2c9ad5e86f9bfc3a4aad61a1df
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/04/2020
ms.locfileid: "78261695"
---
# <a name="---comment-transact-sql"></a>-- (Comentário) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Indica texto fornecido pelo usuário. Os comentários podem ser inseridos em uma linha separada, aninhados no final de uma linha de comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] ou em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. O servidor não avalia o comentário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
-- text_of_comment  
```  
  
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
  
```  
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
  
  
