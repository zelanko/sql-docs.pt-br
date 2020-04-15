---
title: Códigos de erro da biblioteca do Cursor ODBC | Microsoft Docs
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
ms.openlocfilehash: c263ce53c41546e63dc2a830d3db3b903e2e3515
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301427"
---
# <a name="odbc-cursor-library-error-codes"></a>Códigos de erro da Biblioteca de cursores do ODBC
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Microsoft Data Access Component. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. Em vez disso, use cursores de driver e servidor.  
  
 A biblioteca do cursor ODBC retorna os seguintes SQLSTATEs, além daqueles listados na [Referência a API do ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  A biblioteca do cursor não encomenda registros de status; o Driver Manager e o ODBC 3. *x* drivers são responsáveis por encomendar registros de status.  
  
|SQLSTATE|Descrição|Pode ser devolvido de|  
|--------------|-----------------|--------------------------|  
|01000|Cursor não é updatable.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|Biblioteca cursor não usada. A carga falhou.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Biblioteca cursor não usada. Suporte de motorista insuficiente.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Biblioteca cursor não usada. Incompatibilidade de versão com driver manager.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|O motorista voltou SQL_SUCCESS_WITH_INFO. A mensagem de aviso foi perdida.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|Erro geral: Não é possível criar buffer de arquivos.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: Não é possível ler a partir do buffer de arquivos.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: Não é possível gravar para buffer de arquivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Erro geral: Não é possível fechar ou remover o buffer de arquivo.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|A solicitação posicionada não pode ser realizada porque nenhuma coluna pesquisável foi vinculada.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|A solicitação posicionada não pôde ser realizada porque o conjunto de resultados foi criado por uma condição de adesão.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|O buffer bound excede o tamanho máximo do segmento.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|O conjunto de resultados não foi gerado por uma declaração **SELECT.**|**SQLGetData**|  
|SL005|**A** declaração SELECT contém uma cláusula GROUP BY.|**SQLGetData**|  
|SL006|As matrizes de parâmetros não são suportadas com solicitações posicionadas.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** não é permitido em um cursor somente para frente (não tamponado).|**SQLGetData**|  
|SL009|Nenhuma coluna foi vinculada antes de chamar **SQLFetch** ou **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** retornou SQL_ERROR durante uma tentativa de vincular a um buffer interno.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|A opção de declaração só é válida depois de ligar para **SQLFetch** ou **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012|As vinculações da declaração não podem ser alteradas enquanto um cursor estiver aberto.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|Uma solicitação posicionada foi emitida e nem todos os campos de contagem de colunas foram tamponados.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** e **SQLFetchScroll** não podem ser misturados.|**Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
