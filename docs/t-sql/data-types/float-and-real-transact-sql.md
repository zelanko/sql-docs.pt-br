---
title: flutuante e real (Transact-SQL)
ms.custom: ''
ms.date: 09/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- float
- real_TSQL
- real
- float_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- numeric data type, floating point
- float data type
- floating point data [SQL Server]
- real data type
ms.assetid: 08ea66b7-624e-4d8b-86bc-750ff76cdfc5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 921f6e0b26f9187f8dcf241996b601e46ba1cb2e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554494"
---
# <a name="float-and-real-transact-sql"></a>flutuante e real (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Tipos de dados numéricos aproximados para uso com dados numéricos de ponto flutuante. Os dados de ponto flutuante são aproximados; portanto, nem todos os valores no intervalo de tipo de dados podem ser representados de maneira exata. O sinônimo ISO de **real** é **float(24)** .
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
**float** [ **(** _n_ **)** ] em que *n* é o número de bits usado para armazenar a mantissa do número **float** na notação científica e, portanto, exige a precisão e o tamanho do armazenamento. Se *n* for especificado, ele precisará ser um valor entre **1** e **53**. O valor padrão de *n* é **53**.
  
|Valor de *n*|Precisão|Tamanho de armazenamento|  
|---|---|---|
|**1-24**|7 dígitos|4 bytes|  
|**25-53**|15 dígitos|8 bytes|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata *n* como um dos dois valores possíveis. Se **1**<=n<=**24**, *n* é tratado como **24**. Se **25**<=n<=**53**, *n* é tratado como **53**.  
  
O tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float**[ **(n)** ] está em conformidade com o padrão ISO para todos os valores de *n* de **1** a **53**. O sinônimo de **double precision** é **float(53)** .

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários  
  
|Tipo de dados|Intervalo|Armazenamento|  
|---|---|---|
|**float**|- 1,79E+308 a -2,23E-308, 0 e 2,23E-308 a 1,79E+308|Depende do valor de *n*|  
|**real**|- 3,40E + 38 a -1,18E - 38, 0 e 1,18E - 38 a 3,40E + 38|4 bytes|  
  
##  <a name="converting-float-and-real-data"></a>Convertendo dados float e real  
Os valores de **float** são truncados quando são convertidos em qualquer tipo de inteiro.
  
Quando desejar fazer a conversão de **float** ou **real** em dados de caractere, normalmente, é mais útil usar a função de cadeia de caracteres STR do que CAST( ). Isso porque STR habilita mais controle nas formatações. Para obter mais informações, consulte [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md) e [Funções &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md).
  
Antes do [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)], a conversão de valores **float** para **decimal** ou **numeric** era restrita somente a valores com precisão de 17 dígitos. Qualquer valor **float** menor que 5E-18 (quando definido usando a notação científica de 5E-18 ou a notação decimal de 0,0000000000000000050000000000000005) é arredondado para 0. Essa não é mais uma restrição no [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] em diante.
  
## <a name="see-also"></a>Confira também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
