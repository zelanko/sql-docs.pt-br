---
title: "Operações de biblioteca de cursor | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 25c26cfd81d4ad494406a0559b98c8d6e85a7ded
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="cursor-library-operations"></a>Operações de biblioteca de cursor
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Se um aplicativo trabalhando com um ODBC 2*. x* driver faz chamadas para o ODBC 3. *x* biblioteca de cursores, o aplicativo pode ser capaz de usar o ODBC 3. *x* recursos que não são suportados pelo ODBC 2*. x* driver. Um gravador de aplicativos deve ser cuidadoso como esses recursos são usados, no entanto. Uso de ODBC 3. *x* biblioteca de cursores não faz um ODBC 2*. x* driver em um ODBC 3. *x* driver.
