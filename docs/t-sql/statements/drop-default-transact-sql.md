---
title: "PADRÃO de DROP (Transact-SQL) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_DEFAULT_TSQL
- DROP DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- DROP DEFAULT statement
- defaults [SQL Server], removing
ms.assetid: d2d3af25-8877-46ba-95d9-1844961d97ee
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cb7de5514d74ed4650d44bed145c32e9bea2c845
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-default-transact-sql"></a>DROP DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um ou mais padrões definidos pelo usuário do banco de dados atual.  
  
> [!IMPORTANT]  
>  DROP DEFAULT será removido na próxima versão do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não use DROP DEFAULT em um novo trabalho de desenvolvimento e planeje modificar os aplicativos que atualmente a utilizam. Em vez disso, use definições padrão que você pode criar usando a palavra-chave DEFAULT de [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP DEFAULT [ IF EXISTS ] { [ schema_name . ] default_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SE EXISTIR*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Condicionalmente descarta o padrão somente se ele já existe.  
  
 *schema_name*  
 É o nome do esquema ao qual o padrão pertence.  
  
 *default_name*  
 É o nome de um padrão existente. Para ver uma lista dos padrões existentes, execute **sp_help**. Os padrões devem estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). Especificar o nome do esquema padrão é opcional.  
  
## <a name="remarks"></a>Comentários  
 Antes de remover um padrão, desassocie-o executando **sp_unbindefault** se o padrão estiver atualmente associado a uma coluna ou um tipo de dados de alias.  
  
 Depois que um padrão é descartado de uma coluna que permite valores nulos, NULL é inserido nessa posição quando as linhas são adicionadas e nenhum valor é explicitamente fornecido. Depois que um padrão é descartado de uma coluna NOT NULL, uma mensagem de erro é retornada quando as linhas são adicionadas e nenhum valor é explicitamente fornecido. Estas linhas são adicionadas posteriormente como parte do comportamento da instrução INSERT típica.  
  
## <a name="permissions"></a>Permissões  
 Para executar DROP DEFAULT, no mínimo, um usuário deve ter a permissão ALTER no esquema ao qual o padrão pertence.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-a-default"></a>A. Descartando um padrão  
 Se um padrão não estiver associado a uma coluna ou a um tipo de dados de alias, ele só poderá ser descartado usando DROP DEFAULT. O exemplo a seguir remove o padrão criado pelo usuário chamado `datedflt`.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
         WHERE name = 'datedflt'   
            AND type = 'D')  
   DROP DEFAULT datedflt;  
GO  
```  
  
 Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] você pode usar a sintaxe a seguir.  
  
```  
DROP DEFAULT IF EXISTS datedflt;  
GO  
```  
  
### <a name="b-dropping-a-default-that-has-been-bound-to-a-column"></a>B. Descartando um padrão associado a uma coluna  
 O exemplo a seguir desassocia o padrão associado à coluna `EmergencyContactPhone` da tabela `Contact` e descarta o padrão chamado `phonedflt`.  
  
```  
USE AdventureWorks2012;  
GO  
   BEGIN   
      EXEC sp_unbindefault 'Person.Contact.Phone'  
      DROP DEFAULT phonedflt  
   END;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_unbindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  

