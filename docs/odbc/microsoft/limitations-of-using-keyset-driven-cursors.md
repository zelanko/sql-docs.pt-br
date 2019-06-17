---
title: Limitações do uso de cursores controlados por | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c4910ebd2c6dd988e937f1e9d6a3281bb0e9741
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192327"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitações de uso de cursores controlados por conjunto de chaves
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você deve ser capaz de recuperar uma única coluna ROWID para a tabela consultada. Um cursor controlado por conjunto de chaves não pode ser usado em junções, consultas ou instruções que contêm DISTINCT, GROUP BY, UNION, INTERSECT ou menos cláusulas.  
  
 Além disso, se seu aplicativo usa aliases de tabela, os cursores controlados por conjunto de chaves não funcionará; tipos de cursor somente de avanço ou estáticos são necessários. O conjunto de chaves usando o tipo de cursor com aliases de tabela fará com que o seguinte erro: "[Microsoft] [driver ODBC para Oracle] não é possível usar um cursor controlado por junção, com union, intersect ou conjunto de resultados de menos ou em somente leitura."  
  
> [!NOTE]  
>  Por causa da maneira que o driver lida com a instrução SQL que é enviada para o servidor Oracle, Oracle internamente retorna a seguinte mensagem de erro: "ORA-00964: tabela de nome não na lista."
