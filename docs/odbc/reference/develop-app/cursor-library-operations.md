---
title: Operações da Biblioteca do Cursor | Microsoft Docs
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
ms.openlocfilehash: a2297e72aacad7ea91b7af934a47bebbc61f0686
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301613"
---
# <a name="cursor-library-operations"></a>Operações de biblioteca de cursor
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Se um aplicativo que trabalha com um driver ODBC *2.x* fizer chamadas para a biblioteca de cursor ODBC *3.x,* o aplicativo poderá usar recursos ODBC *3.x* que não são suportados pelo driver ODBC *2.x.* No entanto, um autor de aplicativos deve ter cuidado com a forma como esses recursos são usados. O uso da biblioteca de cursor ODBC *3.x* não faz um driver ODBC *2.x* em um driver ODBC *3.x.*
