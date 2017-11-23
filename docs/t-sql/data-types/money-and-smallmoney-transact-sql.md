---
title: Money e smallmoney (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- money_TSQL
- money
- smallmoney
- smallmoney_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- money data type, about money data type
- money data type
- smallmoney data type
- values [SQL Server], monetary
- currency [SQL Server]
ms.assetid: 57861137-89ea-4b89-b361-390597d7bccc
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bd07ecd1cdacc686e0f831320fd5e939c0c174da
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="money-and-smallmoney-transact-sql"></a>money e smallmoney (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de dados que representam valores monetários ou de moeda.
  
## <a name="remarks"></a>Comentários  
  
|Tipo de dados|Intervalo|Armazenamento|  
|---|---|---|
|**money**|-922,337,203,685,477.5808 para 922.337.203.685.477,5807 (-922,337,203,685,477.58<br />para 922,337,203,685,477.58 para Informatica.  Informatica só dá suporte a dois decimais não quatro.)|8 bytes|  
|**smallmoney**|-214.748,3648 a 214.748,3647|4 bytes|  
  
O **money** e **smallmoney** tipos de dados são precisos em dez milésimos de unidades monetárias que eles representam. Para Informatica, o **money** e **smallmoney** tipos de dados são precisos em um centésimos de uma das unidades monetárias que eles representam.
  
Use um ponto para separar unidades monetárias parciais, como centavos, de unidades monetárias inteiras. Por exemplo, 2.15 especifica 2 dólares e 15 centavos.
  
Esses tipos de dados podem usar qualquer um dos seguintes símbolos de moeda.
  
![Tabela de símbolos de moeda, valores hexadecimais](../../t-sql/data-types/media/money01.gif "tabela de símbolos de moeda, valores hexadecimais")
  
Os dados de moeda ou monetários não precisam ser incluídos entre aspas simples ( ' ). É importante lembrar que apesar de você poder especificar valores monetários precedidos por um símbolo de moeda, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não armazena quaisquer informações de moeda associada com o símbolo, só armazena o valor numérico.
  
## <a name="converting-money-data"></a>Convertendo dados money
Quando você converte em **money** de tipos de dados inteiro, as unidades são consideradas em unidades monetárias. Por exemplo, o valor de inteiro de 4 é convertido para o **money** equivalente de 4 unidades monetárias.
  
O exemplo a seguir converte **smallmoney** e **money** valores **varchar** e **decimal** tipos de dados, respectivamente.
  
```sql
DECLARE @mymoney_sm smallmoney = 3148.29,  
        @mymoney    money = 3148.29;  
SELECT  CAST(@mymoney_sm AS varchar) AS 'SM_MONEY varchar',  
        CAST(@mymoney AS decimal)    AS 'MONEY DECIMAL';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
SM_MONEY VARCHAR               MONEY DECIMAL  
------------------------------ ----------------------  
3148.29                        3148    
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também
[Instrução ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) 
 [CAST e CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md) 
 [Criar tabela &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md) 
 [Tipos de dados &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md) 
 [DECLARE @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 
 [Definir @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/set-local-variable-transact-sql.md) 
 [Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

