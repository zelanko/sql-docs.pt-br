---
title: Novos recursos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b40803dac6c9f296043a8dcac50f9bc69036875a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302394"
---
# <a name="new-features"></a>Novos recursos
A nova funcionalidade a seguir foi introduzida no ODBC *3. x*. Um aplicativo ODBC *3. x* trabalhando com um driver ODBC *2. x* não poderá usar essa funcionalidade. O Gerenciador de driver ODBC *3. x* não mapeia esses recursos ao trabalhar com um driver ODBC *2. x* .  
  
-   Funções que usam um identificador de descritor como um argumento: **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**e **SQLCopyDesc**.  
  
-   As funções **SQLSetEnvAttr** e **SQLGetEnvAttr**.  
  
-   O uso de **SQLAllocHandle** para alocar um identificador de descritor. (O uso de **SQLAllocHandle** para alocar identificadores de ambiente, conexão e instrução é duplicado, não novo, funcionalidade.)  
  
-   O uso de **SQLGetConnectAttr** para obter os atributos de conexão do SQL_ATTR_AUTO_IPD. (O uso de **SQLSetConnectAttr** para definir e **SQLGetConnectAttr** para Get, outros atributos de conexão são duplicados, não novos, funcionalidade.)  
  
-   O uso de **SQLSetStmtAttr** para definir e **SQLGetStmtAttr** para Get, os atributos de instrução a seguir. (O uso de **SQLSetStmtAttr** para definir e **SQLGetStmtAttr** para Get, outros atributos de instrução são duplicados, não novos, funcionalidade.)  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_ENABLE_AUTO_IPD  
  
     SQL_ATTR_FETCH_BOOKMARK_PTR  
  
     SQL_ATTR_BIND_OFFSET  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     SQL_DESC_PARAM_STATUS_PTR  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR  
  
     SQL_ATTR_PARAMSET_SIZE  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_ROW_ARRAY_SIZE  
  
-   O uso de **SQLGetStmtAttr** para obter os atributos de instrução a seguir. (O uso de **SQLGetStmtAttr** para obter outros atributos de instrução é a funcionalidade duplicada, e não a nova funcionalidade.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Uso do tipo de dados intervalo C, os tipos de dados SQL de intervalo, os tipos de dados BIGINT C e a estrutura de dados SQL_C_NUMERIC.  
  
-   Associação de parâmetros de linha.  
  
-   Buscas de indicador com base em deslocamento, como chamar **SQLFetchScroll** com um argumento *FetchOrientation* de SQL_FETCH_BOOKMARK e especificar um deslocamento diferente de 0.  
  
-   **SQLFetch** retornando a matriz de status de linha, o número de linhas buscadas, buscando várias linhas, combinando chamadas com **SQLFetchScroll**e intermisturando chamadas com **SQLBulkOperations** ou **SQLSetPos**. Para obter mais informações, consulte a próxima seção, [cursores de bloco, cursores roláveis e compatibilidade com versões anteriores para aplicativos ODBC 3. x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
-   Parâmetros nomeados.  
  
-   Qualquer uma das opções **SQLGetInfo** específicas do ODBC *3. x*. (Se um aplicativo ODBC *3. x* que trabalha com um driver ODBC *2. x* chamar os tipos de informações SQL_XXX_CURSOR_ATTRIBUTES1, que substituiram vários tipos de informações ODBC *2. x* , algumas das informações podem ser confiáveis, mas algumas podem não ser confiáveis. Para obter mais informações, consulte [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   Deslocamentos de ligação.  
  
-   Atualização, atualização e exclusão por indicadores (por meio de uma chamada para **SQLBulkOperations**).  
  
-   Chamando **SQLBulkOperations** ou **SQLSetPos** no estado s5.  
  
-   Os campos ROW_NUMBER e COLUMN_NUMBER no registro de diagnóstico (que devem ser recuperados pelas funções de substituição **SQLGetDiagField** ou **SQLGetDiagRec**).  
  
-   Contagens de linhas aproximadas.  
  
-   Informações de aviso (SQL_ROW_SUCCESS_WITH_INFO de **SQLFetchScroll**).  
  
-   Indicadores de comprimento variável.  
  
-   Informações de erro estendidas para matrizes de parâmetros.  
  
-   Todas as novas colunas nos conjuntos de resultados retornadas pelas funções de catálogo.  
  
-   Uso de **SQLDescribeCol** e **SQLColAttribute** na coluna 0.  
  
-   Uso de qualquer atributo de coluna específico do ODBC *3. x*em uma chamada para **SQLColAttribute**.  
  
-   Uso de vários identificadores de ambiente.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para aplicativos 3.x ODBC](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
