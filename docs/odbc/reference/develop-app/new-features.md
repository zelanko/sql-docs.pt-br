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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4582a99797d5f6035f6d5d639514c5a6fdd572d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794060"
---
# <a name="new-features"></a>Novos recursos
A seguinte nova funcionalidade foi introduzida no ODBC *3.x*. ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver não poderão usar essa funcionalidade. O ODBC *3.x* Gerenciador de Driver não mapeia esses recursos ao trabalhar com ODBC *2.x* driver.  
  
-   Funções que usam um descritor de lidar com como um argumento: **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**, and **SQLCopyDesc**.  
  
-   As funções **SQLSetEnvAttr** e **SQLGetEnvAttr**.  
  
-   O uso de **SQLAllocHandle** para alocar um identificador do descritor. (O uso de **SQLAllocHandle** alocar identificadores de ambiente, conexão e instrução é uma funcionalidade duplicada, não é nova,.)  
  
-   O uso de **SQLGetConnectAttr** para obter os atributos de conexão SQL_ATTR_AUTO_IPD. (O uso de **SQLSetConnectAttr** a ser definido, e **SQLGetConnectAttr** para obter, outros atributos de conexão é uma funcionalidade duplicada, não é nova,.)  
  
-   O uso de **SQLSetStmtAttr** a ser definido, e **SQLGetStmtAttr** para obter os seguintes atributos de instrução. (O uso de **SQLSetStmtAttr** a ser definido, e **SQLGetStmtAttr** para obter, outros atributos de instrução é uma funcionalidade duplicada, não é nova,.)  
  
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
  
-   O uso de **SQLGetStmtAttr** para obter os seguintes atributos de instrução. (O uso de **SQLGetStmtAttr** obter outra instrução de atributos é uma funcionalidade duplicada, não novas funcionalidades.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Uso do tipo de dados de intervalo de C, os tipos de dados SQL de intervalo, os tipos de dados BIGINT C e a estrutura de dados SQL_C_NUMERIC.  
  
-   A associação de parâmetros.  
  
-   Indicador com base no deslocamento de busca, por exemplo, chamar **SQLFetchScroll** com um *FetchOrientation* argumento de SQL_FETCH_BOOKMARK e especificando um deslocamento diferente de 0.  
  
-   **SQLFetch** retornar a matriz de status de linha, o número de linhas buscadas, buscar várias linhas, chamadas entremear com **SQLFetchScroll**e chamadas entremear com **SQLBulkOperations** ou **SQLSetPos**. Para obter mais informações, consulte a próxima seção, [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para aplicativos 3.x ODBC](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
-   Parâmetros nomeados.  
  
-   Qualquer um dos ODBC *3.x*-específico **SQLGetInfo** opções. (Se um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver chama os tipos de informações SQL_XXX_CURSOR_ATTRIBUTES1 que substituíram vários ODBC *2.x* tipos de informação, algumas das informações podem ser confiáveis, mas alguns podem não ser confiáveis. Para obter mais informações, consulte [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   Deslocamentos de associação.  
  
-   Atualização, atualizando e excluindo por indicadores (por meio de uma chamada para **SQLBulkOperations**).  
  
-   Chamando **SQLBulkOperations** ou **SQLSetPos** no estado S5.  
  
-   Os campos ROW_NUMBER e Núm_col no registro de diagnóstico (que precisam ser recuperados pelas funções de substituição **SQLGetDiagField** ou **SQLGetDiagRec**).  
  
-   Contagens de linha aproximada.  
  
-   Informações de aviso (SQL_ROW_SUCCESS_WITH_INFO partir **SQLFetchScroll**).  
  
-   Indicadores de comprimento variável.  
  
-   Informações de erro estendidas para matrizes de parâmetros.  
  
-   Todas as colunas novas em conjuntos de resultados retornados pelas funções de catálogo.  
  
-   Uso de **SQLDescribeCol** e **SQLColAttribute** na coluna 0.  
  
-   Uso de qualquer ODBC *3.x*-atributos de coluna específica em uma chamada para **SQLColAttribute**.  
  
-   Uso de vários identificadores de ambiente.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para aplicativos 3.x ODBC](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
