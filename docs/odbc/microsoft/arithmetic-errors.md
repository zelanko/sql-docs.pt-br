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
ms.openlocfilehash: 2e0880e1746b4b65070fb28bf8d83aadec301aa4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138176"
---
# <a name="arithmetic-errors"></a>Erros aritméticos
O driver ODBC avalia a cláusula WHERE em uma instrução SELECT à medida que ela busca cada linha. Se uma linha contiver um valor que causa um erro aritmético, como divisão por zero ou estouro numérico, o driver retornará todas as linhas, mas retornará erros para colunas com erros aritméticos. No entanto, ao inserir ou atualizar, o driver ODBC interrompe a inserção ou a atualização de dados quando o primeiro erro aritmético é encontrado.
