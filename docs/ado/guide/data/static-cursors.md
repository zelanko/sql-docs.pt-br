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
manager: jroth
ms.openlocfilehash: e8337a6e93aba36e8b5838dcbf6d2e084fe022f1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700344"
---
# <a name="static-cursors"></a>Cursores estáticos
O cursor estático sempre exibe o resultado definido como ele era quando o cursor foi aberto pela primeira vez. Dependendo da implementação, os cursores estáticos são somente leitura ou leitura/gravação e fornecer a rolagem para frente e para trás. O cursor estático não detecta normalmente, as alterações feitas à associação, ordem ou valores do conjunto de resultados depois que o cursor é aberto. Cursores estáticos podem detectar as próprias atualizações, exclusões e inserções, embora não precisem fazer isso.  
  
 Cursores estáticos detectam nunca outras atualizações, exclusões e inserções. Por exemplo, suponha que um cursor estático busque uma linha e outro aplicativo então atualize a linha. Se o aplicativo buscar novamente a linha do cursor estático, os valores que ele verá estarão inalterados, apesar das alterações feitas por outro aplicativo. Há suporte para todos os tipos de rolagem, mas os provedores podem ou não podem dar suporte a indicadores.  
  
 Se seu aplicativo não precisa detectar alterações de dados e requer a rolagem, o cursor estático é a melhor opção. Use o **adOpenStatic CursorTypeEnum** para indicar que você deseja usar um cursor estático no ADO.  
  
## <a name="see-also"></a>Consulte também  
 [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores keyset](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)
