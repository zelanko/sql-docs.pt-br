---
title: Tipos de dados DateTime | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307057"
---
# <a name="datetime-data-types"></a>Tipo de dados datetime
No ODBC *3. x*, os identificadores dos tipos de dados de data, hora e timestamp SQL foram alterados de SQL_DATE, SQL_TIME e SQL_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 9, 10 e 11) para SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP (com instâncias de **#define** no arquivo de cabeçalho de 91, 92 e 93), respectivamente. Os identificadores de tipo de C correspondentes foram alterados de SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP para SQL_C_TYPE_DATE, SQL_C_TYPE_TIME e SQL_C_TYPE_TIMESTAMP, respectivamente, e as instâncias de **#define** foram alteradas de acordo.  
  
 O tamanho da coluna e os dígitos decimais retornados para os tipos de dados DateTime do SQL no ODBC *3. x* são iguais à precisão e escala retornados para eles no ODBC *2. x*. Esses valores são diferentes dos valores nos campos SQL_DESC_PRECISION e descritor de SQL_DESC_SCALE. (Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.)  
  
 Essas alterações afetam **SQLDescribeCol**, **SQLDescribeParam**e **SQLColAttributes**; **SQLBindCol**, **SQLBindParameter**e **SQLGetData**; **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLStatistics** **e** **SQLSpecialColumns**.  
  
 Um driver ODBC *3. x* processa as chamadas de função listadas no parágrafo anterior de acordo com a configuração do atributo de ambiente SQL_ATTR_ODBC_VERSION. Para **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLSpecialColumns**e **sqlstatistics**, se SQL_ATTR_ODBC_VERSION for definido como SQL_OV_ODBC3, as funções retornarão SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP no campo DATA_TYPE. A coluna COLUMN_SIZE (no conjunto de resultados retornado por **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**e **SQLSpecialColumns**) contém a precisão binária para o tipo numérico aproximado. A coluna NUM_PREC_RADIX (no conjunto de resultados retornado por **SQLColumns**, **SQLGetTypeInfo**e **SQLProcedureColumns**) contém um valor de 2. Se SQL_ATTR_ODBC_VERSION for definido como SQL_OV_ODBC2, as funções retornarão SQL_DATE, SQL_TIME e SQL_TIMESTAMP no campo DATA_TYPE, a coluna COLUMN_SIZE conterá a precisão decimal para o tipo numérico aproximado e a coluna NUM_PREC_RADIX conterá um valor de 10.  
  
 Quando todos os tipos de dados são solicitados em uma chamada para **SQLGetTypeInfo**, o conjunto de resultados retornado pela função conterá SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP conforme definido no ODBC *3. x*e SQL_DATE, SQL_TIME e SQL_TIMESTAMP, conforme definido no ODBC *2. x*.  
  
 Por causa de como o Gerenciador de driver ODBC *3. x* executa o mapeamento dos tipos de dados Date, time e timestamp, ODBC *3.* os drivers x precisam reconhecer apenas **#defines** de 91, 92 e 93 para os tipos de dados Date, time e timestamp C inseridos nos argumentos *TargetType* de **SQLBindCol** e **SQLGetData** , ou o argumento *ValueType* de **SQLBindParameter**, e precisam apenas reconhecer **#defines** de 91, 92 e 93 para os tipos de dados de data, hora e carimbo de hora SQL inseridos no argumento *ParameterType* de **SQLBindParameter** ou o argumento *DataType* de **SQLGetTypeInfo** Para obter mais informações, consulte Data [Type DateTime Changes](../../../odbc/reference/develop-app/datetime-data-type-changes.md).
