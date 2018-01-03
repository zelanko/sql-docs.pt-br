---
title: "Função SQLDataSourceToDriver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLDataSourceToDriver
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDataSourceToDriver
helpviewer_keywords: SQLDataSourceToDriver function [ODBC]
ms.assetid: 0d87fcac-30a0-4303-ad8f-a5b53f4b428d
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d09d649bc53a08ff7389413882bb338d9713ffc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqldatasourcetodriver-function"></a>Função SQLDataSourceToDriver
**SQLDataSourceToDriver** supportstranslations para drivers ODBC. Essa função não é chamada por aplicativos habilitados para ODBC. os aplicativos solicitam tradução por meio de **SQLSetConnectAttr**. O driver associado a *identificador da conexão* especificado em **SQLSetConnectAttr** chama o DLL especificado para realizar conversões de todos os dados que fluem da fonte de dados para o driver. Uma DLL de conversão padrão pode ser especificado no arquivo de inicialização de ODBC.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLDataSourceToDriver(  
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
 [Entrada] Valor da opção.  
  
 *fSqlType*  
 [Entrada] O tipo de dados SQL. Esse argumento instrui o driver como converter *rgbValueIn* em um formato aceitável para o aplicativo. Para obter uma lista de tipos de dados SQL válidos, consulte o [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) seção apêndice d: os tipos de dados.  
  
 *rgbValueIn*  
 [Entrada] Valor a converter.  
  
 *cbValueIn*  
 [Entrada] Comprimento de *rgbValueIn*.  
  
 *rgbValueOut*  
 [Saída] Resultado da conversão.  
  
> [!NOTE]  
>  A DLL de conversão não null terminar com esse valor.  
  
 *cbValueOutMax*  
 [Entrada] Comprimento de *rgbValueOut*.  
  
 *pcbValueOut*  
 [Saída] O número total de bytes (excluindo o byte nulo de terminação) disponíveis para retornar em *rgbValueOut*.  
  
 Para caracteres ou dados binários, se isso for maior que ou igual a *cbValueOutMax*, os dados em *rgbValueOut* será truncado para *cbValueOutMax* bytes.  
  
 Para todos os outros tipos de dados, o valor de *cbValueOutMax* é ignorada e a DLL de conversão pressupõe que o tamanho de *rgbValueOut* é o tamanho do tipo de dados C padrão do tipo de dados SQL especificado com *fSqlType*.  
  
 O *pcbValueOut* argumento pode ser um ponteiro nulo.  
  
 *szErrorMsg*  
 [Saída] Ponteiro para o armazenamento para uma mensagem de erro. Isso é uma cadeia de caracteres vazia, a menos que a conversão falha.  
  
 *cbErrorMsgMax*  
 [Entrada] Comprimento de *szErrorMsg*.  
  
 *pcbErrorMsg*  
 [Saída] Ponteiro para o número total de bytes (excluindo o byte nulo de terminação) disponíveis para retornar em *szErrorMsg*. Se isso for maior que ou igual a *cbErrorMsg*, os dados em *szErrorMsg* será truncado para *cbErrorMsgMax* menos o caractere null de terminação. O *pcbErrorMsg* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 TRUE se a conversão for bem-sucedida, FALSE se a conversão falhar.  
  
## <a name="comments"></a>Comentários  
 O driver chama **SQLDataSourceToDriver** converter alldata (dados do conjunto de resultados, os nomes de tabela, contagens de linha, mensagens de erro e assim por diante) passagem de dados de origem para o driver. A DLL de conversão não pode converter alguns dados, dependendo do tipo de dados e a finalidade da conversão do DLL; Por exemplo, uma DLL que converte dados de caractere de uma página de código para outro ignora todos os dados numéricos e binários.  
  
 O valor de *fOption* é definido como o valor de *vParam* especificado chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION. É um valor de 32 bits que tem um significado específico para um determinado DLL de conversão. Por exemplo, ele pode especificar que um determinado conjunto de caracteres tradução.  
  
 Se o mesmo buffer for especificado para *rgbValueIn* e *rgbValueOut*, a conversão de dados no buffer será executada in-loco.  
  
 Embora *cbValueIn*, *cbValueOutMax*, e *pcbValueOut* são do tipo SDWORD, **SQLDataSourceToDriver** não necessariamente suporte a ponteiros enormes.  
  
 Se **SQLDataSourceToDriver** retorna FALSE, o truncamento de dados pode ter ocorrido durante a conversão. Se *pcbValueOut* (o número de bytes disponíveis para retornar no buffer de saída) é maior do que *cbValueOutMax* (o comprimento do buffer de saída), em seguida, o truncamento. O driver deve determinar se o truncamento aceitável. Se o truncamento não ocorreu, o **SQLDataSourceToDriver** retornou FALSE devido a outro erro. Em ambos os casos, uma mensagem de erro específico é retornada no *szErrorMsg*.  
  
 Para obter mais informações sobre conversão de dados, consulte [DLLs de conversão](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Convertendo dados sendo enviados para a fonte de dados|[SQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|Retornando a configuração de um atributo de conexão|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definir um atributo de conexão|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
