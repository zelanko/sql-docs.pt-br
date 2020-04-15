---
title: Data-hora Tipos de dados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10626c4f0bf2e33c70322a0eb49af6c3e01e4303
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307057"
---
# <a name="datetime-data-types"></a>Tipo de dados datetime
No ODBC *3.x*, os identificadores para os tipos de dados SQL de data, hora e carimbo de data foram alterados de SQL_DATE, SQL_TIME e SQL_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 9, 10 e 11) para SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 91, 92 e 93), respectivamente. Os identificadores de tipo C correspondentes mudaram de SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP para SQL_C_TYPE_DATE, SQL_C_TYPE_TIME e SQL_C_TYPE_TIMESTAMP, respectivamente, e as ocorrências de **#define** mudaram em conformidade.  
  
 O tamanho da coluna e os dígitos decimais retornados para os tipos de dados de data-hora SQL no ODBC *3.x* são os mesmos que a precisão e a escala retornadas para eles em ODBC *2.x*. Esses valores são diferentes dos valores nos campos descritor SQL_DESC_PRECISION e SQL_DESC_SCALE. (Para obter mais informações, consulte [Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no apêndice D: Tipos de dados.)  
  
 Essas alterações afetam **sqldescribecol,** **SQLDescribeParam**e **SQLColAttributes;** **SQLBindCol,** **SQLBindParameter**e **SQLGetData;** e **SQLColumns,** **SQLGetTypeInfo,** **SQLProcedureColumns,** **SQLStatistics**e **SQLSpecialColumns**.  
  
 Um driver ODBC *3.x* processa as chamadas de função listadas no parágrafo anterior de acordo com a configuração do SQL_ATTR_ODBC_VERSION atributo do ambiente. Para **SQLColumns,** **SQLGetTypeInfo,** **SQLProcedureColumns,** **SQLSpecialColumns**e **SQLStatistics,** se SQL_ATTR_ODBC_VERSION estiver definido para SQL_OV_ODBC3, as funções retornam SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP no campo DATA_TYPE. A coluna COLUMN_SIZE (no conjunto de resultados retornado por **SQLColumns,** **SQLGetTypeInfo,** **SQLProcedureColumns**e **SQLSpecialColumns)** contém a precisão binária para o tipo numérico aproximado. A coluna NUM_PREC_RADIX (no conjunto de resultados retornado por **SQLColumns,** **SQLGetTypeInfo**e **SQLProcedureColumns)** contém um valor de 2. Se SQL_ATTR_ODBC_VERSION estiver definido para SQL_OV_ODBC2, então as funções retornam SQL_DATE, SQL_TIME e SQL_TIMESTAMP no campo DATA_TYPE, a coluna COLUMN_SIZE contém a precisão decimal para o tipo numérico aproximado, e a NUM_PREC_RADIX coluna contém um valor de 10.  
  
 Quando todos os tipos de dados forem solicitados em uma chamada para **SQLGetTypeInfo,** o conjunto de resultados retornado pela função conterá SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP como definido no ODBC *3.x*, e SQL_DATE, SQL_TIME e SQL_TIMESTAMP conforme definido no ODBC *2.x*.  
  
 Devido à forma como o ODBC *3.x* Driver Manager realiza o mapeamento dos tipos de dados de data, hora e carimbo de tempo, os drivers ODBC *3.x* só precisam reconhecer **#defines** de 91, 92 e 93 para os tipos de dados C de data, hora e carimbo de tempo inseridos nos argumentos *TargetType* de **SQLBindCol** e **SQLGetData** ou do argumento *ValueType* do **SQLBindParameter**, e precisam apenas reconhecer **#defines** de 91, 92 e 93 para os tipos de dados SQL de data, hora e carimbo de hora inseridos no argumento *ParameterType* do **SQLBindParameter** ou no argumento *DataType* de **SQL** Para obter mais informações, consulte [Alterações do tipo de dados de data de data .](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
