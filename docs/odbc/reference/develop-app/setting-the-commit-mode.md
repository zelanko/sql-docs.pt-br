---
title: Definindo o modo de confirmação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efc999a3644a9146e7195f0bbbb07d130172d30d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445928"
---
# <a name="setting-the-commit-mode"></a>Configurar o modo de confirmação
Aplicativos de especificam o modo de transação com o atributo de conexão SQL_ATTR_AUTOCOMMIT. Por padrão, as transações de ODBC estão no modo de confirmação automática (a menos que **SQLSetConnectAttr** e **SQLSetConnectOption** não são suportados, que é improvável). Alternar do modo de confirmação manual para o modo de confirmação automática automaticamente confirma a qualquer transação aberta sobre a conexão.
