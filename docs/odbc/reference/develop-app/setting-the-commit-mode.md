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
ms.openlocfilehash: a43a78ad9453f65d9b12595851bd622f720b409a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094220"
---
# <a name="setting-the-commit-mode"></a>Configurar o modo de confirmação
Aplicativos de especificam o modo de transação com o atributo de conexão SQL_ATTR_AUTOCOMMIT. Por padrão, as transações de ODBC estão no modo de confirmação automática (a menos que **SQLSetConnectAttr** e **SQLSetConnectOption** não são suportados, que é improvável). Alternar do modo de confirmação manual para o modo de confirmação automática automaticamente confirma a qualquer transação aberta sobre a conexão.
