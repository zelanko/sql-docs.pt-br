---
title: Alterações de tipo de dados DateTime | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076959"
---
# <a name="datetime-data-type-changes"></a>Alterações de tipo de dados datetime
No ODBC *3. x*, os identificadores dos tipos de dados de data, hora e timestamp SQL foram alterados de SQL_DATE, SQL_TIME e SQL_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 9, 10 e 11) para SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 91, 92 e 93), respectivamente. Os identificadores de tipo de C correspondentes foram alterados de SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP para SQL_C_TYPE_DATE, SQL_C_TYPE_TIME e SQL_C_TYPE_TIMESTAMP, respectivamente.  
  
 O tamanho da coluna e os dígitos decimais retornados para os tipos de dados DateTime do SQL no ODBC *3. x* são iguais à precisão e escala retornados para eles no ODBC *2. x*. Esses valores são diferentes dos valores nos campos SQL_DESC_PRECISION e descritor de SQL_DESC_SCALE. (Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).)  
  
 Essas alterações afetam **SQLDescribeCol**, **SQLDescribeParam**e **SQLColAttribute**; **SQLBindCol**, **SQLBindParameter**e **SQLGetData**; **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLStatistics** **e** **SQLSpecialColumns**.  
  
 A tabela a seguir mostra como o Gerenciador de driver ODBC *3. x* executa o mapeamento dos tipos de dados Date, time e timestamp C inseridos nos argumentos *TargetType* de **SQLBindCol** e **SQLGetData** ou no argumento *ValueType* de **SQLBindParameter**.  
  
|Tipo de dados<br /><br /> código inserido|aplicativo *2. x* para<br /><br /> Driver *2. x*|aplicativo *2. x* para<br /><br /> Driver *3. x*|aplicativo *3. x* para<br /><br /> Driver *2. x*|aplicativo *3. x* para<br /><br /> Driver *3. x*|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|Nenhum mapeamento|SQL_C_TYPE_DATE (91)|Nenhum mapeamento [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|Erro (de DM)|Erro (de DM)|SQL_C_DATE (9)|Nenhum mapeamento [2]|  
|SQL_C_TIME (10)|Nenhum mapeamento|SQL_C_TYPE_TIME (92)|Nenhum mapeamento [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|Erro (de DM)|Erro (de DM)|SQL_C_TIME (10)|Nenhum mapeamento [2]|  
|SQL_C_TIMESTAMP (11)|Nenhum mapeamento|SQL_C_TYPE_TIMESTAMP (93)|Nenhum mapeamento [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|Erro (de DM)|Erro (de DM)|SQL_C_TIMESTAMP (11)|Nenhum mapeamento [2]|  
  
 [1] como resultado disso, um aplicativo ODBC *3. x* trabalhando com um driver ODBC *2. x* pode usar os códigos de data, hora ou timestamp retornados nos conjuntos de resultados que são retornados pelas funções de catálogo.  
  
 [2] como resultado disso, um aplicativo ODBC *3. x* trabalhando com um driver ODBC *3. x* pode usar os códigos de data, hora ou timestamp retornados nos conjuntos de resultados que são retornados pelas funções de catálogo.  
  
 A tabela a seguir mostra como o Gerenciador de driver ODBC *3. x* executa o mapeamento dos tipos de dados de data, hora e carimbo de hora SQL inseridos no argumento *ParameterType* de **SQLBindParameter** ou no argumento *DataType* de **SQLGetTypeInfo**.  
  
|Tipo de dados<br /><br /> código inserido|aplicativo *2. x* para<br /><br /> Driver *2. x*|aplicativo *2. x* para<br /><br /> Driver *3. x*|aplicativo *3. x* para<br /><br /> Driver *2. x*|aplicativo *3. x* para<br /><br /> Driver *3. x*|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|Nenhum mapeamento|SQL_TYPE_DATE (91)|Nenhum mapeamento [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|Erro (de DM)|Erro (de DM)|SQL_DATE (9)|Nenhum mapeamento [2]|  
|SQL_TIME (10)|Nenhum mapeamento|SQL_TYPE_TIME (92)|Nenhum mapeamento [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|Erro (de DM)|Erro (de DM)|SQL_TIME (10)|Nenhum mapeamento [2]|  
|SQL_TIMESTAMP (11)|Nenhum mapeamento|SQL_TYPE_TIMESTAMP (93)|Nenhum mapeamento [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|Erro (de DM)|Erro (de DM)|SQL_TIMESTAMP (11)|Nenhum mapeamento [2]|  
  
 [1] como resultado disso, um aplicativo ODBC *3. x* trabalhando com um driver ODBC *2. x* pode usar os códigos de data, hora ou timestamp retornados nos conjuntos de resultados que são retornados pelas funções de catálogo.  
  
 [2] como resultado disso, um aplicativo ODBC *3. x* trabalhando com um driver ODBC *3. x* pode usar os códigos de data, hora ou timestamp retornados nos conjuntos de resultados que são retornados pelas funções de catálogo.
