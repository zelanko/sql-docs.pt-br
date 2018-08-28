---
title: APPROX_COUNT_DISTINCT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- APPROX_COUNT_DISTINCT
dev_langs:
- TSQL
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1978f22adf54f13d04df0b103ebe5f37a4eac7b4
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43077566"
---
# <a name="approxcountdistinct-transact-sql"></a>APPROX_COUNT_DISTINCT (Transact-SQL)
[!INCLUDE[appliesto-xx-asdb-asdw-pdw-md](../../includes/appliesto-xx-asdb-asdw-pdw-md.md)]

Essa função retorna o número aproximado de valores não nulos exclusivos em um grupo. 
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

> [!NOTE]
> APPROX_COUNT_DISTINCT é um recurso em versão prévia pública.  
  
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
  
## <a name="remarks"></a>Remarks  
`APPROX_COUNT_DISTINCT( expression )` avalia uma expressão de cada linha em um grupo e retorna o número aproximado de valores não nulos exclusivos em um grupo. Essa função foi projetada para fornecer agregações em grandes conjuntos de dados, nos quais a capacidade de resposta é mais importante do que a precisão absoluta.  

`APPROX_COUNT_DISTINCT` foi projetado para uso em cenários de big data e é otimizado para as seguintes condições:
- Acesso de conjuntos de dados com milhões de linhas ou mais *e*
- Agregação de uma coluna ou colunas com muitos valores distintos

A implementação da função garante uma taxa de erro de até %2 em uma probabilidade de 97%. 

`APPROX_COUNT_DISTINCT` requer menos memória do que uma operação COUNT DISTINCT exaustiva.  Dado o volume de memória menor, `APPROX_COUNT_DISTINCT` apresenta menos probabilidade de despejo de memória em disco comparado com uma operação COUNT DISTINCT precisa. 

> [!NOTE]
> Com cadeias de caracteres confidenciais de agrupamento, a versão prévia pública do APPROX_COUNT_DISTINCT usa uma correspondência binária e gera resultados que teriam sido gerados na presença de agrupamentos BIN, e não de BIN2. 
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-approxcountdistinct"></a>A. Usar APPROX_COUNT_DISTINCT 
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
  
### <a name="b-using-approxcountdistinct-with-group-by"></a>B. Usar APPROX_COUNT_DISTINCT com GROUP BY 
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
