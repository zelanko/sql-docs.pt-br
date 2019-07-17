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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138176"
---
# <a name="arithmetic-errors"></a>Erros aritméticos
O driver ODBC avalia a cláusula WHERE em uma instrução SELECT, conforme ele busca cada linha. Se uma linha contiver um valor que causa um erro aritmético, como estouro de divisão por zero ou numérico, o driver retorna todas as linhas, mas retorna erros para colunas com erros de aritmética. Ao inserir ou atualizar, no entanto, o driver ODBC para de inserção ou atualização de dados quando o primeiro erro aritmético é encontrado.
