---
title: Chamando SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ad8a1d13091dd9413afb79b17eb701688d7f902
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="calling-sqlclosecursor"></a>Chamar SQLCloseCursor
Porque **SQLCloseCursor** é quase o mesmo que **SQLFreeStmt** com SQL_CLOSE, o Gerenciador de Driver não mapeia essa função. Funções de substituição são mapeadas para que existente ODBC 2 *. x* aplicativos podem mover facilmente para ODBC 3. *x* usando as novas funções. Essas mudanças, torna mais fácil para esses aplicativos começar a usar o novo ODBC 3. *x* funcionalidade dentro do código condicional de forma modular. **SQLCloseCursor** não representam nenhuma nova funcionalidade. Um aplicativo não obter uma vantagem movendo para **SQLCloseCursor** de **SQLFreeStmt** com SQL_CLOSE.
