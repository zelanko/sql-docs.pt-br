---
title: Novos recursos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77620585dffabc97a9e85455236bf51b575d0d3a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="new-features"></a>Novos recursos
A nova funcionalidade a seguir foi introduzida em ODBC 3. *x*. ODBC 3. *x* aplicativo trabalhando com um ODBC 2 *. x* driver não poderão usar essa funcionalidade. O ODBC 3. *x* Gerenciador de Driver não mapear esses recursos quando estiver trabalhando com um ODBC 2 *. x* driver.  
  
-   Funções que usam um descritor de tratar como um argumento: **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**, e **SQLCopyDesc**.  
  
-   As funções **SQLSetEnvAttr** e **SQLGetEnvAttr**.  
  
-   O uso de **SQLAllocHandle** para alocar um identificador do descritor. (O uso de **SQLAllocHandle** alocar identificadores de ambiente, conexão e instrução é duplicada, não nova funcionalidade.)  
  
-   O uso de **SQLGetConnectAttr** para obter os atributos de conexão SQL_ATTR_AUTO_IPD. (O uso de **SQLSetConnectAttr** para definir e **SQLGetConnectAttr** para obter, outros atributos de conexão é duplicada, não nova funcionalidade.)  
  
-   O uso de **SQLSetStmtAttr** para definir e **SQLGetStmtAttr** para obter os seguintes atributos de instrução. (O uso de **SQLSetStmtAttr** para definir e **SQLGetStmtAttr** para obter, outros atributos de instrução é duplicada, não nova funcionalidade.)  
  
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
  
-   O uso de **SQLGetStmtAttr** para obter os seguintes atributos de instrução. (O uso de **SQLGetStmtAttr** obter outra instrução de atributos é funções duplicadas, não novas funcionalidades.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Uso de tipo de dados de intervalo C, os tipos de dados SQL do intervalo, os tipos de dados BIGINT C e a estrutura de dados SQL_C_NUMERIC.  
  
-   A associação de parâmetros.  
  
-   Indicador com base no deslocamento de busca, como chamar **SQLFetchScroll** com um *FetchOrientation* argumento de SQL_FETCH_BOOKMARK e especificando um deslocamento diferente de 0.  
  
-   **SQLFetch** retornar a matriz de status de linha, o número de linhas buscadas, buscar várias linhas, chamadas entremear com **SQLFetchScroll**e chama entremear com **SQLBulkOperations** ou **SQLSetPos**. Para obter mais informações, consulte a próxima seção, [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para os aplicativos ODBC 3. x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
-   Parâmetros nomeados.  
  
-   Nenhum do ODBC 3. *x*– específico **SQLGetInfo** opções. (Se for um ODBC 3. *x* aplicativo trabalhando com um ODBC 2. *x* driver chama os tipos de informações SQL_XXX_CURSOR_ATTRIBUTES1 que substituíram várias ODBC 2. *x* tipos de informação, algumas das informações podem ser confiáveis, mas alguns não podem ser confiáveis. Para obter mais informações, consulte [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   Deslocamentos de ligação.  
  
-   A atualização, atualizando e excluindo por indicadores (por meio de uma chamada para **SQLBulkOperations**).  
  
-   Chamando **SQLBulkOperations** ou **SQLSetPos** no estado S5.  
  
-   Os campos ROW_NUMBER e Núm_col no registro de diagnóstico (que precisam ser recuperados pelas funções de substituição **SQLGetDiagField** ou **SQLGetDiagRec**).  
  
-   Contagens de linhas aproximada.  
  
-   Informações de aviso (SQL_ROW_SUCCESS_WITH_INFO de **SQLFetchScroll**).  
  
-   Indicadores de comprimento variável.  
  
-   Informações de erro estendidas para matrizes de parâmetros.  
  
-   Todas as colunas novas em conjuntos de resultados retornados pelas funções de catálogo.  
  
-   O uso de **SQLDescribeCol** e **SQLColAttribute** na coluna 0.  
  
-   Uso de qualquer ODBC 3. *x*– atributos de coluna específica em uma chamada para **SQLColAttribute**.  
  
-   Uso de vários identificadores de ambiente.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para aplicativos 3.x ODBC](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
