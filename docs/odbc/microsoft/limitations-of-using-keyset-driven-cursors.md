---
title: "Limitações de uso de cursores controlados por conjuntos de chaves | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 54581e6bf4aceebc50a752ee460458671e8047bd
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitações de uso de cursores controlados por conjunto de chaves
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você deve ser capaz de recuperar uma única coluna ROWID da tabela consultada. Um cursor controlado por conjunto de chaves não pode ser usado em junções, consultas ou instruções que contêm DISTINCT, GROUP BY, UNION, INTERSECT ou menos cláusulas.  
  
 Além disso, se seu aplicativo usa aliases de tabela, os cursores controlados por conjunto de chaves não funciona. tipos de cursor somente de encaminhamento ou estáticos são necessários. O conjunto de chaves usando o tipo de cursor com aliases de tabela fará com que o seguinte erro: "[Microsoft] [ODBC driver for Oracle] não é possível usar um cursor orientado na junção, com union, intersect ou conjunto de resultados de subtração ou em somente leitura."  
  
> [!NOTE]  
>  Por causa da forma que o driver trata a instrução SQL que é enviada para o servidor Oracle, o Oracle internamente retorna a seguinte mensagem de erro: "ORA-00964: tabela nome não na lista."

