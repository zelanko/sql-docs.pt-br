---
title: "Diagnóstico do descritor, informações, tipos específicos de driver - dados, | Microsoft Docs"
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
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ccf90b309c6a2355612546e82c2181988879520
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de dados específica do driver, tipos de descritor, tipos de informação, tipos de diagnóstico e atributos
Drivers podem alocar valores específicos de driver para o seguinte:  
  
-   **Indicadores de tipo de dados do SQL** são usados em *ParameterType* na **SQLBindParameter** e no *DataType* em **SQLGetTypeInfo** e retornado por **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLGetTypeInfo**,  **SQLDescribeParam**, **SQLProcedureColumns**, e **SQLSpecialColumns**.  
  
-   **Campos de descritor** são usados em *FieldIdentifier* na **SQLColAttribute**, **SQLGetDescField**, e **SQLSetDescField** .  
  
-   **Campos de diagnóstico** são usados em *DiagIdentifier* na **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   **Tipos de informações** são usados em *informação* na **SQLGetInfo**.  
  
-   **Atributos de instrução e Conexão** são usados em *atributo* na **SQLGetConnectAttr**, **SQLGetStmtAttr**,  **SQLSetConnectAttr**, e **SQLSetStmtAttr**.  
  
 Para cada um desses itens, há dois conjuntos de valores: valores reservados para uso pelo ODBC e os valores reservados para uso pelos drivers. Antes de implementar valores específicos do driver, um gravador de driver deve solicitar um valor para cada tipo específico de driver, o campo ou o atributo do Open Group. Para novos desenvolvimentos do driver, use o intervalo descrito na tabela a seguir. O Gerenciador de Driver do ODBC 3.8 não irá gerar um erro se for usado um valor desconhecido que não está no intervalo descrito abaixo. No entanto, em versões posteriores do Gerenciador de Driver poderá gerar um erro se valores desconhecidos são recebidos que não estão no intervalo.  
  
 Quando qualquer um desses valores é passado para uma função ODBC, o driver deve verificar se o valor é válido. Drivers retornam SQLSTATE HYC00 (recurso opcional não implementado) para valores específicos de driver que se aplicam a outros drivers.  
  
 Começando com o ODBC 3.8, gravadores de driver podem alocar atributos específicos do driver em um intervalo reservado.  
  
> [!NOTE]  
>  O Gerenciador de Driver do ODBC 3.8 valida nem impõe esses intervalos para compatibilidade com versões anteriores. Uma versão futura do Gerenciador de Driver pode aplicá-las, no entanto.  
  
|Tipo de atributo|Tipo de dados ODBC|Intervalo de específicos de driver base|Limite de intervalo específico de driver|Constante ODBC para o intervalo de valor específico do driver de base|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|Indicadores de tipo de dados SQL|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|Campos de descritor|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|Campos de diagnóstico|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|Tipos de informações|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|Atributos de Conexão|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|Atributos de instrução|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  Tipos de dados específica do driver, campos de descritor, campos de diagnóstico, tipos de informação, atributos de instrução e atributos de conexão devem ser descritos na documentação do driver. Quando qualquer um desses valores é passado para uma função ODBC, o driver deve verificar se o valor é válido. Drivers retornam SQLSTATE HYC00 (recurso opcional não implementado) para valores específicos de driver que se aplicam a outros drivers.  
  
 Os valores de base são definidos para facilitar o desenvolvimento de driver. Por exemplo, os atributos de diagnóstico específicos de driver podem ser definidos no seguinte formato:  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
