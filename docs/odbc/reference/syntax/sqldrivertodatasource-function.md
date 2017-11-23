---
title: "Função SQLDriverToDataSource | Microsoft Docs"
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
apiname: SQLDriverToDataSource
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDriverToDataSource
helpviewer_keywords: SQLDriverToDataSource function [ODBC]
ms.assetid: 0de28eb5-8aa9-43e4-a87f-7dbcafe800dc
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0fcb5ecd444385b44ecc82d1952cbde88b55e594
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqldrivertodatasource-function"></a>Função SQLDriverToDataSource
**SQLDriverToDataSource** oferece suporte a conversões para drivers ODBC. Essa função não é chamada por aplicativos habilitados para ODBC. os aplicativos solicitam tradução por meio de **SQLSetConnectAttr**. O driver associado a *identificador da conexão* especificado em **SQLSetConnectAttr** chama o DLL especificado para realizar conversões de todos os dados que fluem do driver para a fonte de dados. Uma DLL de conversão padrão pode ser especificado no arquivo de inicialização de ODBC.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Valor da opção.  
  
 *fSqlType*  
 [Entrada] O tipo de dados SQL ODBC. Esse argumento instrui o driver como converter *rgbValueIn* em um formato aceitável pela fonte de dados. Para obter uma lista de tipos de dados SQL válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md).  
  
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
 O driver chama **SQLDriverToDataSource** para converter todos os dados (instruções SQL, parâmetros e assim por diante) passando do driver para a fonte de dados. A DLL de conversão não pode converter alguns dados, dependendo do tipo de dados e a finalidade da conversão do DLL. Por exemplo, uma DLL que converte dados de caractere de uma página de código para outro ignora todos os dados numéricos e binários.  
  
 O valor de *fOption* é definido como o valor de *vParam* especificado chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION. É um valor de 32 bits que tem um significado específico para um determinado DLL de conversão. Por exemplo, ele pode especificar que um determinado conjunto de caracteres tradução.  
  
 Se o mesmo buffer for especificado para *rgbValueIn* e *rgbValueOut*, a conversão de dados no buffer será executada in-loco.  
  
 Embora *cbValueIn*, *cbValueOutMax*, e *pcbValueOut* são do tipo SDWORD, **SQLDriverToDataSource** não necessariamente suporte a ponteiros enormes.  
  
 Se **SQLDriverToDataSource** retorna FALSE, o truncamento de dados pode ter ocorrido durante a conversão. Se *pcbValueOut* (o número de bytes disponíveis para retornar no buffer de saída) é maior do que *cbValueOutMax* (o comprimento do buffer de saída), em seguida, o truncamento. O driver deve determinar se o truncamento aceitável. Se o truncamento não ocorreu, o **SQLDriverToDataSource** retornou FALSE devido a outro erro. Em ambos os casos, uma mensagem de erro específico é retornada no *szErrorMsg*.  
  
 Para obter mais informações sobre conversão de dados, consulte [DLLs de conversão](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Convertendo dados retornados da fonte de dados|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|Retornando a configuração de um atributo de conexão|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definir um atributo de conexão|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
