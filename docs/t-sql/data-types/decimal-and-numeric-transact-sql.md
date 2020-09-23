---
title: decimal e numeric (Transact-SQL) | Microsoft Docs
description: Referência de Transact-SQL para os tipos de dados decimal e numeric. Decimal e numeric são sinônimos de tipos de dados numéricos que têm uma precisão e uma escala fixas.
ms.date: 09/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- decimal
- decimal_TSQL
- numeric
- numeric_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decimal data type
- decimal data type, about decimal data type
- numeric data type
- numeric data type, about numeric data type
ms.assetid: 9d862a90-e6b7-4692-8605-92358dccccdf
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 05c7ee73b7f37cdc96847f546db11f351b5edd68
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116164"
---
# <a name="decimal-and-numeric-transact-sql"></a>decimal e numeric (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Tipos de dados numéricos que têm precisão e escala fixos. Decimal e numeric são sinônimos e podem ser usados intercambiavelmente.
  
## <a name="arguments"></a>Argumentos
**decimal**[ **(** _p_[ **,** _s_] **)** ] e **numeric**[ **(** _p_[ **,** _s_] **)** ]  
Números de precisão e escala fixos. Quando a precisão máxima for usada, os valores válidos serão de - 10^38 +1 a 10^38 - 1. Os sinônimos ISO para **decimal** são **dez** e **dec(** _p_, _s_ **)** . **numeric** é funcionalmente equivalente a **decimal**.
  
p (precisão)  
O número total máximo de dígitos decimais a ser armazenados. Esse número inclui o que está à direita e à esquerda do ponto decimal. A precisão deve ser um valor de 1 até a precisão máxima de 38. A precisão padrão é 18.
  
> [!NOTE]  
>  Informatica é compatível apenas com 16 dígitos significativos, independentemente da precisão e da escala especificadas.  
  
*s* (escala)  
O número máximo de dígitos decimais que são armazenados à direita do ponto decimal. Esse número é subtraído de *p* para determinar o número máximo de dígitos à esquerda do separador decimal. A escala deve ser um valor de 0 a *p*, e só poderá ser especificada se a precisão for definida. A escala padrão é 0; portanto, 0 <= *s* \<= *p*. Os tamanhos máximos de armazenamento variam, com base na precisão.
  
|Precisão|Bytes de armazenamento|  
|---|---|
|1 - 9|5|  
|10–19|9|  
|20–28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica (conectado por meio do conector do SQL Server PDW Informatica) é compatível apenas com 16 dígitos significativos, independentemente da precisão e da escala especificadas.  
  
## <a name="converting-decimal-and-numeric-data"></a>Convertendo dados decimais e numéricos
Para os tipos de dados **decimal** e **numeric**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera cada combinação de precisão e escala como um tipo de dados diferente. Por exemplo, **decimal(5,5)** e **decimal(5,0)** são considerados tipos de dados diferentes.
  
Nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], uma constante com um ponto decimal é convertida automaticamente em um valor de dados **numeric**, usando a escala e a precisão mínimas necessárias. Por exemplo, a constante 12,345 é convertida em um valor **numeric** com uma precisão 5 e uma escala 3.
  
Converter de **decimal** ou **numeric** para **float** ou **real** pode causar perda de precisão. Converter de **int**, **smallint**, **tinyint**, **float**, **real**, **money** ou **smallmoney** para **decimal** ou **numeric** pode causar estouro.
  
Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa arredondamento ao converter um número em um valor **decimal** ou **numeric** com precisão e escala inferiores. Por outro lado, se a opção SET ARITHABORT for ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] irá gerar um erro quando acontecer o estouro. Apenas a perda de precisão e escala não é suficiente para gerar um erro.
  
Antes do [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)], a conversão de valores **float** para **decimal** ou **numeric** era restrita somente a valores com precisão de 17 dígitos. Qualquer valor **float** menor que 5E-18 (quando definido usando a notação científica de 5E-18 ou a notação decimal de 0,0000000000000000050000000000000005) é arredondado para 0. Essa não é mais uma restrição no [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] em diante.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir cria uma tabela usando os tipos de dados **decimal** e **numérico**.  Os valores são inseridos em cada coluna. Os resultados são retornados usando uma instrução SELECT.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyDecimalColumn DECIMAL(5,2)  
,MyNumericColumn NUMERIC(10,5)
  
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
  
## <a name="see-also"></a>Confira também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
