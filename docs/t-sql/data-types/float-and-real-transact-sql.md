---
title: float e real (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 40
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4dbe0f65cd06b9f9ad3ff5b164c16317a8fd5080
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452500"
---
# <a name="float-and-real-transact-sql"></a>flutuante e real (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de dados numéricos aproximados para uso com dados numéricos de ponto flutuante. Os dados de ponto flutuante são aproximados; portanto, nem todos os valores no intervalo de tipo de dados podem ser representados de maneira exata. O sinônimo ISO de **real** é **float(24)**.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
**float** [ **(***n***)** ] Em que *n* é o número de bits usados para armazenar a mantissa do número **float** em notação científica e, portanto, exige a precisão e o tamanho do armazenamento. Se *n* for especificado, ele precisará ser um valor entre **1** e **53**. O valor padrão de *n* é **53**.
  
|Valor de *n*|Precisão|Tamanho de armazenamento|  
|---|---|---|
|**1-24**|7 dígitos|4 bytes|  
|**25-53**|15 dígitos|8 bytes|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata *n* como um dos dois valores possíveis. Se **1**<=n<=**24**, *n* é tratado como **24**. Se **25**<=n<=**53**, *n* é tratado como **53**.  
  
O tipo de dados **float**[**(n)**] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em conformidade com o padrão ISO para todos os valores de *n* de **1** a **53**. O sinônimo de **double precision** é **float(53)**.
  
## <a name="remarks"></a>Remarks  
  
|Tipo de dados|Intervalo|Armazenamento|  
|---|---|---|
|**float**|- 1,79E+308 a -2,23E-308, 0 e 2,23E-308 a 1,79E+308|Depende do valor de *n*|  
|**real**|- 3,40E + 38 a -1,18E - 38, 0 e 1,18E - 38 a 3,40E + 38|4 bytes|  
  
##  <a name="converting-float-and-real-data"></a>Convertendo dados float e real  
Os valores de **float** são truncados quando são convertidos em qualquer tipo de inteiro.
  
Quando desejar fazer a conversão de **float** ou **real** em dados de caractere, normalmente, é mais útil usar a função de cadeia de caracteres STR do que CAST( ). Isso porque STR habilita mais controle nas formatações. Para obter mais informações, consulte [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md) e [Funções &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md).
  
A conversão de valores **float** que usam notação científica para **decimal** ou **numeric** é restrita a valores de precisão de 17 dígitos apenas. Qualquer valor < 5E-18 é arredondado para 0.
  
## <a name="see-also"></a>Confira também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
