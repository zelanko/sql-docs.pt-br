---
title: Novos Recursos | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302394"
---
# <a name="new-features"></a>Novos recursos
A nova funcionalidade a seguir foi introduzida no ODBC *3.x*. Um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* não poderá usar essa funcionalidade. O Gerenciador de Driver ODBC *3.x* não mapeia esses recursos ao trabalhar com um driver ODBC *2.x.*  
  
-   Funções que tomam uma alça de descritor como argumento: **SQLSetDescField,** **SQLGetDescField,** **SQLSetDescRec,** **SQLGetDescRec**e **SQLCopyDesc**.  
  
-   As funções **SQLSetEnvAttr** e **SQLGetEnvAttr**.  
  
-   O uso de **SQLAllocHandle** para alocar uma alça descritor. (O uso do **SQLAllocHandle** para alocar o ambiente, a conexão e as alças de declaração é duplicado, não novo, funcionalidade.)  
  
-   O uso do **SQLGetConnectAttr** para obter os atributos de conexão SQL_ATTR_AUTO_IPD. (O uso do **SQLSetConnectAttr** para definir e **sqlGetConnectAttr** para obter, outros atributos de conexão é duplicado, não novo, funcionalidade.)  
  
-   O uso de **SQLSetStmtAttr** para definir e **SQLGetStmtAttr** para obter, os atributos de declaração a seguir. (O uso de **SQLSetStmtAttr** para definir e **SQLGetStmtAttr** para obter, outros atributos de declaração são duplicados, não novos, funcionalidade.)  
  
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
  
-   O uso de **SQLGetStmtAttr** para obter os seguintes atributos de declaração. (O uso do **SQLGetStmtAttr** para obter outros atributos de declaração é funcionalidade duplicada, não nova funcionalidade.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Utilização do tipo de dados do intervalo C, dos tipos de dados SQL intervalados, dos tipos de dados BIGINT C e da estrutura de dados SQL_C_NUMERIC.  
  
-   Vinculação em termos de linha de parâmetros.  
  
-   Os pontos de marcação baseados em deslocamento, como chamar **SQLFetchScroll** com um argumento *FetchOrientation* de SQL_FETCH_BOOKMARK e especificar um deslocamento diferente de 0.  
  
-   **SQLFetch** retornando a matriz de status de linha, número de linhas buscadas, buscando várias linhas, intermisturando chamadas com **SQLFetchScroll**e intermisturando chamadas com **SQLBulkOperations** ou **SQLSetPos**. Para obter mais informações, consulte a próxima seção, [Cursors de bloco, cursores roláveis e compatibilidade retrógrada para aplicativos ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
-   Parâmetros nomeados.  
  
-   Qualquer uma das opções **SQLGetInfo** específicas do ODBC *3.x.* (Se um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* chamar os tipos de informações SQL_XXX_CURSOR_ATTRIBUTES1, que substituíram vários tipos de informações ODBC *2.x,* algumas das informações podem ser confiáveis, mas algumas podem não ser confiáveis. Para obter mais informações, consulte [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   Vincular deslocamentos.  
  
-   Atualizando, atualizando e excluindo por marcadores (através de uma chamada para **SQLBulkOperations**).  
  
-   Chamando **SQLBulkOperations** ou **SQLSetPos** no estado S5.  
  
-   Os campos ROW_NUMBER e COLUMN_NUMBER no registro de diagnóstico (que devem ser recuperados pelas funções de substituição **SQLGetDiagField** ou **SQLGetDiagRec**).  
  
-   A linha aproximada conta.  
  
-   Informações de aviso (SQL_ROW_SUCCESS_WITH_INFO do **SQLFetchScroll**).  
  
-   Marcadores de comprimento variável.  
  
-   Informações de erro estendidas para matrizes de parâmetros.  
  
-   Todas as novas colunas nos conjuntos de resultados retornadas pelas funções do catálogo.  
  
-   Uso de **SQLDescribeCol** e **SQLColAttribute** na coluna 0.  
  
-   Uso de quaisquer atributos de coluna específicos do ODBC *3.x*em uma chamada para **SQLColAttribute**.  
  
-   Uso de múltiplas alças de ambiente.  
  
 Esta seção contém o seguinte tópico.  
  
-   [Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para aplicativos 3.x ODBC](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
