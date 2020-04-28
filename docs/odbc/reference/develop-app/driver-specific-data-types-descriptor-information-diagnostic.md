---
title: Tipos específicos de driver-dados, descritor, informações, diagnóstico | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305758"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de dados específicos do driver, tipos de descritor, tipos de informações, tipos de diagnóstico e atributos
Os drivers podem alocar valores específicos de driver para o seguinte:  
  
-   **Indicadores de tipo de dados SQL** Eles são usados em *ParameterType* em **SQLBindParameter** e em *DataType* em **SQLGetTypeInfo** e retornados por **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLGetTypeInfo**, **SQLDescribeParam**, **SQLProcedureColumns**e **SQLSpecialColumns**.  
  
-   **Campos de descritor** Eles são usados em *FieldIdentifier* em **SQLColAttribute**, **SQLGetDescField**e **SQLSetDescField**.  
  
-   **Campos de diagnóstico** Eles são usados em *DiagIdentifier* em **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   **Tipos de informações** Eles são usados em *InfoType* no **SQLGetInfo**.  
  
-   **Atributos de conexão e instrução** Eles são usados no *atributo* **SQLGetConnectAttr**, **SQLGetStmtAttr**, **SQLSetConnectAttr**e **SQLSetStmtAttr**.  
  
 Para cada um desses itens, há dois conjuntos de valores: valores reservados para uso pelo ODBC e valores reservados para uso por drivers. Antes de implementar valores específicos de driver, um gravador de driver deve solicitar um valor para cada tipo específico de driver, campo ou atributo de Open Group. Para o novo desenvolvimento de driver, use o intervalo descrito na tabela a seguir. O Gerenciador de driver ODBC 3,8 não gerará um erro se um valor desconhecido for usado, que não esteja no intervalo descrito abaixo. No entanto, as versões posteriores do Gerenciador de driver podem gerar um erro se forem recebidos valores desconhecidos que não estão no intervalo.  
  
 Quando qualquer um desses valores é passado para uma função ODBC, o driver deve verificar se o valor é válido. Os drivers retornam SQLSTATE HYC00 (recurso opcional não implementado) para valores específicos de driver que se aplicam a outros drivers.  
  
 A partir do ODBC 3,8, os gravadores de driver podem alocar atributos específicos de driver dentro de um intervalo reservado.  
  
> [!NOTE]  
>  O Gerenciador de driver ODBC 3,8 nem valida nem impõe esses intervalos para compatibilidade com versões anteriores. No entanto, uma versão futura do Gerenciador de driver pode imaplicá-las.  
  
|Tipo de atributo|Tipo de dados ODBC|Base do intervalo específico do driver|Limite de intervalo específico do driver|Constante ODBC para base de intervalo de valores específicos do driver|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|Indicadores de tipo de dados SQL|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|Campos de descritor|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|Campos de diagnóstico|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|Tipos de informações|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|Atributos de conexão|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|Atributos de instrução|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  Tipos de dados específicos de driver, campos de descritores, campos de diagnóstico, tipos de informações, atributos de instrução e atributos de conexão devem ser descritos na documentação do driver. Quando qualquer um desses valores é passado para uma função ODBC, o driver deve verificar se o valor é válido. Os drivers retornam SQLSTATE HYC00 (recurso opcional não implementado) para valores específicos de driver que se aplicam a outros drivers.  
  
 Os valores de base são definidos para facilitar o desenvolvimento de driver. Por exemplo, os atributos de diagnóstico específicos do driver podem ser definidos no seguinte formato:  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
