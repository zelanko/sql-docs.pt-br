---
description: DATEFROMPARTS (Transact-SQL)
title: DATEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 405155dbc721afe162baca38f6db04e73625c639
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111197"
---
# <a name="datefromparts-transact-sql"></a>DATEFROMPARTS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Essa função retorna um valor **date** que é mapeado para os valores de dia, mês e ano especificados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DATEFROMPARTS ( year, month, day )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*year*  
Uma expressão de inteiro que especifica um ano.
  
*month*  
Uma expressão de inteiro que especifica um mês, de 1 a 12.
  
*day*  
Uma expressão de inteiro que especifica um dia.
  
## <a name="return-types"></a>Tipos de retorno
**date**
  
## <a name="remarks"></a>Comentários  
`DATEFROMPARTS` retorna um valor **date** com a parte de data definida como o ano, mês e dia especificados e a parte de hora definida como o padrão. Para argumentos inválidos, `DATEFROMPARTS` gerará um erro. `DATEFROMPARTS` retornará nulo se pelo menos um argumento necessário tiver um valor nulo.
  
Essa função pode operar comunicação remota para servidores [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posteriores. Ela não pode operar comunicação remota para servidores com uma versão inferior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].
  
## <a name="examples"></a>Exemplos  
Este exemplo mostra a função `DATEFROMPARTS` em ação.
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Veja também
[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)
  
  

