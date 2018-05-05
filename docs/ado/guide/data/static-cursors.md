---
title: Cursores estáticos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a837ce0d285f24772be5a88e29c0929e398e6582
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="static-cursors"></a>Cursores estáticos
O cursor estático sempre exibe o conjunto de resultados como ele era quando o cursor foi aberto pela primeira vez. Dependendo da implementação, Cursores estáticos são somente leitura ou leitura/gravação e fornecer a rolagem para frente e para trás. O cursor estático não detecta normalmente as alterações feitas à associação, ordem ou valores do conjunto de resultados depois que o cursor é aberto. Cursores estáticos podem detectar suas próprias atualizações, exclusões e inserções, embora eles não são necessários para fazer isso.  
  
 Cursores estáticos nunca detectam outros atualiza, exclui e insere. Por exemplo, suponha que um cursor estático busca uma linha e outro aplicativo, em seguida, atualiza a linha. Se o aplicativo refetches a linha do cursor estático, os valores que ele vê são inalterados, apesar das alterações feitas por outro aplicativo. Há suporte para todos os tipos de rolagem, mas provedores podem ou não podem oferecer suporte a indicadores.  
  
 Se seu aplicativo não precisa detectar alterações de dados e exige a rolagem, o cursor estático é a melhor opção. Use o **adOpenStatic CursorTypeEnum** para indicar que você deseja usar um cursor estático no ADO.  
  
## <a name="see-also"></a>Consulte também  
 [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)
