---
title: Select Statement Limitações | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d91e93076a67287cbbd2b64b2ad0d6414a0aea6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300916"
---
# <a name="select-statement-limitations"></a>Limitações da instrução SELECT
Uma coluna de função agregada não pode ser misturada com uma coluna não agregada em uma declaração SELECT.  
  
 A lista selecionada de uma declaração SELECT que tenha uma cláusula GROUP BY só pode ter expressões da cláusula GROUP BY ou funções definidas.  
  
 Não é suportado o uso de um asterisco (para selecionar todas as colunas) em uma declaração SELECT contendo uma cláusula GROUP BY. Os nomes das colunas a serem selecionadas devem ser especificados.  
  
 O uso de uma barra vertical em uma declaração SELECT não é suportado. Use um parâmetro na declaração SELECT se você precisar consultar um valor de dados que contenha uma barra vertical.  
  
 Ao usar um alias de coluna em uma declaração SELECT, a palavra "as" deve preceder o alias. Por exemplo, "SELECT col1 as a from b." Sem o "as", a declaração retornará um erro.  
  
 Se um nome de coluna incorreto for inserido em uma declaração SELECT, um erro do SQLSTATE 07001, "Número errado de parâmetros", será retornado em vez de um erro SQLSTATE S0022, "Coluna Não Encontrada".  
  
 Quando o driver do Microsoft Excel é usado, se uma seqüência de string vazia for inserida em uma coluna, a seqüência de string vazia será convertida em UM NULL; uma declaração SELECT pesquisada que é executada com uma seqüência de string vazia na cláusula WHERE não terá sucesso nessa coluna.
