---
title: float e real (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5f955e5d367a17602959f5294f9fb5d393b186b5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="float-and-real-transact-sql"></a>flutuante e real (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de dados numéricos aproximados para uso com dados numéricos de ponto flutuante. Os dados de ponto flutuante são aproximados; portanto, nem todos os valores no intervalo de tipo de dados podem ser representados de maneira exata. O sinônimo ISO para **real** é **float (24)**.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
**float** [ **(***n***)** ] onde  *n*  é o número de bits que são usados para armazenar a mantissa do **float** número em notação científica e, portanto, determina o tamanho de armazenamento e precisão. Se  *n*  for especificado, ele deve ser um valor entre **1** e **53**. O valor padrão de  *n*  é **53**.
  
|*n*valor|Precisão|Tamanho de armazenamento|  
|---|---|---|
|**1-24**|7 dígitos|4 bytes|  
|**25-53**|15 dígitos|8 bytes|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]trata  *n*  como um dos dois valores possíveis. Se **1**<=n<=**24**,  *n*  é tratado como **24**. Se **25**<=n<=**53**,  *n*  é tratado como **53**.  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float**[**(n)**] tipo de dados está em conformidade com o padrão ISO para todos os valores de  *n*  de **1** por meio de **53**. O sinônimo para **dupla precisão** é **float(53)**.
  
## <a name="remarks"></a>Comentários  
  
|Tipo de dados|Intervalo|Armazenamento|  
|---|---|---|
|**float**|- 1,79E+308 a -2,23E-308, 0 e 2,23E-308 a 1,79E+308|Depende do valor de*n*|  
|**real**|- 3,40E + 38 a -1,18E - 38, 0 e 1,18E - 38 a 3,40E + 38|4 bytes|  
  
##  <a name="converting-float-and-real-data"></a>Convertendo dados float e real  
Valores de **float** são truncados quando eles são convertidos em qualquer tipo de inteiro.
  
Quando você deseja converter de **float** ou **real** para dados de caracteres, usando a função de cadeia de caracteres STR é geralmente mais útil do que CAST (). Isso porque STR habilita mais controle nas formatações. Para obter mais informações, consulte [STR &#40; Transact-SQL &#41; ](../../t-sql/functions/str-transact-sql.md) e [funções &#40; Transact-SQL &#41; ](../../t-sql/functions/functions.md).
  
Conversão de **float** valores que usam notação científica para **decimal** ou **numérico** é restrita a valores de precisão de 17 dígitos apenas. Qualquer valor de < 5E-18 Arredonda para baixo para 0.
  
## <a name="see-also"></a>Consulte também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Conversão de tipo de dados &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
