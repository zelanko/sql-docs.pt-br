---
title: Erros aritméticos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0d957d6091dc5fa29ee8a0b707c0e7fe7dfc7c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696294"
---
# <a name="arithmetic-errors"></a>Erros aritméticos
O driver ODBC avalia a cláusula WHERE em uma instrução SELECT, conforme ele busca cada linha. Se uma linha contiver um valor que causa um erro aritmético, como estouro de divisão por zero ou numérico, o driver retorna todas as linhas, mas retorna erros para colunas com erros de aritmética. Ao inserir ou atualizar, no entanto, o driver ODBC para de inserção ou atualização de dados quando o primeiro erro aritmético é encontrado.
