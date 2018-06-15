---
title: Limitações de uso de cursores controlados por conjuntos de chaves | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8ae5c5fbc73ff0128eb44944d5a0e5573c5b0d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32900131"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitações de uso de cursores controlados por conjunto de chaves
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você deve ser capaz de recuperar uma única coluna ROWID da tabela consultada. Um cursor controlado por conjunto de chaves não pode ser usado em junções, consultas ou instruções que contêm DISTINCT, GROUP BY, UNION, INTERSECT ou menos cláusulas.  
  
 Além disso, se seu aplicativo usa aliases de tabela, os cursores controlados por conjunto de chaves não funciona. tipos de cursor somente de encaminhamento ou estáticos são necessários. O conjunto de chaves usando o tipo de cursor com aliases de tabela fará com que o seguinte erro: "[Microsoft] [ODBC driver for Oracle] não é possível usar um cursor orientado na junção, com union, intersect ou conjunto de resultados de subtração ou em somente leitura."  
  
> [!NOTE]  
>  Por causa da forma que o driver trata a instrução SQL que é enviada para o servidor Oracle, o Oracle internamente retorna a seguinte mensagem de erro: "ORA-00964: tabela nome não na lista."
