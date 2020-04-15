---
title: Excluindo linhas no conjunto de linhas com SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 940bcc3e2ee6a042394797d6038028cce64862f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305947"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Excluir linhas no conjunto de linhas com SQLSetPos
A operação de exclusão de **SQLSetPos** faz com que a fonte de dados exclua uma ou mais linhas selecionadas de uma tabela. Para excluir linhas com **SQLSetPos,** o aplicativo chama **SQLSetPos** com *Operation* definido como SQL_DELETE e *RowNumber* definido como o número da linha a ser excluída. Se *O Número de* linhas for 0, todas as linhas do conjunto de linhas serão excluídas.  
  
 Após o retorno **de SQLSetPos,** a linha excluída é a linha atual e seu status é SQL_ROW_DELETED. A linha não pode ser usada em nenhuma operação posicionada adicionalmente, como chamadas para **SQLGetData** ou **SQLSetPos**.  
  
 Ao excluir todas as linhas do conjunto de linhas *(O Número* de linhas é igual a 0), o aplicativo pode impedir que o driver exclua certas linhas usando o array de operação de linha, da mesma forma que para a operação de atualização do **SQLSetPos**. (Consulte [linhas de atualização no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 Todas as linhas excluídas devem existir no conjunto de resultados. Se os buffers de aplicativo foram preenchidos por busca e se uma matriz de status de linha foi mantida, seus valores em cada uma dessas posições de linha não devem ser SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW.
