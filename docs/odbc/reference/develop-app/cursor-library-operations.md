---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 748d917ad060609d40e40a24e5669cff37188691
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792658"
---
# <a name="cursor-library-operations"></a>Operações de biblioteca de cursor
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Se um aplicativo trabalhar com ODBC *2.x* driver faz chamadas para o ODBC *3.x* biblioteca de cursores, o aplicativo poderá usar o ODBC *3.x* recursos que não estão compatível com ODBC *2.x* driver. Um gravador de aplicativos deve ter cuidado como esses recursos são usados, no entanto. Uso de ODBC *3.x* biblioteca de cursores ODBC não faz *2.x* driver em ODBC *3.x* driver.
