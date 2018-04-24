---
title: Cursores de somente avanço | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 90ca5c097080d09276bc66754264fcf6ada658ea
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="forward-only-cursors"></a>Cursores de somente avanço
O tipo de cursor padrão típica, chamado de um cursor somente de avanço (ou não rolável), pode avançar apenas o conjunto de resultados. Um cursor de somente avanço não dá suporte a rolagem (a capacidade de mover para a frente e para trás no conjunto de resultados); suporta apenas a busca de linhas do início ao final do conjunto de resultados. Com alguns cursores de somente avanço (como com a biblioteca de cursores do SQL Server), todas as instruções delete, update e insert feitas pelo usuário atual (ou confirmadas por outros usuários) que afetam as linhas no conjunto de resultados são visíveis como as linhas buscadas. No entanto, como o cursor não pode ser revertido, as alterações feitas às linhas no banco de dados depois que a linha foi buscada não são visíveis pelo cursor.  
  
 Depois que os dados da linha atual são processados, o cursor de somente avanço libera os recursos que foram usados para armazenar dados. Cursores de somente avanço são dinâmicos por padrão, o que significa que todas as alterações são detectadas como a linha atual é processada. Isso fornece a abertura de cursor mais rápida e permite que o conjunto de resultados para exibir as atualizações feitas nas tabelas subjacentes.  
  
 Enquanto os cursores de somente avanço não dão suporte a rolagem para trás, seu aplicativo pode retornar ao início do conjunto de resultados por fechar e reabrir o cursor. Isso é uma maneira eficiente para trabalhar com quantidades pequenas de dados. Como alternativa, seu aplicativo pode ler o conjunto de resultados de uma vez, armazenar em cache os dados localmente e, em seguida, procure o cache de dados local.  
  
 Se seu aplicativo não exigir rolar pelo conjunto de resultados, o cursor somente de avanço é a melhor maneira de recuperar dados rapidamente com o mínimo de sobrecarga. Use o **adOpenForwardOnly CursorTypeEnum** para indicar que você deseja usar um cursor somente de encaminhamento no ADO.  
  
## <a name="see-also"></a>Consulte também  
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)
