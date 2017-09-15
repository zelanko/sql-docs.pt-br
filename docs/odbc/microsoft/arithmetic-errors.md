---
title: "Erros de aritmética | Microsoft Docs"
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
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d3585f6e1be7a3f9451231004979321202d7852
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="arithmetic-errors"></a>Erros de aritmética
O driver ODBC avalia a cláusula WHERE em uma instrução SELECT como ele busca cada linha. Se uma linha contiver um valor que causa um erro aritmético, como o estouro de divisão por zero ou numérico, o driver retorna todas as linhas, mas retorna erros para colunas com erros de aritmética. Ao inserir ou atualizar, no entanto, o driver ODBC para inserir ou atualizar dados quando o primeiro erro aritmético é encontrado.
