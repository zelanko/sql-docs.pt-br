---
title: Erros de aritmética | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e52d0edb1704df3e4085e417493fd68b7a7af977
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="arithmetic-errors"></a>Erros de aritmética
O driver ODBC avalia a cláusula WHERE em uma instrução SELECT como ele busca cada linha. Se uma linha contiver um valor que causa um erro aritmético, como o estouro de divisão por zero ou numérico, o driver retorna todas as linhas, mas retorna erros para colunas com erros de aritmética. Ao inserir ou atualizar, no entanto, o driver ODBC para inserir ou atualizar dados quando o primeiro erro aritmético é encontrado.
