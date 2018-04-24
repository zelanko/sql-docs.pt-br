---
title: DATEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b5348706b7326a56b5d1367104301db557b8cd8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="datefromparts-transact-sql"></a>DATEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Retorna um valor de **date** para o ano, o mês e o dia especificados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATEFROMPARTS ( year, month, day )  
```  
  
## <a name="arguments"></a>Argumentos  
*year*  
Expressão de inteiro que especifica um ano.
  
*month*  
Expressão de inteiro que especifica um mês, de 1 a 12.
  
*day*  
Expressão de inteiro que especifica um dia.
  
## <a name="return-types"></a>Tipos de retorno
**date**
  
## <a name="remarks"></a>Remarks  
**DATEFROMPARTS** retorna um valor de **date** com a parte de data definida como o ano, o mês e o dia especificados e a parte de hora definida com o padrão. Se os argumentos não forem válidos, um erro será gerado. Se os argumentos necessários forem nulos, nulo será retornado.
  
Essa função é capaz de ser remota para servidores do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e acima. Ela não será remota para servidores de versão anterior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir demonstra a função **DATEFROMPARTS**.
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Confira também
[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)
  
  

