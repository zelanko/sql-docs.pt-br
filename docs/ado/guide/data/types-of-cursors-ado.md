---
description: Tipos de cursor (ADO)
title: Tipos de cursores (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
author: rothja
ms.author: jroth
ms.openlocfilehash: ea996827565f0cc6d593078e7772c336699260bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452708"
---
# <a name="types-of-cursors-ado"></a>Tipos de cursor (ADO)
Como regra geral, seu aplicativo deve usar o cursor mais simples que fornece o acesso de dados necessário. Cada maior característica do cursor além dos conceitos básicos (somente encaminhamento, somente leitura, estático, rolagem, sem buffer) tem um preço na memória do cliente, na carga de rede ou no desempenho. Em muitos casos, as opções de cursor padrão geram um cursor mais complexo do que o seu aplicativo realmente precisa.  
  
 A escolha do tipo de cursor depende de como seu aplicativo usa o conjunto de resultados e também de várias considerações de design, incluindo o tamanho do conjunto de resultados, a porcentagem dos dados que provavelmente serão usados, a sensibilidade às alterações de dados e os requisitos de desempenho do aplicativo.  
  
 Em seu mais básico, a escolha do cursor depende se você precisa alterar ou simplesmente exibir os dados:  
  
-   Se você só precisa percorrer um conjunto de resultados, mas não alterar dados, use um cursor [estático](../../../ado/guide/data/static-cursors.md) ou [somente de avanço](../../../ado/guide/data/forward-only-cursors.md) .  
  
-   Se você tiver um conjunto de resultados grande e precisar selecionar apenas algumas linhas, use um cursor de conjunto de [chaves](../../../ado/guide/data/keyset-cursors.md) .  
  
-   Se você quiser sincronizar um conjunto de resultados com adições, alterações e exclusões recentes por todos os usuários simultâneos, use um cursor [dinâmico](../../../ado/guide/data/dynamic-cursors.md) .  
  
 Embora cada tipo de cursor pareça ser distinto, tenha em mente que esses tipos de cursor não são tão diferentes variedades que simplesmente o resultado de características e opções sobrepostas.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [Cursores estáticos](../../../ado/guide/data/static-cursors.md)  
  
-   [Cursores do conjunto de chaves](../../../ado/guide/data/keyset-cursors.md)  
  
-   [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores do conjunto de chaves](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)
