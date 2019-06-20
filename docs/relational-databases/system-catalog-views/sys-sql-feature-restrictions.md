---
title: sys.sql_feature_restrictions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/07/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_sql_feature_restrictions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_feature_restrictions catalog view
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b583afef9f52da7801384d4a7a9c76deaf8d4ee4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822682"
---
# <a name="syssqlfeaturerestrictions-transact-sql"></a>sys.sql_feature_restrictions (Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Retorna uma linha para cada restrição no banco de dados.
  
| Nome da coluna | Tipo de dados | Descrição |
|-------------|-----------|-------------|
| class       | nvarchar(128) | Classe de objeto ao qual a restrição se aplica |
| objeto      | nvarchar(256) | Nome do objeto ao qual a restrição se aplica |
| Recurso     | nvarchar(128) | Recurso que é restrito |
  
## <a name="remarks"></a>Comentários

Atualmente, os recursos a seguir podem ser restritos:

| Recurso          | Descrição |
|------------------|-------------|
| N'ErrorMessages' | Quando restrito, qualquer dado de usuário dentro da mensagem de erro será mascarado. |
| N'Waitfor'       | Quando a restrito, o comando retornará imediatamente sem nenhum atraso. |
  
## <a name="permissions"></a>Permissões

A entidade em execução deve ter o `CONTROL` permissão no banco de dados.
  
## <a name="see-also"></a>Consulte também

 [Restrições de recursos](../../relational-databases/security/feature-restrictions.md)
