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
author: rothja
ms.author: jroth
ms.openlocfilehash: 13a175d9e98fec5795c2756e79f96304b2ab2cc6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759012"
---
# <a name="understanding-cursors-and-locks"></a>Noções básicas sobre cursores e bloqueios
É importante entender como os cursores funcionam para que você possa selecionar o melhor e mais eficiente tipo de cursor para os requisitos de acesso a dados de um aplicativo. Uma configuração de cursor menos do que o ideal pode tornar as operações de acesso a dados um pouco lentas.  
  
 Muitos recursos do objeto **RECORDSET** ADO são determinados pelo tipo e pelo local do cursor, bem como pelo tipo de bloqueio.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [O que é um cursor?](../../../ado/guide/data/what-is-a-cursor.md)  
  
-   [Tipos de cursores](../../../ado/guide/data/types-of-cursors-ado.md)  
  
-   [A importância da posição do cursor](../../../ado/guide/data/the-significance-of-cursor-location.md)  
  
-   [O Microsoft Cursor Service para OLE DB](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md)  
  
-   [O que é um bloqueio?](../../../ado/guide/data/what-is-a-lock.md)  
  
-   [Usar CacheSize](../../../ado/guide/data/using-cachesize.md)  
  
-   [Características de cursor e de bloqueio](../../../ado/guide/data/cursor-and-lock-characteristics.md)
