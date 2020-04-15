---
title: Excluindo linhas por marcador com SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b6a4c1b24ee276c86175392eb45ac5ce0aa45e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305957"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>Excluir linhas por indicador com SQLBulkOperations
Ao excluir uma linha por marcador, **o SQLBulkOperations** faz com que a fonte de dados exclua uma ou mais linhas selecionadas da tabela. As linhas são identificadas pelo marcador em uma coluna de marcadores vinculada.  
  
 Para excluir linhas por marcador com **SQLBulkOperations,** o aplicativo faz o seguinte:  
  
1.  Recupera e armazena os marcadores de todas as linhas a serem excluídas. Se houver mais de um marcador e a vinculação em termos de coluna for usada, os marcadores serão armazenados em uma matriz; se houver mais de um marcador e a vinculação em termos de linha for usada, os marcadores são armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE ao número de marcadores e vincula o buffer contendo o valor do marcador, ou a matriz de marcadores, à coluna 0.  
  
3.  Chama **SQLBulkOperations** com *operação* definida para SQL_DELETE_BY_BOOKMARK.
