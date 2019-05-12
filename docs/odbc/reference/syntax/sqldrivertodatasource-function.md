---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 844e11e72bb46b69229a9a4747ac7e64f013f14e
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537168"
---
# <a name="sqldrivertodatasource-function"></a>Função SQLDriverToDataSource
**SQLDriverToDataSource** oferece suporte a conversões para drivers ODBC. Essa função não é chamada por aplicativos ODBC habilitado; os aplicativos solicitam tradução por meio **SQLSetConnectAttr**. O driver associado a *ConnectionHandle* especificado na **SQLSetConnectAttr** chama a DLL especificada para executar conversões de todos os dados que fluem do driver para a fonte de dados. Uma DLL de conversão padrão pode ser especificado no arquivo de inicialização ODBC.  
  
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
 [Entrada] Valor da opção.  
  
 *fSqlType*  
 [Entrada] O tipo de dados SQL ODBC. Esse argumento informa o driver como converter *rgbValueIn* em um formato aceitável pela fonte de dados. Para obter uma lista dos tipos de dados SQL válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md).  
  
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
 O driver chama **SQLDriverToDataSource** para converter todos os dados (instruções SQL, parâmetros e assim por diante) passando do driver para a fonte de dados. A DLL de conversão pode não traduzir alguns dados, dependendo do tipo de dados e a finalidade da conversão do DLL. Por exemplo, uma DLL que converte dados de caractere de uma página de código para outro ignora todos os dados numéricos e binários.  
  
 O valor de *fOption* é definido como o valor de *vParam* especificada chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION. É um valor de 32 bits que tem um significado específico para um determinado DLL de conversão. Por exemplo, ele poderia especificar a que tradução do conjunto de um determinado caractere.  
  
 Se o mesmo buffer é especificado para *rgbValueIn* e *rgbValueOut*, a conversão de dados no buffer será executada em vigor.  
  
 Embora *cbValueIn*, *cbValueOutMax*, e *pcbValueOut* são do tipo SDWORD, **SQLDriverToDataSource** não necessariamente suporte a ponteiros enormes.  
  
 Se **SQLDriverToDataSource** retorna FALSE, o truncamento de dados pode ter ocorrido durante a tradução. Se *pcbValueOut* (o número de bytes disponíveis para retornar no buffer de saída) é maior que *cbValueOutMax* (o comprimento do buffer de saída), em seguida, o truncamento ocorreu. O driver deve determinar se o truncamento era aceitável. Se o truncamento não tivesse ocorrido, o **SQLDriverToDataSource** retornou FALSE devido a outro erro. Em ambos os casos, uma mensagem de erro específico é retornada no *szErrorMsg*.  
  
 Para obter mais informações sobre conversão de dados, consulte [DLLs de conversão](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Conversão de dados retornados da fonte de dados|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|Retornando a configuração de um atributo de conexão|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definir um atributo de conexão|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
