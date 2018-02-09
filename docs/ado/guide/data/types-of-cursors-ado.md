---
title: Tipos de cursores (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ec8ccca017236a8f6aa784d92e8304a98452f02
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="types-of-cursors-ado"></a>Tipos de cursores (ADO)
Como regra geral, seu aplicativo deve usar o cursor mais simples que fornece acesso a dados necessários. Cada característica de cursor adicionais além do básico (somente avanço, somente leitura, estáticos, rolagem, sem buffer) tem um preço — na memória do cliente, a carga de rede ou o desempenho. Em muitos casos, as opções de cursor padrão geram um cursor mais complexo do que realmente necessidades de seu aplicativo.  
  
 A escolha do tipo de cursor depende de como seu aplicativo usa o conjunto de resultados e também em várias considerações de design, incluindo o tamanho do conjunto de resultados, a porcentagem dos dados deve ser usado, sensibilidade a alterações de dados e o desempenho do aplicativo requisitos.  
  
 Basicamente, a escolha de cursor depende se você precisa alterar ou exibir apenas os dados:  
  
-   Se você precisar rolar por um conjunto de resultados, mas não os dados de alteração, use um [somente de avanço](../../../ado/guide/data/forward-only-cursors.md) ou [estático](../../../ado/guide/data/static-cursors.md) cursor.  
  
-   Se você tiver um conjunto de resultados grande e necessário selecionar apenas algumas linhas, use um [keyset](../../../ado/guide/data/keyset-cursors.md) cursor.  
  
-   Se você deseja sincronizar um conjunto de resultados com recente adiciona, altera e exclui todos os usuários simultâneos, use um [dinâmico](../../../ado/guide/data/dynamic-cursors.md) cursor.  
  
 Embora cada tipo de cursor parece ser distintos, tenha em mente que esses tipos de cursor não são muito diferentes variedades como simplesmente o resultado da sobreposição de características e opções.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [Cursores estáticos](../../../ado/guide/data/static-cursors.md)  
  
-   [Cursores do conjunto de chaves](../../../ado/guide/data/keyset-cursors.md)  
  
-   [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>Consulte também  
 [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)
