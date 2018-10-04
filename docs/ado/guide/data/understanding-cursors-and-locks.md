---
title: Noções básicas sobre cursores e bloqueios | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO]
- cursors [ADO]
ms.assetid: c1b7d7e6-1707-4ce2-863f-0c6dea967df6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5c5a0d7d51acfd2ecf6d0ffda945a6223c7e04f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696955"
---
# <a name="understanding-cursors-and-locks"></a>Noções básicas sobre cursores e bloqueios
É importante entender como os cursores funcionam para que você possa selecionar o tipo de cursor melhor e mais eficiente para requisitos de acesso a dados do aplicativo. Uma configuração de cursor menos aquém do ideal pode fazer operações de acesso a dados lamentavelmente lentas.  
  
 Muitos recursos do ADO **Recordset** objeto são determinados pelo tipo e local do cursor, bem como o tipo de bloqueio.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [O que é um cursor?](../../../ado/guide/data/what-is-a-cursor.md)  
  
-   [Tipos de cursor](../../../ado/guide/data/types-of-cursors-ado.md)  
  
-   [A importância da posição do cursor](../../../ado/guide/data/the-significance-of-cursor-location.md)  
  
-   [O Microsoft Cursor Service para OLE DB](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md)  
  
-   [O que é um bloqueio?](../../../ado/guide/data/what-is-a-lock.md)  
  
-   [Usando CacheSize](../../../ado/guide/data/using-cachesize.md)  
  
-   [Características de cursor e de bloqueio](../../../ado/guide/data/cursor-and-lock-characteristics.md)
