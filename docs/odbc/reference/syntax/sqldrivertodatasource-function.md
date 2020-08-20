---
description: Função SQLDriverToDataSource
title: Função SQLDriverToDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverToDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverToDataSource
helpviewer_keywords:
- SQLDriverToDataSource function [ODBC]
ms.assetid: 0de28eb5-8aa9-43e4-a87f-7dbcafe800dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da885e3be81a7a7de04a58bbb92725317477e80e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461137"
---
# <a name="sqldrivertodatasource-function"></a>Função SQLDriverToDataSource
O **SQLDriverToDataSource** dá suporte a traduções para drivers ODBC. Essa função não é chamada por aplicativos habilitados para ODBC; os aplicativos solicitam a conversão por meio de **SQLSetConnectAttr**. O driver associado ao *ConnectionHandle* especificado em **SQLSETCONNECTATTR** chama a DLL especificada para executar traduções de todos os dados que fluem do driver para a fonte de dados. Uma DLL de tradução padrão pode ser especificada no arquivo de inicialização ODBC.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLDriverToDataSource(  
     UDWORD     fOption,  
     SWORD      fSqlType,  
     PTR        rgbValueIn,  
     SDWORD     cbValueIn,  
     PTR        rgbValueOut,  
     SDWORD     cbValueOutMax,  
     SDWORD *   pcbValueOut,  
     UCHAR *    szErrorMsg,  
     SWORD      cbErrorMsgMax,  
     SWORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>Argumentos  
 *fOption*  
 Entrada Valor da opção.  
  
 *fSqlType*  
 Entrada O tipo de dados SQL ODBC. Esse argumento informa ao driver como converter *rgbValueIn* em um formato aceitável pela fonte de dados. Para obter uma lista de tipos de dados SQL válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md).  
  
 *rgbValueIn*  
 Entrada Valor a ser convertido.  
  
 *cbValueIn*  
 Entrada Comprimento de *rgbValueIn*.  
  
 *rgbValueOut*  
 Der Resultado da tradução.  
  
> [!NOTE]  
>  A DLL de tradução não é nula – Finalize esse valor.  
  
 *cbValueOutMax*  
 Entrada Comprimento de *rgbValueOut*.  
  
 *pcbValueOut*  
 Der O número total de bytes (excluindo o byte de terminação nula) disponível para retornar em *rgbValueOut*.  
  
 Para dados de caracteres ou binários, se for maior ou igual a *cbValueOutMax*, os dados em *rgbValueOut* serão truncados para *cbValueOutMax* bytes.  
  
 Para todos os outros tipos de dados, o valor de *cbValueOutMax* é ignorado e a DLL de tradução pressupõe que o tamanho de *rgbValueOut* é o tamanho do tipo de dados C padrão do tipo de dados SQL especificado com *fSqlType*.  
  
 O argumento *pcbValueOut* pode ser um ponteiro nulo.  
  
 *szErrorMsg*  
 Der Ponteiro para armazenamento de uma mensagem de erro. Esta é uma cadeia de caracteres vazia, a menos que a tradução tenha falhado.  
  
 *cbErrorMsgMax*  
 Entrada Comprimento de *szErrorMsg*.  
  
 *pcbErrorMsg*  
 Der Aponta para o número total de bytes (excluindo o byte de terminação nula) disponível para retornar em *szErrorMsg*. Se for maior ou igual a *cbErrorMsg*, os dados em *szErrorMsg* serão truncados para *cbErrorMsgMax* menos o caractere de terminação nula. O argumento *pcbErrorMsg* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 TRUE se a tradução for bem-sucedida, FALSE se a tradução tiver falhado.  
  
## <a name="comments"></a>Comentários  
 O driver chama **SQLDriverToDataSource** para converter todos os dados (instruções SQL, parâmetros e assim por diante) passando do driver para a fonte de dados. A DLL de tradução pode não converter alguns dados, dependendo do tipo de dados e da finalidade da DLL de tradução. Por exemplo, uma DLL que traduz dados de caractere de uma página de código para outra ignora todos os dados numéricos e binários.  
  
 O valor de *fOption* é definido como o valor de *VParam* especificado chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION. É um valor de 32 bits que tem um significado específico para uma determinada DLL de tradução. Por exemplo, ele pode especificar uma determinada tradução de conjunto de caracteres.  
  
 Se o mesmo buffer for especificado para *rgbValueIn* e *rgbValueOut*, a conversão de dados no buffer será executada no local.  
  
 Embora *cbValueIn*, *cbValueOutMax*e *pcbValueOut* sejam do tipo SDWORD, **SQLDriverToDataSource** não necessariamente oferece suporte a ponteiros enormes.  
  
 Se **SQLDriverToDataSource** retornar false, o truncamento de dados poderá ter ocorrido durante a tradução. Se *pcbValueOut* (o número de bytes disponíveis para retornar no buffer de saída) for maior que *cbValueOutMax* (o comprimento do buffer de saída), o truncamento ocorrerá. O driver deve determinar se o truncamento foi aceitável ou não. Se o truncamento não ocorreu, o **SQLDriverToDataSource** retornou false devido a outro erro. Em ambos os casos, uma mensagem de erro específica é retornada em *szErrorMsg*.  
  
 Para obter mais informações sobre a tradução de dados, consulte [DLLs de tradução](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Convertendo dados retornados da fonte de dados|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|Retornando a configuração de um atributo de conexão|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definindo um atributo de conexão|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
