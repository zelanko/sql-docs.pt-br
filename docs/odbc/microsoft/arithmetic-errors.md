---
description: Erros aritméticos
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e2fa142b43f1e96693390f777c90ea6f10705f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500399"
---
# <a name="arithmetic-errors"></a>Erros aritméticos
O driver ODBC avalia a cláusula WHERE em uma instrução SELECT à medida que ela busca cada linha. Se uma linha contiver um valor que causa um erro aritmético, como divisão por zero ou estouro numérico, o driver retornará todas as linhas, mas retornará erros para colunas com erros aritméticos. No entanto, ao inserir ou atualizar, o driver ODBC interrompe a inserção ou a atualização de dados quando o primeiro erro aritmético é encontrado.
