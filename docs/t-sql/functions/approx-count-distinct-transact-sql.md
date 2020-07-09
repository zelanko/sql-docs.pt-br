---
title: APPROX_COUNT_DISTINCT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APPROX_COUNT_DISTINCT
dev_langs:
- TSQL
author: joesackmsft
ms.author: josack
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e8a506597e3f702f36996da687fe0cf4058fc2ca
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007946"
---
# <a name="approx_count_distinct-transact-sql"></a>APPROX_COUNT_DISTINCT (Transact-SQL)

[!INCLUDE [sqlserver2019-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2019-asdb-asdbmi-asa.md)]

Essa função retorna o número aproximado de valores não nulos exclusivos em um grupo. 
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse and Parallel Data Warehouse  

APPROX_COUNT_DISTINCT ( expression )   
```  
  
## <a name="arguments"></a>Argumentos  
*expressão*  
Uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo, exceto **image**, **sql_variant**, **ntext** ou **text**. 

## <a name="return-types"></a>Tipos de retorno
 **bigint**  
  
## <a name="remarks"></a>Comentários  
`APPROX_COUNT_DISTINCT( expression )` avalia uma expressão de cada linha em um grupo e retorna o número aproximado de valores não nulos exclusivos em um grupo. Essa função foi projetada para fornecer agregações em grandes conjuntos de dados, nos quais a capacidade de resposta é mais importante do que a precisão absoluta.  

`APPROX_COUNT_DISTINCT` foi projetado para uso em cenários de big data e é otimizado para as seguintes condições:
- Acesso de conjuntos de dados com milhões de linhas ou mais *e*
- Agregação de uma coluna ou colunas com muitos valores distintos

A implementação da função garante uma taxa de erro de até %2 em uma probabilidade de 97%. 

`APPROX_COUNT_DISTINCT` requer menos memória do que uma operação COUNT DISTINCT exaustiva.  Dado o volume de memória menor, `APPROX_COUNT_DISTINCT` apresenta menos probabilidade de despejo de memória em disco comparado com uma operação COUNT DISTINCT precisa. Saiba mais sobre o algoritmo usado para conseguir isso em [HyperLogLog](https://en.wikipedia.org/wiki/HyperLogLog).

> [!NOTE]
> Com as cadeias de caracteres confidenciais de ordenação, APPROX_COUNT_DISTINCT usa uma correspondência binária e fornece resultados que teriam sido gerados na presença de ordenações BIN, não BIN2. 
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-approx_count_distinct"></a>a. Usar APPROX_COUNT_DISTINCT 
Este exemplo retorna o número aproximado de chaves de ordem diferentes da tabela ordens.
  
```sql
SELECT APPROX_COUNT_DISTINCT(O_OrderKey) AS Approx_Distinct_OrderKey
FROM dbo.Orders;
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Approx_Distinct_OrderKey
------------------------
15164704
```
  
### <a name="b-using-approx_count_distinct-with-group-by"></a>B. Usar APPROX_COUNT_DISTINCT com GROUP BY 
Este exemplo retorna o número aproximado de chaves de ordem diferentes por status da ordem da tabela ordens. 
  
```sql
SELECT O_OrderStatus, APPROX_COUNT_DISTINCT(O_OrderKey) AS Approx_Distinct_OrderKey
FROM dbo.Orders
GROUP BY O_OrderStatus
ORDER BY O_OrderStatus; 
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
O_OrderStatus                                                    Approx_Distinct_OrderKey
---------------------------------------------------------------- ------------------------
F                                                                7397838
O                                                                7387803
P                                                                388036
```
    
## <a name="see-also"></a>Confira também
[Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md) 
