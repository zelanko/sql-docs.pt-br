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
manager: craigg
ms.openlocfilehash: 3147ec1eb3fc790ae3672e9f39870935ee085b7e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47598905"
---
# <a name="drop-synonym-transact-sql"></a>DROP SYNONYM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove um sinônimo de um esquema especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP SYNONYM [ IF EXISTS ] [ schema. ] synonym_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Remove condicionalmente o sinônimo somente se ele já existe.  
  
 *schema*  
 Especifica o esquema no qual o sinônimo existe. Se o esquema não for especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará o esquema padrão do usuário atual.  
  
 *synonym_name*  
 É o nome do sinônimo a ser descartado.  
  
## <a name="remarks"></a>Remarks  
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
  
  
