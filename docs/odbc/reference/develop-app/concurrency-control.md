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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294846"
---
# <a name="concurrency-control"></a>Controle de simultaneidade
A *simultaneidade* é a capacidade de duas transações usarem os mesmos dados ao mesmo tempo e, com o maior isolamento da transação, geralmente vem com uma simultaneidade reduzida. Isso ocorre porque o isolamento de transação é geralmente implementado por linhas de bloqueio e, à medida que mais linhas são bloqueadas, menos transações podem ser concluídas sem serem bloqueadas pelo menos temporariamente por uma linha bloqueada. Embora a simultaneidade reduzida seja geralmente aceita como uma compensação para os níveis de isolamento de transação mais altos necessários para manter a integridade do banco de dados, ela pode se tornar um problema em aplicativos interativos com alta atividade de leitura/gravação que usa cursores.  
  
 Por exemplo, suponha que um aplicativo execute a instrução SQL **Select \* em Orders**. Ele chama **SQLFetchScroll** para rolar pelo conjunto de resultados e permite que o usuário atualize, exclua ou insira pedidos. Depois que o usuário atualiza, exclui ou insere um pedido, o aplicativo confirma a transação.  
  
 Se o nível de isolamento for de leitura repetida, a transação poderá-depender de como ela é implementada-bloquear cada linha retornada por **SQLFetchScroll**. Se o nível de isolamento for serializável, a transação poderá bloquear a tabela de pedidos inteira. Em ambos os casos, a transação libera seus bloqueios somente quando ele é confirmado ou revertido. Portanto, se o usuário gastar muito tempo lendo pedidos e, muito pouco, atualizando, excluindo ou inserindo-os, a transação poderá bloquear facilmente um grande número de linhas, tornando-as indisponíveis para outros usuários.  
  
 Esse é um problema, mesmo que o cursor seja somente leitura e o aplicativo permita que o usuário Leia apenas os pedidos existentes. Nesse caso, o aplicativo confirma a transação e libera os bloqueios, quando chama **SQLCloseCursor** (no modo de confirmação automática) ou **SQLEndTran** (no modo de confirmação manual).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de simultaneidade](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Simultaneidade otimista](../../../odbc/reference/develop-app/optimistic-concurrency.md)
