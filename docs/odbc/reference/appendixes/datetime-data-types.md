---
title: Tipos de dados de data e hora | Microsoft Docs
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
- data types [ODBC], date
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- data types [ODBC], timestamp
- data types [ODBC], backward compatibility
- compatibility [ODBC], datetime data types
- data types [ODBC], time
ms.assetid: 6b9363c9-04bf-4492-a210-7aa15dea4af8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d546fff544c616d4f2750dba76c4b8e68d21aab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241010"
---
# <a name="datetime-data-types"></a>Tipo de dados datetime
Em ODBC 3 *. x*, os identificadores de data, hora e tipos de dados SQL de carimbo de hora foram alterados de SQL_DATE, SQL_TIME e SQL_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 9, 10 e 11) para SQL _ TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 91, 92 e 93), respectivamente. O tipo correspondente de C identificadores foram alterados de SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME e SQL_C_TYPE_TIMESTAMP, respectivamente e as instâncias de **#define** foram alterados adequadamente.  
  
 O tamanho da coluna e dígitos decimais retornados para os tipos de dados de data e hora do SQL no ODBC 3 *. x* são o mesmo que a precisão e escala retornou para elas no ODBC 2. *x*. Esses valores são diferentes dos valores nos campos de descritor de SQL_DESC_PRECISION e SQL_DESC_SCALE. (Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: Tipos de dados).  
  
 Essas alterações afetam **SQLDescribeCol**, **SQLDescribeParam**, e **SQLColAttributes**; **SQLBindCol**, **SQLBindParameter**, e **SQLGetData**; e **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**, **SQLStatistics**, e **SQLSpecialColumns**.  
  
 Um ODBC 3 *. x* driver processa as chamadas de função listadas no parágrafo anterior de acordo com a configuração do atributo ambiente SQL_ATTR_ODBC_VERSION. Para **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLSpecialColumns**, e **SQLStatistics** , se SQL_ATTR_ODBC_VERSION estiver definido como SQL_OV_ODBC3, as funções de retorno SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP no campo DATA_TYPE. A coluna COLUMN_SIZE (no conjunto de resultados retornado por **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, e **SQLSpecialColumns**) contém a precisão binária para o tipo numérico aproximado. A coluna NUM_PREC_RADIX (no conjunto de resultados retornado por **SQLColumns**, **SQLGetTypeInfo**, e **SQLProcedureColumns**) contém um valor de 2. Se SQL_ATTR_ODBC_VERSION é definido como SQL_OV_ODBC2 e, em seguida, as funções de retorno SQL_DATE, SQL_TIME e SQL_TIMESTAMP no campo DATA_TYPE, a coluna COLUMN_SIZE contém a precisão decimal para o tipo numérico aproximado e a coluna NUM_PREC_RADIX contém um valor de 10.  
  
 Quando todos os tipos de dados são solicitados em uma chamada para **SQLGetTypeInfo**, o conjunto de resultados retornado pela função conterá SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP conforme definido em ODBC 3 *. x*, e SQL_DATE, SQL_TIME e SQL_TIMESTAMP conforme definido no ODBC 2. *x*.  
  
 Devido a como o ODBC 3 *. x* Gerenciador de Driver executa o mapeamento de data, hora e carimbo de hora de tipos de dados, ODBC 3 *. x* drivers precisam apenas reconhecer **#defines** de 91, 92, e 93 para a data, hora e tipos de dados de carimbo de hora C inserido na *TargetType* argumentos do **SQLBindCol** e **SQLGetData** ou o  *ValueType* argumento de **SQLBindParameter**e precisam apenas reconhecer **#defines** de 91, 92 e 93 para a data, hora e tipos de dados SQL de carimbo de hora é inserido no *ParameterType* argumento **SQLBindParameter** ou o *tipo de dados* argumento do **SQLGetTypeInfo**. Para obter mais informações, consulte [alterações de tipo de dados de data e hora](../../../odbc/reference/develop-app/datetime-data-type-changes.md).
