---
title: DROP SYNONYM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SYNONYM
- DROP_SYNONYM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting synonyms
- synonyms [SQL Server], removing
- removing synonyms
- DROP SYNONYM statement
- dropping synonyms
ms.assetid: 23578932-e4de-4c39-a5a0-ce45139c4269
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 59c26a7e490edb120d8819d8e2b16158b5b41e76
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68072136"
---
# <a name="drop-synonym-transact-sql"></a>DROP SYNONYM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove um sinônimo de um esquema especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP SYNONYM [ IF EXISTS ] [ schema. ] synonym_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Remove condicionalmente o sinônimo somente se ele já existe.  
  
 *schema*  
 Especifica o esquema no qual o sinônimo existe. Se o esquema não for especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará o esquema padrão do usuário atual.  
  
 *synonym_name*  
 É o nome do sinônimo a ser descartado.  
  
## <a name="remarks"></a>Comentários  
 Referências a sinônimos não são associadas a esquemas. Portanto, você pode descartar um sinônimo a qualquer momento. As referências a sinônimos descartados só serão localizadas no momento da execução.  
  
 É possível criar, descartar e referenciar sinônimos em SQL dinâmico.  
  
## <a name="permissions"></a>Permissões  
 Para descartar um sinônimo, um usuário deve satisfazer pelo menos uma das condições a seguir. O usuário deve ser:  
  
-   O proprietário atual de um sinônimo.  
  
-   Um usuário autorizado que mantenha CONTROL em um sinônimo.  
  
-   Um usuário autorizado que mantenha a permissão ALTER SCHEMA no esquema contentor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir primeiramente cria um sinônimo `MyProduct` e, em seguida, descarta-o.  
  
```  
USE tempdb;  
GO  
-- Create a synonym for the Product table in AdventureWorks2012.  
CREATE SYNONYM MyProduct  
FOR AdventureWorks2012.Production.Product;  
GO  
-- Drop synonym MyProduct.  
USE tempdb;  
GO  
DROP SYNONYM MyProduct;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
