---
title: Mudanças no tipo de dados de data-hora | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f186047dd31aa2c4b66ec1ce73c8cb9fae31c04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304639"
---
# <a name="datetime-data-type-changes"></a>Alterações de tipo de dados datetime
No ODBC *3.x*, os identificadores para os tipos de dados SQL de data, hora e carimbo de data foram alterados de SQL_DATE, SQL_TIME e SQL_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 9, 10 e 11) para SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 91, 92 e 93), respectivamente. Os identificadores de tipo C correspondentes mudaram de SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP para SQL_C_TYPE_DATE, SQL_C_TYPE_TIME e SQL_C_TYPE_TIMESTAMP, respectivamente.  
  
 O tamanho da coluna e os dígitos decimais retornados para os tipos de dados de data-hora SQL no ODBC *3.x* são os mesmos que a precisão e a escala retornadas para eles em ODBC *2.x*. Esses valores são diferentes dos valores nos campos descritor SQL_DESC_PRECISION e SQL_DESC_SCALE. (Para obter mais informações, consulte [Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho do display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).)  
  
 Essas alterações afetam **sqldescribecol,** **SQLDescribeParam**e **SQLColAttribute;** **SQLBindCol,** **SQLBindParameter**e **SQLGetData;** e **SQLColumns,** **SQLGetTypeInfo,** **SQLProcedureColumns,** **SQLStatistics**e **SQLSpecialColumns**.  
  
 A tabela a seguir mostra como o ODBC *3.x* Driver Manager realiza o mapeamento dos tipos de dados de data, hora e carimbo de ponto de ponto de data c inseridos nos argumentos *TargetType* de **SQLBindCol** e **SQLGetData** ou no argumento *ValueType* do **SQLBindParameter**.  
  
|Tipo de dados<br /><br /> código inserido|*2.x* aplicativo para<br /><br /> *Driver 2.x*|*2.x* aplicativo para<br /><br /> *Driver 3.x*|*Aplicativo 3.x* para<br /><br /> *Driver 2.x*|*Aplicativo 3.x* para<br /><br /> *Driver 3.x*|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|Sem mapeamento|SQL_C_TYPE_DATE (91)|Nenhum mapeamento[1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|Erro (do DM)|Erro (do DM)|SQL_C_DATE (9)|Nenhum mapeamento[2]|  
|SQL_C_TIME (10)|Sem mapeamento|SQL_C_TYPE_TIME (92)|Nenhum mapeamento[1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|Erro (do DM)|Erro (do DM)|SQL_C_TIME (10)|Nenhum mapeamento[2]|  
|SQL_C_TIMESTAMP (11)|Sem mapeamento|SQL_C_TYPE_TIMESTAMP (93)|Nenhum mapeamento[1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|Erro (do DM)|Erro (do DM)|SQL_C_TIMESTAMP (11)|Nenhum mapeamento[2]|  
  
 [1] Como resultado disso, um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* pode usar os códigos de data, hora ou carimbo de data retornados nos conjuntos de resultados que são retornados pelas funções do catálogo.  
  
 [2] Como resultado disso, um aplicativo ODBC *3.x* que trabalha com um driver ODBC *3.x* pode usar os códigos de data, hora ou carimbo de data retornados nos conjuntos de resultados que são retornados pelas funções do catálogo.  
  
 A tabela a seguir mostra como o ODBC *3.x* Driver Manager realiza o mapeamento dos tipos de dados SQL de data, hora e carimbo de ponto de hora inseridos no argumento *ParameterType* do **SQLBindParameter** ou no argumento *DataType* do **SQLGetTypeInfo**.  
  
|Tipo de dados<br /><br /> código inserido|*2.x* aplicativo para<br /><br /> *Driver 2.x*|*2.x* aplicativo para<br /><br /> *Driver 3.x*|*Aplicativo 3.x* para<br /><br /> *Driver 2.x*|*Aplicativo 3.x* para<br /><br /> *Driver 3.x*|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|Sem mapeamento|SQL_TYPE_DATE (91)|Nenhum mapeamento[1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|Erro (do DM)|Erro (do DM)|SQL_DATE (9)|Nenhum mapeamento[2]|  
|SQL_TIME (10)|Sem mapeamento|SQL_TYPE_TIME (92)|Nenhum mapeamento[1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|Erro (do DM)|Erro (do DM)|SQL_TIME (10)|Nenhum mapeamento[2]|  
|SQL_TIMESTAMP (11)|Sem mapeamento|SQL_TYPE_TIMESTAMP (93)|Nenhum mapeamento[1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|Erro (do DM)|Erro (do DM)|SQL_TIMESTAMP (11)|Nenhum mapeamento[2]|  
  
 [1] Como resultado disso, um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* pode usar os códigos de data, hora ou carimbo de data retornados nos conjuntos de resultados que são retornados pelas funções do catálogo.  
  
 [2] Como resultado disso, um aplicativo ODBC *3.x* que trabalha com um driver ODBC *3.x* pode usar os códigos de data, hora ou carimbo de data retornados nos conjuntos de resultados que são retornados pelas funções do catálogo.
