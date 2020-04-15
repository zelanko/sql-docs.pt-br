---
title: Controle de simultaneidade | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8afba3b3b8c8fee1307473c790186d509b37d982
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294846"
---
# <a name="concurrency-control"></a>Controle de simultaneidade
*A concorrência* é a capacidade de duas transações de usar os mesmos dados ao mesmo tempo, e com o aumento do isolamento das transações geralmente vem a concorrência reduzida. Isso ocorre porque o isolamento das transações geralmente é implementado por linhas de bloqueio e, à medida que mais linhas são bloqueadas, menos transações podem ser concluídas sem serem bloqueadas pelo menos temporariamente por uma linha bloqueada. Embora a concorrência reduzida seja geralmente aceita como uma troca para os níveis mais altos de isolamento de transações necessários para manter a integridade do banco de dados, ela pode se tornar um problema em aplicativos interativos com alta atividade de leitura/gravação que usam cursores.  
  
 Por exemplo, suponha que um aplicativo execute a declaração SQL **SELECT \* FROM Orders**. Ele chama **SQLFetchScroll** para percorrer o conjunto de resultados e permite que o usuário atualize, exclua ou insira ordens. Depois que o usuário atualiza, exclui ou insere um pedido, o aplicativo comete a transação.  
  
 Se o nível de isolamento for Read Repetível, a transação pode - dependendo de como ela é implementada - bloquear cada linha retornada pelo **SQLFetchScroll**. Se o nível de isolamento for serializável, a transação pode bloquear toda a tabela Orders. Em ambos os casos, a transação libera seus bloqueios somente quando está comprometida ou revertida. Assim, se o usuário gasta muito tempo lendo pedidos e muito pouco tempo atualizando, excluindo ou inserindo-os, a transação pode facilmente bloquear um grande número de linhas, tornando-as indisponíveis para outros usuários.  
  
 Isso é um problema, mesmo que o cursor seja somente leitura e o aplicativo permita que o usuário leia apenas as ordens existentes. Neste caso, o aplicativo comete a transação e libera bloqueios, quando ele chama **SQLCloseCursor** (no modo de confirmação automática) ou **SQLEndTran** (no modo de confirmação manual).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de simultaneidade](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Concorrência Otimista](../../../odbc/reference/develop-app/optimistic-concurrency.md)
