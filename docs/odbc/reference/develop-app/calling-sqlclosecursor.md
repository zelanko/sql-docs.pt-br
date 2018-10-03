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
manager: craigg
ms.openlocfilehash: 7ee139dd652204c750c99d8bad8ab2b17c7c1ba1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685954"
---
# <a name="calling-sqlclosecursor"></a>Calling SQLCloseCursor
Porque **SQLCloseCursor** é quase o mesmo que **SQLFreeStmt** com SQL_CLOSE, o Gerenciador de Driver não mapeie essa função. Funções de substituição são mapeadas para que o existente ODBC 2 *. x* aplicativos podem mover facilmente para ODBC 3. *x* usando as novas funções. Uma movimentação desse tipo torna mais fácil para esses aplicativos começar a usar o novo ODBC 3. *x* funcionalidade dentro do código condicional de uma maneira modular. **SQLCloseCursor** não representa nenhuma nova funcionalidade. Um aplicativo não receberá qualquer vantagem ao mudar para **SQLCloseCursor** partir **SQLFreeStmt** com SQL_CLOSE.
