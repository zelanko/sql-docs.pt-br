---
title: Configuração do modo de confirmação | Microsoft Docs
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
ms.openlocfilehash: f05aaca2349a612cda7c5b6b257e7a1d5a5ea9c5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299816"
---
# <a name="setting-the-commit-mode"></a>Configurar o modo de confirmação
Os aplicativos especificam o modo de transação com o atributo de conexão SQL_ATTR_AUTOCOMMIT. Por padrão, as transações ODBC estão no modo de confirmação automática (a menos que **SQLSetConnectAttr** e **SQLSetConnectOption** não sejam suportados, o que é improvável). A mudança do modo de confirmação manual para o modo de confirmação automática compromete automaticamente qualquer transação aberta na conexão.
