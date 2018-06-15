---
title: Erros de aritmética | Microsoft Docs
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
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 867de0b8982b22f9f9574c334226bccc01798065
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32899491"
---
# <a name="arithmetic-errors"></a>Erros de aritmética
O driver ODBC avalia a cláusula WHERE em uma instrução SELECT como ele busca cada linha. Se uma linha contiver um valor que causa um erro aritmético, como o estouro de divisão por zero ou numérico, o driver retorna todas as linhas, mas retorna erros para colunas com erros de aritmética. Ao inserir ou atualizar, no entanto, o driver ODBC para inserir ou atualizar dados quando o primeiro erro aritmético é encontrado.
