---
title: DATETIMEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATETIMEFROMPARTS_TSQL
- DATETIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEFROMPARTS function
ms.assetid: 6008148b-bf75-4c98-9392-68a89fa0711c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 505b1ac04eae49c58a4166fcceba8ec9bf53a66a
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945729"
---
# <a name="datetimefromparts-transact-sql"></a>DATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Essa função retorna um valor **datetime** para os argumentos de data e hora especificados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATETIMEFROMPARTS ( year, month, day, hour, minute, seconds, milliseconds )  
```  
  
## <a name="arguments"></a>Argumentos  
*year*  
Uma expressão de inteiro que especifica um ano.
  
*month*  
Uma expressão de inteiro que especifica um mês.
  
*day*  
Uma expressão de inteiro que especifica um dia.
  
*hour*  
Uma expressão de inteiro que especifica horas.
  
*minute*  
Uma expressão de inteiro que especifica minutos.
  
*segundos*  
Uma expressão de inteiro que especifica segundos.
  
*milliseconds*  
Uma expressão de inteiro que especifica milissegundos.
  
## <a name="return-types"></a>Tipos de retorno
**datetime**
  
## <a name="remarks"></a>Remarks  
`DATETIMEFROMPARTS` retorna um valor **datetime** completamente inicializado. `DATETIMEFROMPARTS` gerará um erro se pelo menos um argumento necessário tiver um valor inválido. `DATETIMEFROMPARTS` retornará nulo se pelo menos um argumento necessário tiver um valor nulo.
  
Essa função dá suporte à comunicação remota para servidores [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e acima. Ela não dará suporte a comunicação remota para servidores que têm uma versão anterior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Exemplos  
  
```sql
SELECT DATETIMEFROMPARTS ( 2010, 12, 31, 23, 59, 59, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Confira também
[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)
  
  

