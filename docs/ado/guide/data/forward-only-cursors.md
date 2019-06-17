---
title: Cursores de somente avanço | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 15d11b8882e8e39a03ffb7509526a4f66b6553b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700708"
---
# <a name="forward-only-cursors"></a>Cursores de somente avanço
O tipo de cursor padrão típica, chamado de um cursor somente de avanço (ou não rolável), pode avançar somente por meio do conjunto de resultados. Um cursor de somente avanço não dá suporte a rolagem (a capacidade de mover para frente e para trás no conjunto de resultados); ele só dá suporte à busca linhas do início ao final do conjunto de resultados. Com alguns cursores de somente avanço (como com a biblioteca de cursores do SQL Server), todas as instruções delete, update e insert feitas pelo usuário atual (ou confirmadas por outros usuários) que afetam as linhas no conjunto de resultados são visíveis como as linhas sejam buscadas. Porém, como o cursor não podem ser revertido, as alterações feitas nas linhas no banco de dados depois que a linha foi buscada não são visíveis pelo cursor.  
  
 Depois que os dados da linha atual são processados, o cursor de somente avanço libera os recursos que foram usados para manter esses dados. Cursores somente de avanço são dinâmicos por padrão, o que significa que todas as alterações são detectadas conforme a linha atual é processada. Isso permite uma abertura do cursor mais rápida e que o conjunto de resultados exiba as atualizações feitas nas tabelas subjacentes.  
  
 Embora os cursores de somente avanço não dão suporte a rolagem para trás, seu aplicativo pode retornar ao início do conjunto de resultados por fechar e reabrir o cursor. Isso é uma maneira eficiente para trabalhar com quantidades pequenas de dados. Como alternativa, seu aplicativo pode ler o conjunto de resultados de uma vez, armazenar em cache os dados localmente e, em seguida, procure o cache de dados local.  
  
 Se seu aplicativo não exigir a rolagem por meio do conjunto de resultados, o cursor de somente avanço é a melhor maneira de recuperar dados rapidamente com a menor quantidade de sobrecarga. Use o **adOpenForwardOnly CursorTypeEnum** para indicar que você deseja usar um cursor de somente avanço no ADO.  
  
## <a name="see-also"></a>Consulte também  
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores keyset](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)
