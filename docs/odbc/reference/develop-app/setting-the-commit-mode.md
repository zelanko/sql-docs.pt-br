---
description: Configurar o modo de confirmação
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a71d6f97f4683f9177c940be7d6ca1cc4a27c01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494620"
---
# <a name="setting-the-commit-mode"></a>Configurar o modo de confirmação
Aplicativos especifique o modo de transação com o atributo de conexão SQL_ATTR_AUTOCOMMIT. Por padrão, as transações ODBC estão no modo de confirmação automática (a menos que **SQLSetConnectAttr** e **SQLSetConnectOption** não tenham suporte, o que é improvável). Alternar do modo de confirmação manual para o modo de confirmação automática confirma automaticamente qualquer transação aberta na conexão.
