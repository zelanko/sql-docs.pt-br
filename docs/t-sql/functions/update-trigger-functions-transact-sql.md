---
title: Update () (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE()_TSQL
- UPDATE()
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], UPDATE function
- testing column updates
- UPDATE function
- UPDATE() function
- detecting changes
- columns [SQL Server], change detection
- UPDATE statement [SQL Server], UPDATE function
- verifying column updates
- checking column updates
ms.assetid: 8e3be25b-2e3b-4d1f-a610-dcbbd8d72084
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 644848af581b0db5a26b9958db4660b4cab66163
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="update---trigger-functions-transact-sql"></a>UPDATE - funções de gatilho (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um valor booliano que indica se foi feita uma tentativa de INSERT ou UPDATE em uma coluna especificada de uma tabela ou exibição. UPDATE() é usado em qualquer lugar no corpo de um gatilho INSERT ou UPDATE do [!INCLUDE[tsql](../../includes/tsql-md.md)] para testar se o gatilho deve executar determinadas ações.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UPDATE ( column )   
```  
  
## <a name="arguments"></a>Argumentos  
 *coluna*  
 É o nome da coluna a ser testada para uma ação INSERT ou UPDATE. Como o nome da tabela está especificado na cláusula ON do gatilho, não inclua o nome da tabela antes do nome da coluna. A coluna pode ser de qualquer [tipo de dados](../../t-sql/data-types/data-types-transact-sql.md) suporte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Entretanto, não é possível usar colunas computadas nesse contexto.  
  
## <a name="return-types"></a>Tipos de retorno  
 Booliano  
  
## <a name="remarks"></a>Comentários  
 UPDATE() retorna TRUE, independentemente de uma tentativa de INSERT ou UPDATE ter êxito.  
  
 Para testar uma ação INSERT ou UPDATE para mais de uma coluna, especifique uma atualização individual (*coluna*) após o primeiro deles. Também é possível testar várias colunas para ações INSERT ou UPDATE usando COLUMNS_UPDATED. Isto retorna um padrão de bits que indica quais colunas foram inseridas ou atualizadas.  
  
 IF UPDATE retorna o valor TRUE em ações INSERT porque as colunas tiverem valores explícitos ou implícitos (NULL) inseridos.  
  
> [!NOTE]  
>  IF UPDATE (*coluna*n) cláusula funciona como um se se... Caso contrário, ou cláusula WHILE e pode usar o BEGIN... Bloco final. Para obter mais informações, consulte [linguagem de controle de fluxo &#40; Transact-SQL &#41; ](~/t-sql/language-elements/control-of-flow.md).  
  
 ATUALIZAÇÃO (*coluna*) pode ser usado em qualquer lugar dentro do corpo de um [!INCLUDE[tsql](../../includes/tsql-md.md)] gatilho.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um gatilho que imprime uma mensagem para o cliente quando qualquer pessoa tentar atualizar as colunas `StateProvinceID` ou `PostalCode` da tabela `Address`.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
      WHERE name = 'reminder' AND type = 'TR')  
   DROP TRIGGER Person.reminder;  
GO  
CREATE TRIGGER reminder  
ON Person.Address  
AFTER UPDATE   
AS   
IF ( UPDATE (StateProvinceID) OR UPDATE (PostalCode) )  
BEGIN  
RAISERROR (50009, 16, 10)  
END;  
GO  
-- Test the trigger.  
UPDATE Person.Address  
SET PostalCode = 99999  
WHERE PostalCode = '12345';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [COLUMNS_UPDATED &#40; Transact-SQL &#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  

