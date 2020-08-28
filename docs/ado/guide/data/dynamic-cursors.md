---
description: Cursores dinâmicos
title: Cursores dinâmicos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], dynamic
- dynamic cursors [ADO]
ms.assetid: 00460f30-8cf7-494e-82df-41012f40ae51
author: rothja
ms.author: jroth
ms.openlocfilehash: e8ce85233cec96af3d804652225b4d14698287db
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991347"
---
# <a name="dynamic-cursors"></a>Cursores dinâmicos
Cursores dinâmicos detectam todas as alterações feitas nas linhas no conjunto de resultados, independentemente de as alterações ocorrerem de dentro do cursor ou de outros usuários fora do cursor. Todas as instruções INSERT, Update e Delete feitas por todos os usuários são visíveis por meio do cursor. O cursor dinâmico pode detectar quaisquer alterações feitas nas linhas, na ordem e nos valores do conjunto de resultados depois que o cursor for aberto. As atualizações feitas fora do cursor não ficam visíveis até que sejam confirmadas (a menos que o nível de isolamento da transação do cursor esteja definido como "não confirmado").  
  
 Por exemplo, suponha que um cursor dinâmico busque duas linhas e outro aplicativo e, em seguida, atualize uma dessas linhas e exclua a outra. Se o cursor dinâmico então buscar essas linhas, ele não localizará a linha excluída, mas exibirá os novos valores para a linha atualizada.  
  
 O cursor dinâmico é uma boa opção se o aplicativo precisar detectar todas as atualizações simultâneas feitas por outros usuários. Use o **AdOpenDynamic CursorTypeEnum** para indicar que você deseja usar um cursor dinâmico no ADO.  
  
## <a name="see-also"></a>Consulte Também  
 [Cursores de somente avanço](./forward-only-cursors.md)   
 [Cursores estáticos](./static-cursors.md)   
 [Cursores do conjunto de chaves](./keyset-cursors.md)