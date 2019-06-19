---
title: Classificador DROP WORKLOAD (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- DROP_WORKLOAD_CLASSIFIER_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 67909db180af056add12324622cfd6094d8729fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65105829"
---
# <a name="drop-workload-classifier-transact-sql"></a>DROP WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Descarta um classificador de gerenciamento de carga de trabalho definido pelo usuário existente.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  

```
DROP WORKLOAD CLASSIFIER classifier_name;
```

## <a name="arguments"></a>Argumentos

*classifier_name*  
Especifique o nome pelo qual o classificador de carga de trabalho é identificado.  classifier_name é um sysname.  Ele pode ter até 128 caracteres e deve ser exclusivo dentro da instância.
  
## <a name="remarks"></a>Remarks

A instrução DROP WORKLOAD CLASSIFIER não é permitida em classificadores de carga de trabalho do sistema.

Se as solicitações estão em execução ou na fila de solicitação em estado suspenso, elas manterão sua classificação e o classificador poderá ser removido imediatamente.  Descartar e recriar o classificador com importância diferente não afetará uma solicitação já classificada.

## <a name="permissions"></a>Permissões

Requer a permissão CONTROL DATABASE.  
  
## <a name="examples"></a>Exemplos

O seguinte exemplo descarta o classificador de carga de trabalho denominado `wgcELTROLE`.  

```sql
DROP WORKLOAD CLASSIFIER wgcELTRole;
```

> [!NOTE]
> Uma solicitação enviada sem um classificador correspondente é classificada para o grupo de carga de trabalho padrão.  O grupo de carga de trabalho padrão é a classe de recurso smallrc.
  
## <a name="see-also"></a>Consulte Também

[CREATE WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-classifier-transact-sql.md)</br>
[Classificação de carga de trabalho do SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
