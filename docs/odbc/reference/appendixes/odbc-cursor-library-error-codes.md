---
description: Códigos de erro da Biblioteca de cursores do ODBC
title: Códigos de erro da biblioteca de cursores ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 414de02eb7145006af4faa543735888082a3d6ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466131"
---
# <a name="odbc-cursor-library-error-codes"></a>Códigos de erro da Biblioteca de cursores do ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do componente de acesso a dados da Microsoft. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. Em vez disso, use cursores de driver e servidor.  
  
 A biblioteca de cursores ODBC retorna os seguintes sqlstates além daqueles listados na [referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  A biblioteca de cursores não ordena os registros de status; o Gerenciador de driver e ODBC 3. os drivers *x* são responsáveis pela ordenação de registros de status.  
  
|SQLSTATE|Descrição|Pode ser retornado de|  
|--------------|-----------------|--------------------------|  
|01000|O cursor não é atualizável.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|Biblioteca de cursores não usada. Falha no carregamento.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Biblioteca de cursores não usada. Suporte a driver insuficiente.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Biblioteca de cursores não usada. Incompatibilidade de versão com o Gerenciador de driver.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|O driver retornou SQL_SUCCESS_WITH_INFO. A mensagem de aviso foi perdida.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|Erro geral: não é possível criar o buffer de arquivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: não é possível ler o buffer do arquivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: não é possível gravar no buffer do arquivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: não é possível fechar ou remover o buffer de arquivo.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|A solicitação posicionada não pode ser executada porque nenhuma coluna pesquisável foi associada.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|A solicitação posicionada não pôde ser realizada porque o conjunto de resultados foi criado por uma condição de junção.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|O buffer associado excede o tamanho máximo do segmento.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|O conjunto de resultados não foi gerado por uma instrução **Select** .|**SQLGetData**|  
|SL005|A instrução **Select** contém uma cláusula Group by.|**SQLGetData**|  
|SL006|Não há suporte para matrizes de parâmetros com solicitações posicionadas.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** não é permitido em um cursor de somente avanço (sem buffer).|**SQLGetData**|  
|SL009|Nenhuma coluna foi associada antes de chamar **SQLFetch** ou **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** retornou SQL_ERROR durante uma tentativa de associar a um buffer interno.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|A opção de instrução é válida somente após chamar **SQLFetch** ou **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012|As associações de instrução não podem ser alteradas enquanto um cursor estiver aberto.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|Uma solicitação posicionada foi emitida e nem todos os campos de contagem de coluna foram armazenados em buffer.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** e **SQLFetchScroll** não podem ser misturados.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
