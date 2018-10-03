---
title: Tipos de cursor (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ecf079c86362aeae78b7c9ceaad640b0ad1519c4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47786954"
---
# <a name="types-of-cursors-ado"></a>Tipos de cursor (ADO)
Como regra geral, seu aplicativo deve usar o cursor mais simples que fornece acesso a dados necessários. Cada característica de cursor adicionais além do básico (somente avanço, somente leitura, estáticos, rolagem, sem buffer) tem um preço — na memória do cliente, a carga de rede ou desempenho. Em muitos casos, as opções de cursor padrão geram um cursor mais complexo do que seu aplicativo realmente precisa.  
  
 A escolha do tipo de cursor depende de como o aplicativo usa o conjunto de resultados e também em várias considerações de design, incluindo o tamanho do conjunto de resultados, a porcentagem dos dados podem ser usados, sensibilidade a alterações de dados e o desempenho do aplicativo requisitos.  
  
 Em sua forma mais básica, sua escolha de cursor depende se você precisa alterar ou simplesmente visualizar os dados:  
  
-   Se você apenas precisar rolar por um conjunto de resultados, mas não os dados de alteração, use uma [somente de avanço](../../../ado/guide/data/forward-only-cursors.md) ou [estático](../../../ado/guide/data/static-cursors.md) cursor.  
  
-   Se você tiver um conjunto de resultados grande e precisa selecionar apenas algumas linhas, use uma [keyset](../../../ado/guide/data/keyset-cursors.md) cursor.  
  
-   Se você deseja sincronizar um conjunto de resultados com recente adiciona, altera e exclui todos os usuários simultâneos, use uma [dinâmico](../../../ado/guide/data/dynamic-cursors.md) cursor.  
  
 Embora cada tipo de cursor parece ser distintos, lembre-se que esses tipos de cursor não são muito diferentes variedades como simples resultado das características e opções de sobreposição.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [Cursores estáticos](../../../ado/guide/data/static-cursors.md)  
  
-   [Cursores do conjunto de chaves](../../../ado/guide/data/keyset-cursors.md)  
  
-   [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>Consulte também  
 [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores keyset](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)
