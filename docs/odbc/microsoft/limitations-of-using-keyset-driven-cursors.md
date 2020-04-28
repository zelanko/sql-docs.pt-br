---
title: Limitações de uso de cursores controlados por conjunto de chaves | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284146"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitações de uso de cursores controlados por conjunto de chaves
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você deve ser capaz de recuperar uma única coluna de ROWID para a tabela consultada. Um cursor controlado por conjunto de chaves não pode ser usado em junções, consultas ou instruções que contêm cláusulas distintas, agrupar por, União, interseção ou subtração.  
  
 Além disso, se seu aplicativo usar aliases de tabela, os cursores controlados por conjunto de chaves não funcionarão; os tipos de cursor somente encaminhamento ou estáticos são necessários. Usar o tipo de cursor do conjunto de chaves com aliases de tabela causará o seguinte erro: "[Microsoft] [ODBC driver for Oracle] não é possível usar o cursor controlado por conjunto de chaves na junção, com Union, Intersect ou subtração ou on Read Only Result set."  
  
> [!NOTE]  
>  Devido à maneira como o driver manipula a instrução SQL que é enviada para o servidor Oracle, a Oracle retorna internamente a seguinte mensagem de erro: "ORA-00964: o nome da tabela não está na lista".
