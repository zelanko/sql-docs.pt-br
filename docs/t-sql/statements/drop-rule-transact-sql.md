---
title: REGRA de DROP (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_RULE_TSQL
- DROP RULE
dev_langs:
- TSQL
helpviewer_keywords:
- rules [SQL Server], removing
- deleting roles
- DROP RULE statement
- removing roles
- dropping roles
ms.assetid: 8370b730-7fd5-43fe-a7f6-8300b3caa16d
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ba898b1c9f94f4e38102da929709b4a05f889b7e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-rule-transact-sql"></a>DROP RULE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma ou mais regras definidas pelo usuário do banco de dados atual.  
  
> [!IMPORTANT]  
>  DROP RULE será removido na próxima versão do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não use DROP RULE em um novo trabalho de desenvolvimento e planeje modificar os aplicativos que atualmente a utilizam. Em vez disso, use restrições de verificação que você pode criar usando a palavra-chave CHECK de [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) ou [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md). Para obter mais informações, consulte [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP RULE [ IF EXISTS ] { [ schema_name . ] rule_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SE EXISTIR*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Descarta condicionalmente a regra somente se ele já existe.  
  
 *schema_name*  
 É o nome do esquema ao qual a regra pertence.  
  
 *regra*  
 É a regra a ser removida. Nomes de regras devem estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). A especificação do esquema da regra é opcional.  
  
## <a name="remarks"></a>Comentários  
 Para descartar uma regra, primeiro, desvincule-a se ela estiver atualmente vinculada a uma coluna ou a um tipo de dados de alias. Para desvincular a regra, use **sp_unbindrule**. Se a regra estiver vinculada quando você tentar descartá-la, uma mensagem de erro será exibida e a instrução DROP RUL será cancelada.  
  
 Depois que a regra é descartada, os novos dados inseridos nas colunas anteriormente controladas pela regra não são afetados por suas restrições. Os dados existentes não sofrem nenhuma alteração.  
  
 A instrução DROP RULE não se aplica a restrições CHECK. Para obter mais informações sobre como descartar restrições de verificação, consulte [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Para executar DROP RULE, no mínimo, um usuário deve ter a permissão ALTER no esquema ao qual a regra pertence.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir desvincula e descarta a regra chamada `VendorID_rule`. 
  
```  
sp_unbindrule 'Production.ProductVendor.VendorID'  
DROP RULE VendorID_rule  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_unbindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  


