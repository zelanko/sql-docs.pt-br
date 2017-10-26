---
title: Chamando SQLCloseCursor | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f0d8c7ccb49840ae9477fac5a002b94b79c98302
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="calling-sqlclosecursor"></a>Chamar SQLCloseCursor
Porque **SQLCloseCursor** é quase o mesmo que **SQLFreeStmt** com SQL_CLOSE, o Gerenciador de Driver não mapeia essa função. Funções de substituição são mapeadas para que existente ODBC 2*. x* aplicativos podem mover facilmente para ODBC 3.* x* usando as novas funções. Essas mudanças, torna mais fácil para esses aplicativos começar a usar o novo ODBC 3. *x* funcionalidade dentro do código condicional de forma modular. **SQLCloseCursor** não representam nenhuma nova funcionalidade. Um aplicativo não obter uma vantagem movendo para **SQLCloseCursor** de **SQLFreeStmt** com SQL_CLOSE.

