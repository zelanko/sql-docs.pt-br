---
title: Códigos de erro de biblioteca de Cursor ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3fb86e1332e3b7e4d89003ccf6421151e5d9cec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100676"
---
# <a name="odbc-cursor-library-error-codes"></a>Códigos de erro da Biblioteca de cursores do ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Microsoft Data Access Component. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. Em vez disso, use cursores de servidor e de driver.  
  
 A biblioteca de cursores ODBC retorna as seguintes SQLSTATEs, além daqueles listados na [referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  A biblioteca de cursores não ordena os registros de status; o Gerenciador de Driver e o ODBC 3. *x* drivers são responsáveis por ordem de registros de status.  
  
|SQLSTATE|Descrição|Pode ser retornado de|  
|--------------|-----------------|--------------------------|  
|01000|Cursor não é atualizável.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|Biblioteca de cursores não usada. Falha ao carregar.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Biblioteca de cursores não usada. Suporte a driver insuficientes.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Biblioteca de cursores não usada. Incompatibilidade de versão com o Gerenciador de Driver.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Driver retornou SQL_SUCCESS_WITH_INFO. A mensagem de aviso foi perdida.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|Erro geral: Não é possível criar o buffer de arquivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: Não é possível ler do buffer de arquivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: Não é possível gravar no buffer de arquivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: Não é possível fechar ou remover o buffer de arquivo.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|Solicitação posicionada não pode ser executada porque não há colunas pesquisáveis eram vinculadas.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|Solicitação posicionada não pôde ser executada porque o conjunto de resultados foi criado por uma condição de junção.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|Buffer vinculado excede o tamanho máximo de segmento.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|Conjunto de resultados não foi gerado por uma **selecionar** instrução.|**SQLGetData**|  
|SL005|**Selecione** instrução contém uma cláusula GROUP BY.|**SQLGetData**|  
|SL006|Não há suporte para matrizes de parâmetro com solicitações posicionadas.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** não é permitido em um cursor somente de avanço de (sem buffer).|**SQLGetData**|  
|SL009|Não há colunas foram associadas antes de chamar **SQLFetch** ou **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** retornado SQL_ERROR durante uma tentativa de associar a um buffer interno.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|Opção de instrução é válida somente depois de chamar **SQLFetch** ou **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012|Associações de instrução não podem ser alteradas enquanto um cursor é aberto.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|Uma solicitação posicionada foi emitida e nem todos os campos de contagem de coluna foram armazenados em buffer.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** e **SQLFetchScroll** não podem ser misturados.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
