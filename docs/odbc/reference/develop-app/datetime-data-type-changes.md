---
title: Altera o tipo de dados datetime | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40d432cd25752c88b6c82209269c1d37a6bf5f63
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="datetime-data-type-changes"></a>Alterações de tipo de dados datetime
Em ODBC 3. *x*, os identificadores de data, hora e tipos de dados SQL timestamp foram alterados de SQL_DATE, SQL_TIME e SQL_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 9, 10 e 11) para SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 91, 92 e 93), respectivamente. Os identificadores de tipo C correspondentes foram alterados desde SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME e SQL_C_TYPE_TIMESTAMP, respectivamente.  
  
 O tamanho de coluna e retornados para os tipos de dados de data/hora do SQL em ODBC 3 casas decimais. *x* tem o mesmo que a precisão e escala retornado para eles no ODBC 2. *x*. Esses valores são diferentes dos valores nos campos de descritor SQL_DESC_PRECISION e SQL_DESC_SCALE. (Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).)  
  
 Essas alterações afetam **SQLDescribeCol**, **SQLDescribeParam**, e **SQLColAttribute**; **SQLBindCol**, **SQLBindParameter**, e **SQLGetData**; e **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**, **SQLStatistics**, e **SQLSpecialColumns**.  
  
 A tabela a seguir mostra como o ODBC 3*. x* executa o Gerenciador de Driver mapeamento de data, hora e carimbo de hora C de tipos de dados inserido no *TargetType* argumentos de **SQLBindCol**e **SQLGetData** ou o *ValueType* argumento de **SQLBindParameter**.  
  
|Tipo de dados<br /><br /> código inserido|2.*x* aplicativo<br /><br /> 2.*x* driver|2.*x* aplicativo<br /><br /> 3.*x* driver|3.*x* aplicativo<br /><br /> 2.*x* driver|3.*x* aplicativo<br /><br /> 3.*x* driver|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|Nenhum mapeamento|SQL_C_TYPE_DATE (91)|Nenhum mapeamento [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|Erro (do DM)|Erro (do DM)|SQL_C_DATE (9)|Nenhum mapeamento [2]|  
|SQL_C_TIME (10)|Nenhum mapeamento|SQL_C_TYPE_TIME (92)|Nenhum mapeamento [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|Erro (do DM)|Erro (do DM)|SQL_C_TIME (10)|Nenhum mapeamento [2]|  
|SQL_C_TIMESTAMP (11)|Nenhum mapeamento|SQL_C_TYPE_TIMESTAMP (93)|Nenhum mapeamento [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|Erro (do DM)|Erro (do DM)|SQL_C_TIMESTAMP (11)|Nenhum mapeamento [2]|  
  
 [1] como resultado de isso, um ODBC 3. *x* aplicativo trabalhando com um ODBC 2. *x* driver pode usar os códigos de data, hora ou carimbo de hora retornados nos conjuntos de resultados retornados pelas funções de catálogo.  
  
 [2] como resultado de isso, um ODBC 3. *x* aplicativo trabalhando com um ODBC 3. *x* driver pode usar os códigos de data, hora ou carimbo de hora retornados nos conjuntos de resultados retornados pelas funções de catálogo.  
  
 A tabela a seguir mostra como o ODBC 3*. x* executa o Gerenciador de Driver mapeamento dos data, hora e carimbo de hora SQL tipos de dados inserido no *ParameterType* argumento de **SQLBindParameter**  ou o *DataType* argumento de **SQLGetTypeInfo**.  
  
|Tipo de dados<br /><br /> código inserido|2.*x* aplicativo<br /><br /> 2.*x* driver|2.*x* aplicativo<br /><br /> 3.*x* driver|3.*x* aplicativo<br /><br /> 2.*x* driver|3.*x* aplicativo<br /><br /> 3.*x* driver|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|Nenhum mapeamento|SQL_TYPE_DATE (91)|Nenhum mapeamento [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|Erro (do DM)|Erro (do DM)|SQL_DATE (9)|Nenhum mapeamento [2]|  
|SQL_TIME (10)|Nenhum mapeamento|SQL_TYPE_TIME (92)|Nenhum mapeamento [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|Erro (do DM)|Erro (do DM)|SQL_TIME (10)|Nenhum mapeamento [2]|  
|SQL_TIMESTAMP (11)|Nenhum mapeamento|SQL_TYPE_TIMESTAMP (93)|Nenhum mapeamento [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|Erro (do DM)|Erro (do DM)|SQL_TIMESTAMP (11)|Nenhum mapeamento [2]|  
  
 [1] como resultado de isso, um ODBC 3. *x* aplicativo trabalhando com um ODBC 2. *x* driver pode usar os códigos de data, hora ou carimbo de hora retornados nos conjuntos de resultados retornados pelas funções de catálogo.  
  
 [2] como resultado de isso, um ODBC 3. *x* aplicativo trabalhando com um ODBC 3. *x* driver pode usar os códigos de data, hora ou carimbo de hora retornados nos conjuntos de resultados retornados pelas funções de catálogo.
