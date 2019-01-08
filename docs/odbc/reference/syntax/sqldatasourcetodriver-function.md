---
title: Função SQLDataSourceToDriver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSourceToDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSourceToDriver
helpviewer_keywords:
- SQLDataSourceToDriver function [ODBC]
ms.assetid: 0d87fcac-30a0-4303-ad8f-a5b53f4b428d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0ad4a98689db00c6dcb484e7a04bb973d2e1761
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206255"
---
# <a name="sqldatasourcetodriver-function"></a>Função SQLDataSourceToDriver
**SQLDataSourceToDriver** supportstranslations para drivers ODBC. Essa função não é chamada por aplicativos ODBC habilitado; os aplicativos solicitam tradução por meio **SQLSetConnectAttr**. O driver associado a *ConnectionHandle* especificado na **SQLSetConnectAttr** chama a DLL especificada para executar conversões de todos os dados que fluem da fonte de dados para o driver. Uma DLL de conversão padrão pode ser especificado no arquivo de inicialização ODBC.  
  
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
 [Entrada] O tipo de dados SQL. Esse argumento informa o driver como converter *rgbValueIn* em um formato aceitável para o aplicativo. Para obter uma lista dos tipos de dados SQL válidos, consulte o [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) seção no Apêndice d: Tipos de dados.  
  
 *rgbValueIn*  
 [Entrada] Valor a ser movido.  
  
 *cbValueIn*  
 [Entrada] Comprimento da *rgbValueIn*.  
  
 *rgbValueOut*  
 [Saída] Resultado da conversão.  
  
> [!NOTE]  
>  A DLL de conversão não null terminar com esse valor.  
  
 *cbValueOutMax*  
 [Entrada] Comprimento da *rgbValueOut*.  
  
 *pcbValueOut*  
 [Saída] O número total de bytes (excluindo o byte nulo de terminação) disponíveis para retornar na *rgbValueOut*.  
  
 Para caracteres ou dados binários, se isso for maior que ou igual a *cbValueOutMax*, os dados no *rgbValueOut* será truncado com *cbValueOutMax* bytes.  
  
 Para todos os outros tipos de dados, o valor de *cbValueOutMax* será ignorado e a DLL de conversão pressupõe que o tamanho dos *rgbValueOut* é o tamanho do tipo de dados C padrão do tipo de dados SQL especificado com *fSqlType*.  
  
 O *pcbValueOut* argumento pode ser um ponteiro nulo.  
  
 *szErrorMsg*  
 [Saída] Ponteiro para o armazenamento para uma mensagem de erro. Isso é uma cadeia de caracteres vazia, a menos que a conversão falhou.  
  
 *cbErrorMsgMax*  
 [Entrada] Comprimento da *szErrorMsg*.  
  
 *pcbErrorMsg*  
 [Saída] Ponteiro para o número total de bytes (excluindo o byte nulo de terminação) disponíveis para retornar na *szErrorMsg*. Se isso for maior que ou igual a *cbErrorMsg*, os dados no *szErrorMsg* será truncado com *cbErrorMsgMax* menos do caractere nulo de terminação. O *pcbErrorMsg* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 TRUE se a conversão foi bem-sucedida, FALSE se a conversão tiver falhado.  
  
## <a name="comments"></a>Comentários  
 O driver chama **SQLDataSourceToDriver** traduzir alldata (dados do conjunto de resultados, nomes de tabela, contagens de linhas, as mensagens de erro e assim por diante) de passagem dos dados de origem do driver. A DLL de conversão não pode converter alguns dados, dependendo do tipo de dados e a finalidade da conversão do DLL; Por exemplo, uma DLL que converte dados de caractere de uma página de código para outro ignora todos os dados numéricos e binários.  
  
 O valor de *fOption* é definido como o valor de *vParam* especificada chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION. É um valor de 32 bits que tem um significado específico para um determinado DLL de conversão. Por exemplo, ele poderia especificar a que tradução do conjunto de um determinado caractere.  
  
 Se o mesmo buffer é especificado para *rgbValueIn* e *rgbValueOut*, a conversão de dados no buffer será executada em vigor.  
  
 Embora *cbValueIn*, *cbValueOutMax*, e *pcbValueOut* são do tipo SDWORD, **SQLDataSourceToDriver** não necessariamente suporte a ponteiros enormes.  
  
 Se **SQLDataSourceToDriver** retorna FALSE, o truncamento de dados pode ter ocorrido durante a tradução. Se *pcbValueOut* (o número de bytes disponíveis para retornar no buffer de saída) é maior que *cbValueOutMax* (o comprimento do buffer de saída), em seguida, o truncamento ocorreu. O driver deve determinar se o truncamento era aceitável. Se o truncamento não tivesse ocorrido, o **SQLDataSourceToDriver** retornou FALSE devido a outro erro. Em ambos os casos, uma mensagem de erro específico é retornada no *szErrorMsg*.  
  
 Para obter mais informações sobre conversão de dados, consulte [DLLs de conversão](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Conversão de dados sendo enviados para a fonte de dados|[SQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|Retornando a configuração de um atributo de conexão|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definir um atributo de conexão|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
