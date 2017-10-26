---
title: SQLExtendedFetch (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 25a9e0b16551ca27a6818fcfd890e56aeabfb44b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade de API de ODBC: Nível 2  
  
 Semelhante ao [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) mas retorna várias linhas usando uma matriz para cada coluna. O conjunto de resultados é rolável de avanço e pode ser feito com versões anteriores rolável se o cursor está definido para ser estático, não somente de encaminhamento.  
  
 Por padrão, o Driver de ODBC do Visual FoxPro não retorna linhas marcadas como excluídas em uma tabela FoxPro. Linhas marcadas para exclusão, mas ainda não foram removidas de uma tabela não são incluídas no cursor de conjunto de resultados. Você pode alterar esse comportamento usando o [definido excluídas](../../odbc/microsoft/set-deleted-command.md) comando.  
  
 Para obter mais informações, consulte [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) no *referência do programador de ODBC*.

