---
title: Tipos específicos do driver - Dados, Descritor, Informações, Diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19bb2dd113fbeae871892ea510713c638c886e5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305758"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de dados específicos do driver, tipos de descritor, tipos de informações, tipos de diagnóstico e atributos
Os drivers podem alocar valores específicos do driver para o seguinte:  
  
-   **Indicadores de tipo de dados SQL** Estes são usados em *ParameterType* no **SQLBindParameter** e no *DataType* no **SQLGetTypeInfo** e retornados por **SQLColAttribute,** **SQLColumns,** **SQLDescribeCol,** **SQLGetTypeInfo,** **SQLDescribeParam,** **SQLProcedureColumns**e **SQLSpecialColumns**.  
  
-   **Campos descritores** Estes são usados no *FieldIdentifier* em **SQLColAttribute,** **SQLGetDescField**e **SQLSetDescField**.  
  
-   **Campos de Diagnóstico** Estes são usados no *DiagIdentifier* em **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   **Tipos de informações** Estes são usados no *InfoType* no **SQLGetInfo**.  
  
-   **Atributos de conexão e declaração** Estes são usados em *Atributo* em **SQLGetConnectAttr,** **SQLGetStmtAttr,** **SQLSetConnectAttr**e **SQLSetStmtAttr**.  
  
 Para cada um desses itens, existem dois conjuntos de valores: valores reservados para uso pela ODBC e valores reservados para uso pelos drivers. Antes de implementar valores específicos do driver, um motorista deve solicitar um valor para cada tipo, campo ou atributo específico do driver do Grupo Aberto. Para o desenvolvimento de novos drivers, use a faixa descrita na tabela abaixo. O Gerenciador de Driver ODBC 3.8 não gerará um erro se um valor desconhecido for usado que não esteja na faixa descrita abaixo. No entanto, versões posteriores do Driver Manager podem gerar um erro se valores desconhecidos forem recebidos que não estejam no intervalo.  
  
 Quando qualquer um desses valores é passado para uma função ODBC, o motorista deve verificar se o valor é válido. Os drivers retornam SQLSTATE HYC00 (recurso opcional não implementado) para valores específicos do driver que se aplicam a outros drivers.  
  
 A partir do ODBC 3.8, os roteiristas de driver podem alocar atributos específicos do driver dentro de uma faixa reservada.  
  
> [!NOTE]  
>  O Gerenciador de Driver ODBC 3.8 não valida nem impõe essas faixas para compatibilidade retrógrada. Uma versão futura do Driver Manager pode aplicá-los, no entanto.  
  
|Tipo de atributo|Tipo de dados ODBC|Base de faixa específica do driver|Limite de intervalo específico do motorista|Constante ODBC para base de valor específica do driver|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|Indicadores de tipo de dados SQL|SQLSMALLINT|0x4000|0x7fff|SQL_DRIVER_SQL_TYPE_BASE|  
|Campos descritores|SQLSMALLINT|0x4000|0x7fff|SQL_DRIVER_DESCRIPTOR_BASE|  
|Campos de diagnóstico|SQLSMALLINT|0x4000|0x7fff|SQL_DRIVER_DIAGNOSTIC_BASE|  
|Tipos de informações|SQLUSMALLINT|0x4000|0x7fff|SQL_DRIVER_INFO_TYPE_BASE|  
|Atributos de conexão|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|Atributos de declaração|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  Tipos de dados específicos do driver, campos de descritores, campos de diagnóstico, tipos de informações, atributos de declaração e atributos de conexão devem ser descritos na documentação do driver. Quando qualquer um desses valores é passado para uma função ODBC, o motorista deve verificar se o valor é válido. Os drivers retornam SQLSTATE HYC00 (recurso opcional não implementado) para valores específicos do driver que se aplicam a outros drivers.  
  
 Os valores base são definidos para facilitar o desenvolvimento do driver. Por exemplo, atributos diagnósticos específicos do driver podem ser definidos no seguinte formato:  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
