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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92df58b76a9a11d0d4ab9821756bff014ecae29a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301186"
---
# <a name="sqldatasourcetodriver-function"></a>Função SQLDataSourceToDriver
**SQLDataSourceToDriver** supportstranslations para drivers ODBC. Essa função não é chamada por aplicativos habilitados para ODBC; os aplicativos solicitam a conversão por meio de **SQLSetConnectAttr**. O driver associado ao *ConnectionHandle* especificado em **SQLSETCONNECTATTR** chama a DLL especificada para executar traduções de todos os dados que fluem da fonte de dados para o driver. Uma DLL de tradução padrão pode ser especificada no arquivo de inicialização ODBC.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
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
 Entrada Valor da opção.  
  
 *fSqlType*  
 Entrada O tipo de dados SQL. Esse argumento informa ao driver como converter *rgbValueIn* em um formato aceitável pelo aplicativo. Para obter uma lista de tipos de dados SQL válidos, consulte a seção [tipos de dados do SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice D: tipos de dados.  
  
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
 O driver chama **SQLDataSourceToDriver** para converter os rowgroup (dados do conjunto de resultados, nomes de tabelas, contagens de linhas, mensagens de erro e assim por diante) passando da fonte de dados para o driver. A DLL de tradução pode não converter alguns dados, dependendo do tipo de dados e da finalidade da DLL de tradução; por exemplo, uma DLL que traduz dados de caractere de uma página de código para outra ignora todos os dados numéricos e binários.  
  
 O valor de *fOption* é definido como o valor de *VParam* especificado chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION. É um valor de 32 bits que tem um significado específico para uma determinada DLL de tradução. Por exemplo, ele pode especificar uma determinada tradução de conjunto de caracteres.  
  
 Se o mesmo buffer for especificado para *rgbValueIn* e *rgbValueOut*, a conversão de dados no buffer será executada no local.  
  
 Embora *cbValueIn*, *cbValueOutMax*e *pcbValueOut* sejam do tipo SDWORD, **SQLDataSourceToDriver** não necessariamente oferece suporte a ponteiros enormes.  
  
 Se **SQLDataSourceToDriver** retornar false, o truncamento de dados poderá ter ocorrido durante a tradução. Se *pcbValueOut* (o número de bytes disponíveis para retornar no buffer de saída) for maior que *cbValueOutMax* (o comprimento do buffer de saída), o truncamento ocorrerá. O driver deve determinar se o truncamento foi aceitável. Se o truncamento não ocorreu, o **SQLDataSourceToDriver** retornou false devido a outro erro. Em ambos os casos, uma mensagem de erro específica é retornada em *szErrorMsg*.  
  
 Para obter mais informações sobre a tradução de dados, consulte [DLLs de tradução](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Convertendo dados enviados para a fonte de dados|[SQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|Retornando a configuração de um atributo de conexão|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definindo um atributo de conexão|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
