---
title: Limitações do uso de cursors orientados por keyset | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2aeb5a0c50192118dfff8ed7d866c3911c2b4007
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284146"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitações de uso de cursores controlados por conjunto de chaves
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você deve ser capaz de recuperar uma única coluna ROWID para a tabela consultada. Um cursor orientado por chave não pode ser usado em adesões, consultas ou declarações que contenham cláusulas DISTINTAS, GROUP BY, UNION, INTERSECT ou MINUS.  
  
 Além disso, se o aplicativo usar aliases de tabela, os cursores orientados por conjuntos de chaves não funcionarão; São necessários tipos de cursor para frente ou estático. O uso do tipo de cursor de conjunto de chaves com aliases de tabela causará o seguinte erro: "[Microsoft][Driver ODBC para Oracle]Não é possível usar cursor orientado por Keyset na junta, com união, interseção ou menos ou no conjunto de resultados somente leitura."  
  
> [!NOTE]  
>  Devido à maneira como o driver lida com a declaração SQL enviada ao servidor Oracle, a Oracle retorna internamente a seguinte mensagem de erro: "ORA-00964: nome da tabela não está na lista DO".
