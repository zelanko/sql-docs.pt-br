---
description: money e smallmoney (Transact-SQL)
title: money e smallmoney (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8218bf8b98cd072dd60f8458c75819761153b634
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111277"
---
# <a name="money-and-smallmoney-transact-sql"></a>money e smallmoney (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Tipos de dados que representam valores monetários ou de moeda.
  
## <a name="remarks"></a>Comentários  
  
|Tipo de dados|Intervalo|Armazenamento|  
|---|---|---|
|**money**|-922.337.203.685.477,5808 a 922.337.203.685.477,5807 (-922.337.203.685.477,58<br />a 922.337.203.685.477,58 para o Informatica.  O Informatica dá suporte apenas a dois decimais, não quatro.)|8 bytes|  
|**smallmoney**|-214.748,3648 a 214.748,3647|4 bytes|  
  
Os tipos de dados **money** e **smallmoney** têm a precisão de dez milésimos das unidades monetárias que eles representam. Para o Informatica, os tipos de dados **money** e **smallmoney** têm a precisão de um centésimo das unidades monetárias que eles representam.
  
Use um ponto para separar unidades monetárias parciais, como centavos, de unidades monetárias inteiras. Por exemplo, 2.15 especifica 2 dólares e 15 centavos.
  
Esses tipos de dados podem usar qualquer um dos seguintes símbolos de moeda.
  
![Tabela de símbolos de moeda, valores hexadecimais](../../t-sql/data-types/media/money01.gif "Tabela de símbolos de moeda, valores hexadecimais")
  
Os dados de moeda ou monetários não precisam ser incluídos entre aspas simples ( ' ). É importante lembrar que apesar de você poder especificar valores monetários precedidos por um símbolo de moeda, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não armazena quaisquer informações de moeda associada com o símbolo, só armazena o valor numérico.
  
## <a name="converting-money-data"></a>Convertendo dados money
Ao fazer a conversão em **money** de tipos de dados inteiro, presume-se que as unidades estejam em unidades monetárias. Por exemplo, o valor inteiro 4 é convertido no equivalente de **money** de 4 unidades monetárias.
  
O exemplo a seguir converte os valores **smallmoney** e **money** nos tipos de dados **varchar** e **decimal**, respectivamente.
  
```sql
DECLARE @mymoney_sm SMALLMONEY = 3148.29,  
        @mymoney    MONEY = 3148.29;  
SELECT  CAST(@mymoney_sm AS VARCHAR) AS 'SM_MONEY varchar',  
        CAST(@mymoney AS DECIMAL)    AS 'MONEY DECIMAL';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
SM_MONEY VARCHAR               MONEY DECIMAL  
------------------------------ ----------------------  
3148.29                        3148    
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Confira também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
