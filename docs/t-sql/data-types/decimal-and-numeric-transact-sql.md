---
title: decimal e numeric (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- decimal
- decimal_TSQL
- numeric
- numeric_TSQL
dev_langs: TSQL
helpviewer_keywords:
- decimal data type
- decimal data type, about decimal data type
- numeric data type
- numeric data type, about numeric data type
ms.assetid: 9d862a90-e6b7-4692-8605-92358dccccdf
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 614025c21f0f021a4b1ad3a193afec8f5115b845
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="decimal-and-numeric-transact-sql"></a>decimal e numeric (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de dados numéricos que têm precisão e escala fixos. Decimais e numéricos são sinônimos e podem ser usadas intercambiavelmente.
  
## <a name="arguments"></a>Argumentos  
**decimal**[ **(***p*[ **,***s*] **)**] e **numérico** [ **(***p*[ **,***s*] **)**]  
Números de precisão e escala fixos. Quando a precisão máxima for usada, os valores válidos serão de - 10^38 +1 a 10^38 - 1. Os sinônimos ISO para **decimal** são **dez** e **dec (***p*, *s***)**. **numérico** é funcionalmente equivalente à **decimal**.
  
p (precisão)  
O número máximo total de dígitos decimais que poderão ser armazenados, à esquerda e à direita do ponto decimal. A precisão deve ser um valor de 1 até a precisão máxima de 38. A precisão padrão é 18.
  
> [!NOTE]  
>  Informatica só oferece suporte a 16 dígitos significativos, independentemente da precisão e escala especificada.  
  
*s* (escala)  
O número máximo de dígitos decimais que poderão ser armazenados à direita do ponto decimal. Esse número é subtraído de *p* para determinar o número máximo de dígitos à esquerda da vírgula decimal. O número máximo de dígitos decimais que podem ser armazenados à direita do ponto decimal. Escala deve ser um valor de 0 a *p*. A escala somente poderá ser especificada se precisão também o for. A escala padrão é 0; Portanto, 0 < = *s* \< =  *p*. Os tamanhos máximos de armazenamento variam, com base na precisão.
  
|Precisão|Bytes de armazenamento|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica (conectado por meio do conector do SQL Server PDW Informatica) só oferece suporte a 16 dígitos significativos, independentemente da precisão e escala especificada.  
  
## <a name="converting-decimal-and-numeric-data"></a>Convertendo dados decimais e numéricos
Para o **decimal** e **numérico** tipos de dados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera cada combinação específica de precisão e escala como um tipo de dados diferente. Por exemplo, **decimal(5,5)** e **decimal(5,0)** são considerados tipos de dados diferentes.
  
Em [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções, uma constante com um ponto decimal é convertida automaticamente em um **numérico** dados de valor, usando a precisão mínima e dimensionar necessário. Por exemplo, a constante 12.345 é convertida em uma **numérico** valor com uma precisão de 5 e uma escala de 3.
  
Convertendo de **decimal** ou **numérico** para **float** ou **real** pode causar perda de precisão. Convertendo de **int**, **smallint**, **tinyint**, **float**, **real**, **money** , ou **smallmoney** como **decimal** ou **numérico** pode causar um estouro.
  
Por padrão, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa arredondamento ao converter um número para um **decimal** ou **numérico** valor com uma precisão e escala inferiores. Porém, se a opção SET ARITHABORT for ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] irá gerar um erro quando acontecer o estouro. Apenas a perda de precisão e escala não é suficiente para gerar um erro.
  
Ao converter valores reais ou flutuantes em valores decimais ou numéricos, o valor decimal nunca terá mais de 17 decimais. Qualquer valor flutuante < 5E-18 será sempre convertido em 0.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir cria uma tabela usando o **decimal** e **numérico** tipos de dados.  Os valores são inseridos em cada coluna e os resultados são retornados usando uma instrução SELECT.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyDecimalColumn decimal(5,2)  
,MyNumericColumn numeric(10,5)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (123, 12345.12);  
GO  
SELECT MyDecimalColumn, MyNumericColumn  
FROM dbo.MyTable;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyDecimalColumn                         MyNumericColumn  
--------------------------------------- ---------------------------------------  
123.00                                  12345.12000  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Consulte também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
