---
description: Calling SQLCloseCursor
title: Chamando SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 925617d79266f0b50ef9b38586b31af91311b63e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494766"
---
# <a name="calling-sqlclosecursor"></a>Calling SQLCloseCursor
Como **SQLCloseCursor** é quase o mesmo que **SQLFreeStmt** com SQL_CLOSE, o Gerenciador de driver não mapeia essa função. As funções de substituição são mapeadas para que os aplicativos ODBC *2. x* existentes possam mover facilmente para o ODBC *3. x* usando as novas funções. Essa movimentação torna mais fácil para esses aplicativos começar a usar a nova funcionalidade ODBC *3. x* dentro do código condicional de maneira modular. **SQLCloseCursor** não representa nenhuma nova funcionalidade. Um aplicativo não tem nenhuma vantagem ao migrar para **SQLCloseCursor** do **SQLFreeStmt** com SQL_CLOSE.
