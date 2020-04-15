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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89e7db7e4b20a35e047dca94cb72d8a6888fb670
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302747"
---
# <a name="sqldrivertodatasource-function"></a>Função SQLDriverToDataSource
**SQLDriverToDataSource** suporta traduções para drivers ODBC. Esta função não é chamada por aplicativos habilitados para ODBC; os aplicativos solicitam tradução através **do SQLSetConnectAttr**. O driver associado ao *ConnectionHandle* especificado no **SQLSetConnectAttr** chama a DLL especificada para executar traduções de todos os dados que fluem do driver para a fonte de dados. Um DLL de tradução padrão pode ser especificado no arquivo de inicialização ODBC.  
  
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
 *fOpção*  
 [Entrada] Valor da opção.  
  
 *fSqlType*  
 [Entrada] O tipo de dados ODBC SQL. Este argumento diz ao driver como converter *rgbValueIn* em um formulário aceitável pela fonte de dados. Para obter uma lista de tipos de dados SQL válidos, consulte Tipos de [dados SQL](../../../odbc/reference/appendixes/sql-data-types.md).  
  
 *rgbValueIn*  
 [Entrada] Valor para traduzir.  
  
 *cbValueIn*  
 [Entrada] Comprimento de *rgbValueIn*.  
  
 *rgbValueOut*  
 [Saída] Resultado da tradução.  
  
> [!NOTE]  
>  A dLL de tradução não termina nulamente este valor.  
  
 *cbValueOutMax*  
 [Entrada] Comprimento do *rgbValueOut*.  
  
 *pcbValueOut*  
 [Saída] O número total de bytes (excluindo o byte de rescisão nula) disponível para retornar em *rgbValueOut*.  
  
 Para dados de caracteres ou binários, se isso for maior ou igual a *cbValueOutMax,* os dados em *rgbValueOut* são truncados para *bytes cbValueOutMax.*  
  
 Para todos os outros tipos de dados, o valor do *cbValueOutMax* é ignorado e a DLL de tradução assume que o tamanho do *rgbValueOut* é o tamanho do tipo de dados C padrão do tipo de dados SQL especificado com *fSqlType*.  
  
 O *argumento pcbValueOut* pode ser um ponteiro nulo.  
  
 *szErrorMsg*  
 [Saída] Ponteiro para armazenamento para uma mensagem de erro. Esta é uma seqüência vazia, a menos que a tradução falhou.  
  
 *cbErrorMsgMax*  
 [Entrada] Comprimento de *szErrorMsg*.  
  
 *pcbErrorMsg*  
 [Saída] Ponteiro para o número total de bytes (excluindo o byte de rescisão nula) disponível para retornar em *szErrorMsg*. Se isso for maior ou igual ao *cbErrorMsg,* os dados no *szErrorMsg* são truncados para *cbErrorMsgMax* menos o caractere de rescisão nula. O *argumento pcbErrorMsg* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 TRUE se a tradução foi bem sucedida, FALSE se a tradução falhou.  
  
## <a name="comments"></a>Comentários  
 O driver chama **SQLDriverToDataSource** para traduzir todos os dados (instruções SQL, parâmetros e assim por diante) passando do driver para a fonte de dados. A dLL de tradução pode não traduzir alguns dados, dependendo do tipo de dados e do propósito da dLL de tradução. Por exemplo, uma DLL que traduz dados de caracteres de uma página de código para outra ignora todos os dados numéricos e binários.  
  
 O valor de *fOption* é definido para o valor do *vParam* especificado ligando para **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_OPTION. É um valor de 32 bits que tem um significado específico para uma determinada tradução DLL. Por exemplo, ele poderia especificar uma determinada tradução de conjunto de caracteres.  
  
 Se o mesmo buffer for especificado para *rgbValueIn* e *rgbValueOut,* a tradução dos dados no buffer será realizada no local.  
  
 Embora *cbValueIn,* *cbValueOutMax*e *pcbValueOut* sejam do tipo SDWORD, **o SQLDriverToDataSource** não suporta necessariamente grandes ponteiros.  
  
 Se **SQLDriverToDataSource** retornar FALSO, a truncação de dados pode ter ocorrido durante a tradução. Se *o pcbValueOut* (o número de bytes disponíveis para retornar no buffer de saída) for maior do que *cbValueOutMax* (o comprimento do buffer de saída), então ocorreu a truncação. O motorista deve determinar se a truncação foi aceitável ou não. Se a truncação não ocorreu, o **SQLDriverToDataSource** retornou FALSO devido a outro erro. Em ambos os casos, uma mensagem de erro específica é retornada em *szErrorMsg*.  
  
 Para obter mais informações sobre a tradução de dados, consulte [DLLs de tradução](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Tradução de dados retornados da fonte de dados|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|Retornando a configuração de um atributo de conexão|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Definindo um atributo de conexão|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
