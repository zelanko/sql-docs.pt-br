---
title: Cursores estáticos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 520c484bdaaa6eb59488900208993a607c5b0f7b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924114"
---
# <a name="static-cursors"></a>Cursores estáticos
O cursor estático sempre exibe o conjunto de resultados como foi quando o cursor foi aberto pela primeira vez. Dependendo da implementação, cursores estáticos são somente leitura ou de leitura/gravação e fornecem rolagem para frente e para trás. O cursor estático geralmente não detecta alterações feitas na associação, na ordem ou nos valores do conjunto de resultados depois que o cursor é aberto. Cursores estáticos podem detectar as próprias atualizações, exclusões e inserções, embora não precisem fazer isso.  
  
 Cursores estáticos nunca detectam outras atualizações, exclusões e inserções. Por exemplo, suponha que um cursor estático busque uma linha e outro aplicativo então atualize a linha. Se o aplicativo buscar novamente a linha do cursor estático, os valores que ele verá estarão inalterados, apesar das alterações feitas por outro aplicativo. Todos os tipos de rolagem têm suporte, mas os provedores podem ou não dar suporte a indicadores.  
  
 Se seu aplicativo não precisar detectar alterações de dados e exigir rolagem, o cursor estático será a melhor opção. Use o **AdOpenStatic CursorTypeEnum** para indicar que você deseja usar um cursor estático no ADO.  
  
## <a name="see-also"></a>Consulte Também  
 [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores do conjunto de chaves](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)
