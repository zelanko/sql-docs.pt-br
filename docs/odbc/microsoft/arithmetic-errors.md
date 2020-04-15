---
title: Erros de Aritmética | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab1b472540d1978a6e7a06d94da7542cc641e999
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299896"
---
# <a name="arithmetic-errors"></a>Erros aritméticos
O driver ODBC avalia a cláusula WHERE em uma declaração SELECT à medida que busca cada linha. Se uma linha contiver um valor que cause um erro aritmético, como estouro de divisão por zero ou numérico, o driver retorna todas as linhas, mas retorna erros para colunas com erros aritméticos. Ao inserir ou atualizar, no entanto, o driver ODBC pára de inserir ou atualizar dados quando o primeiro erro aritmético é encontrado.
