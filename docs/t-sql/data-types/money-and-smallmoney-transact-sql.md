---
title: money e smallmoney (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cb48673efe61e519deb2a82d3ae67e1eee8481cb
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415465"
---
# <a name="money-and-smallmoney-transact-sql"></a>money e smallmoney (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de dados que representam valores monetários ou de moeda.
  
## <a name="remarks"></a>Remarks  
  
|Tipo de dados|Intervalo|Armazenamento|  
|---|---|---|
|**money**|-922.337.203.685.477,5808 a 922.337.203.685.477,5807 (-922.337.203.685.477,58<br />a 922.337.203.685.477,58 para o Informatica.  O Informatica dá suporte apenas a dois decimais, não quatro.)|8 bytes|  
|**smallmoney**|-214.748,3648 a 214.748,3647|4 bytes|  
  
Os tipos de dados **money** e **smallmoney** têm a precisão de dez milésimos das unidades monetárias que eles representam. Para o Informatica, os tipos de dados **money** e **smallmoney** têm a precisão de um centésimo das unidades monetárias que eles representam.
  
Use um ponto para separar unidades monetárias parciais, como centavos, de unidades monetárias inteiras. Por exemplo, 2.15 especifica 2 dólares e 15 centavos.
  
Esses tipos de dados podem usar qualquer um dos seguintes símbolos de moeda.
  
![Tabela de símbolos de moeda, valores hexadecimais](../../t-sql/data-types/media/money01.gif "Table of currency symbols, hexadecimal values")
  
Os dados de moeda ou monetários não precisam ser incluídos entre aspas simples ( ' ). É importante lembrar que apesar de você poder especificar valores monetários precedidos por um símbolo de moeda, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não armazena quaisquer informações de moeda associada com o símbolo, só armazena o valor numérico.
  
## <a name="converting-money-data"></a>Convertendo dados money
Ao fazer a conversão em **money** de tipos de dados inteiro, presume-se que as unidades estejam em unidades monetárias. Por exemplo, o valor inteiro 4 é convertido no equivalente de **money** de 4 unidades monetárias.
  
O exemplo a seguir converte os valores **smallmoney** e **money** nos tipos de dados **varchar** e **decimal**, respectivamente.
  
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
  
## <a name="see-also"></a>Confira também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
