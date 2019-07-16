---
title: Altera o tipo de dados de data e hora | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6bc7e07ab65b5894c3ac2b913e5d4afcbd4f98f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076959"
---
# <a name="datetime-data-type-changes"></a>Alterações de tipo de dados datetime
Em ODBC *3.x*, os identificadores de data, hora e tipos de dados SQL de carimbo de hora foram alterados de SQL_DATE, SQL_TIME e SQL_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 9, 10 e 11) para SQL _ TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 91, 92 e 93), respectivamente. Os identificadores de tipo C correspondentes foram alterados de SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME e SQL_C_TYPE_TIMESTAMP, respectivamente.  
  
 O tamanho da coluna e dígitos decimais retornados para os tipos de dados de data e hora do SQL no ODBC *3.x* são o mesmo que a precisão e escala retornou para elas no ODBC *2.x*. Esses valores são diferentes dos valores nos campos de descritor de SQL_DESC_PRECISION e SQL_DESC_SCALE. (Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).)  
  
 Essas alterações afetam **SQLDescribeCol**, **SQLDescribeParam**, e **SQLColAttribute**; **SQLBindCol**, **SQLBindParameter**, e **SQLGetData**; e **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**, **SQLStatistics**, e **SQLSpecialColumns**.  
  
 A tabela a seguir mostra como o ODBC *3.x* Gerenciador de Driver executa o mapeamento de data, hora e carimbo de hora C de tipos de dados inserida na *TargetType* argumentos de **SQLBindCol**e **SQLGetData** ou o *ValueType* argumento do **SQLBindParameter**.  
  
|Tipo de dados<br /><br /> código digitado|*2. x* aplicativo<br /><br /> *2. x* driver|*2. x* aplicativo<br /><br /> *3. x* driver|*3. x* aplicativo<br /><br /> *2. x* driver|*3. x* aplicativo<br /><br /> *3. x* driver|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|Nenhum mapeamento|SQL_C_TYPE_DATE (91)|Nenhum mapeamento [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|Erro (do DM)|Erro (do DM)|SQL_C_DATE (9)|Nenhum mapeamento [2]|  
|SQL_C_TIME (10)|Nenhum mapeamento|SQL_C_TYPE_TIME (92)|Nenhum mapeamento [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|Erro (do DM)|Erro (do DM)|SQL_C_TIME (10)|Nenhum mapeamento [2]|  
|SQL_C_TIMESTAMP (11)|Nenhum mapeamento|SQL_C_TYPE_TIMESTAMP (93)|Nenhum mapeamento [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|Erro (do DM)|Erro (do DM)|SQL_C_TIMESTAMP (11)|Nenhum mapeamento [2]|  
  
 [1] como resultado de isso, um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver pode usar os códigos de data, hora ou carimbo de hora retornados nos conjuntos de resultados são retornados pelas funções de catálogo.  
  
 [2] como resultado de isso, um ODBC *3.x* aplicativo trabalhar com ODBC *3.x* driver pode usar os códigos de data, hora ou carimbo de hora retornados nos conjuntos de resultados são retornados pelas funções de catálogo.  
  
 A tabela a seguir mostra como o ODBC *3.x* Gerenciador de Driver executa o mapeamento de data, hora e carimbo de hora SQL de tipos de dados inserida na *ParameterType* argumento de **SQLBindParameter**  ou o *DataType* argumento da **SQLGetTypeInfo**.  
  
|Tipo de dados<br /><br /> código digitado|*2. x* aplicativo<br /><br /> *2. x* driver|*2. x* aplicativo<br /><br /> *3. x* driver|*3. x* aplicativo<br /><br /> *2. x* driver|*3. x* aplicativo<br /><br /> *3. x* driver|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|Nenhum mapeamento|SQL_TYPE_DATE (91)|Nenhum mapeamento [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|Erro (do DM)|Erro (do DM)|SQL_DATE (9)|Nenhum mapeamento [2]|  
|SQL_TIME (10)|Nenhum mapeamento|SQL_TYPE_TIME (92)|Nenhum mapeamento [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|Erro (do DM)|Erro (do DM)|SQL_TIME (10)|Nenhum mapeamento [2]|  
|SQL_TIMESTAMP (11)|Nenhum mapeamento|SQL_TYPE_TIMESTAMP (93)|Nenhum mapeamento [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|Erro (do DM)|Erro (do DM)|SQL_TIMESTAMP (11)|Nenhum mapeamento [2]|  
  
 [1] como resultado de isso, um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver pode usar os códigos de data, hora ou carimbo de hora retornados nos conjuntos de resultados são retornados pelas funções de catálogo.  
  
 [2] como resultado de isso, um ODBC *3.x* aplicativo trabalhar com ODBC *3.x* driver pode usar os códigos de data, hora ou carimbo de hora retornados nos conjuntos de resultados são retornados pelas funções de catálogo.
