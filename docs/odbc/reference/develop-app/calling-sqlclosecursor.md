---
title: Chamar SQLCloseCursor | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 447a0892049317813fa9fe6986e6219922a11e28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068689"
---
# <a name="calling-sqlclosecursor"></a>Calling SQLCloseCursor
Porque **SQLCloseCursor** é quase o mesmo que **SQLFreeStmt** com SQL_CLOSE, o Gerenciador de Driver não mapeie essa função. Funções de substituição são mapeadas para que o existente ODBC *2.x* aplicativos podem mover facilmente para ODBC *3.x* usando as novas funções. Uma movimentação desse tipo torna mais fácil para esses aplicativos começar a usar o novo ODBC *3.x* funcionalidade dentro do código condicional de uma maneira modular. **SQLCloseCursor** não representa nenhuma nova funcionalidade. Um aplicativo não receberá qualquer vantagem ao mudar para **SQLCloseCursor** partir **SQLFreeStmt** com SQL_CLOSE.
