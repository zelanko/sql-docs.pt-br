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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e54298e9c25777f10b92f322f1b1e6a3d94c243
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191755"
---
# <a name="concurrency-control"></a>Controle de simultaneidade
*Simultaneidade* é a capacidade de duas transações para usar os mesmos dados ao mesmo tempo, e com transação maior isolamento normalmente vem a redução de simultaneidade. Isso ocorre porque o isolamento de transação geralmente é implementado pelo bloqueio de linhas, e que mais linhas são bloqueadas, menos transações podem ser concluídas sem serem bloqueadas pelo menos temporariamente por uma linha bloqueada. Embora a redução de simultaneidade é aceita normalmente como uma compensação para os níveis mais altos de isolamento de transação necessários para manter a integridade do banco de dados, ele pode se tornar um problema em aplicativos interativos com a atividade de leitura/gravação alta que usar cursores.  
  
 Por exemplo, suponha que um aplicativo executa a instrução SQL **selecionar \* pedidos de**. Ele chama **SQLFetchScroll** para rolar ao redor do resultado definido e permite que o usuário atualizar, excluir ou inserir pedidos. Depois que o usuário atualiza, exclui ou insere um pedido, o aplicativo confirma a transação.  
  
 Se o nível de isolamento for Repeatable Read, a transação poderá - dependendo de como ele é implementado - bloquear cada linha retornada por **SQLFetchScroll**. Se o nível de isolamento é Serializable, a transação pode bloquear toda a tabela de pedidos. Em ambos os casos, a transação libera seus bloqueios somente quando ele é confirmado ou revertido. Portanto, se o usuário gasta muito tempo lendo pedidos e muito pouco tempo, atualizar, excluir ou inseri-los, a transação poderá facilmente bloquear um grande número de linhas, tornando-os disponíveis para outros usuários.  
  
 Isso é um problema, mesmo se o cursor é somente leitura e o aplicativo permite que o usuário leia apenas os pedidos existentes. Nesse caso, o aplicativo confirma a transação e libera os bloqueios, quando ele chama **SQLCloseCursor** (no modo de confirmação automática) ou **SQLEndTran** (no modo de confirmação manual).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tipos de simultaneidade](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Simultaneidade otimista](../../../odbc/reference/develop-app/optimistic-concurrency.md)
