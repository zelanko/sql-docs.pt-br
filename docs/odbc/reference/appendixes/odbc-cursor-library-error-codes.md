---
title: "Códigos de erro de biblioteca de Cursor ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 308ad8ed54aacb9ab7bc169efd9dad020e2f2b66
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-cursor-library-error-codes"></a>Códigos de erro de biblioteca de Cursor ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Microsoft Data Access Component. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use cursores de driver e servidor.  
  
 A biblioteca de cursores ODBC retorna os seguintes SQLSTATEs além daqueles listados em [referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  A biblioteca de cursores não solicitar registros de status. o Gerenciador de Driver e o ODBC 3. *x* drivers serão responsáveis por ordenar registros de status.  
  
|SQLSTATE|Description|Pode ser retornado de|  
|--------------|-----------------|--------------------------|  
|01000|Cursor não é atualizável.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|Biblioteca de cursores não usada. Falha ao carregar.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Biblioteca de cursores não usada. Suporte a driver insuficiente.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Biblioteca de cursores não usada. Incompatibilidade de versão com o Gerenciador de Driver.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Driver retornou SQL_SUCCESS_WITH_INFO. A mensagem de aviso foi perdida.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|Erro geral: não é possível criar buffer de arquivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: não é possível ler o buffer do arquivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: não é possível gravar no buffer de arquivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: não é possível fechar ou remover o buffer de arquivo.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|Solicitação posicionada não pode ser executada porque nenhuma coluna pesquisável foi vinculada.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|Solicitação posicionada não pôde ser executada porque o conjunto de resultados foi criado por uma condição de junção.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|Buffer vinculado excede o tamanho máximo de segmento.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|Conjunto de resultados não foi gerado por um **selecione** instrução.|**SQLGetData**|  
|SL005|**Selecione** instrução contém uma cláusula GROUP BY.|**SQLGetData**|  
|SL006|Não há suporte para matrizes de parâmetros com solicitações posicionadas.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** não é permitido em um cursor somente de avanço de (sem buffer).|**SQLGetData**|  
|SL009|Não há colunas foram associadas antes de chamar **SQLFetch** ou **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** retornado SQL_ERROR durante uma tentativa de associar a um buffer interno.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|Opção de instrução é válida somente depois de chamar **SQLFetch** ou **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012|Associações de instrução não podem ser alteradas enquanto um cursor é aberto.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|Uma solicitação posicionada foi enviada e nem todos os campos de contagem de coluna foram armazenados em buffer.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** e **SQLFetchScroll** não podem ser misturados.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|

