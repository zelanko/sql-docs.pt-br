---
description: Operações de biblioteca de cursor
title: Operações de biblioteca de cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: efe3191e264fe45307ef90624f6b6e76d4ccaff6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429408"
---
# <a name="cursor-library-operations"></a>Operações de biblioteca de cursor
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Se um aplicativo que trabalha com um driver ODBC *2. x* fizer chamadas para a biblioteca de cursores *3. x* ODBC, o aplicativo poderá usar os recursos ODBC *3. x* que não têm suporte do driver ODBC *2. x* . No entanto, um gravador de aplicativos deve ter cuidado com a forma como esses recursos são usados. O uso da biblioteca de cursores do ODBC *3. x* não faz um driver ODBC *2. x* para um driver ODBC *3. x* .
