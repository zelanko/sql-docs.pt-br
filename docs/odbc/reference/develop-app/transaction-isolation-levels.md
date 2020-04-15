---
title: Níveis de isolamento de transações (ODBC) | Microsoft Docs
ms.custom: seo-dt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- dirty reads [ODBC]
- isolation levels [ODBC]
- nonrepeatable reads [ODBC]
- read uncommitted [ODBC]
- read committed [ODBC]
- serializable reads [ODBC]
- phantoms [ODBC]
- transaction isolation [ODBC]
- repeatable reads [ODBC]
- transactions [ODBC], isolation
ms.assetid: 0d638d55-ffd0-48fb-834b-406f466214d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 622b4cd7f0db259b5ecfd5be63b27df64be965e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298029"
---
# <a name="transaction-isolation-levels-odbc"></a>Níveis de isolamento de transações (ODBC)
Os níveis de isolamento de *transações* são uma medida de até que ponto o isolamento das transações é bem sucedido. Em particular, os níveis de isolamento das transações são definidos pela presença ou ausência dos seguintes fenômenos:  
  
-   **Leituras Sujas** Uma *leitura suja* ocorre quando uma transação lê dados que ainda não foram cometidos. Por exemplo, suponha que a transação 1 atualize uma linha. A transação 2 lê a linha atualizada antes que a transação 1 comprometa a atualização. Se a transação 1 reverter a alteração, a transação 2 terá dados lidos que nunca existiram.  
  
-   **Leituras não repetíveis** Uma *leitura não repetível* ocorre quando uma transação lê a mesma linha duas vezes, mas obtém dados diferentes a cada vez. Por exemplo, suponha que a transação 1 leia uma linha. A transação 2 atualiza ou exclui essa linha e compromete a atualização ou exclusão. Se a transação 1 reler a linha, ela recuperará diferentes valores de linha ou descobrirá que a linha foi excluída.  
  
-   **Fantasmas** Um *fantasma* é uma linha que corresponde aos critérios de pesquisa, mas não é visto inicialmente. Por exemplo, suponha que a transação 1 leia um conjunto de linhas que satisfaçam alguns critérios de pesquisa. A transação 2 gera uma nova linha (através de uma atualização ou de uma inserção) que corresponde aos critérios de pesquisa para a transação 1. Se a transação 1 reexecutar a declaração que lê as linhas, ela obtém um conjunto diferente de linhas.  
  
 Os quatro níveis de isolamento de transações (definidos pelo SQL-92) são definidos em termos desses fenômenos. Na tabela a seguir, um "X" marca cada fenômeno que pode ocorrer.  
  
|Nível de isolamento de transações|Leituras sujas|Leituras não repetíveis|Fantasmas|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Leitura não confirmada|X|X|X|  
|Leitura confirmada|--|X|X|  
|Leitura repetida|--|--|X|  
|Serializável|--|--|--|  
  
 A tabela a seguir descreve maneiras simples de um DBMS implementar os níveis de isolamento da transação.  
  
> [!IMPORTANT]  
>  A maioria dos DBMSs usa esquemas mais complexos do que estes para aumentar a concorrência. Estes exemplos são fornecidos apenas para fins de ilustração. Em particular, a ODBC não prescreve como dbmss particulares isolam transações entre si.  
  
|Isolamento de transações|Possível implementação|  
|---------------------------|-----------------------------|  
|Leitura não confirmada|As transações não são isoladas umas das outras. Se o DBMS suporta outros níveis de isolamento de transações, ele ignora qualquer mecanismo que use para implementar esses níveis. Para que eles não afetem negativamente outras transações, as transações em execução no nível Read Uncommitted geralmente são somente leitura.|  
|Leitura confirmada|A transação aguarda até que as linhas bloqueadas por outras transações sejam desbloqueadas; isso impede que ele leia quaisquer dados "sujos".<br /><br /> A transação mantém um bloqueio de leitura (se ele só ler a linha) ou o bloqueio de gravação (se ele atualizar ou excluir a linha) na linha atual para impedir que outras transações atualizem ou excluam.a. A transação libera bloqueios de leitura quando ele sai da linha atual. Ele segura as travas de gravação até que seja comprometida ou revertida.|  
|Leitura repetida|A transação aguarda até que as linhas bloqueadas por outras transações sejam desbloqueadas; isso impede que ele leia quaisquer dados "sujos".<br /><br /> A transação mantém bloqueios de leitura em todas as linhas que retorna ao aplicativo e anota bloqueios em todas as linhas que insere, atualiza ou exclui. Por exemplo, se a transação incluir a declaração SQL **SELECT \* FROM Orders**, a transação bloqueia as linhas à medida que o aplicativo as busca. Se a transação incluir a declaração SQL **DELETE FROM Orders WHERE Status = 'CLOSED',** a transação bloqueia as linhas de gravação à medida que as exclui.<br /><br /> Como outras transações não podem atualizar ou excluir essas linhas, a transação atual evita leituras não repetíveis. A transação libera seus bloqueios quando está comprometida ou revertida.|  
|Serializável|A transação aguarda até que as linhas bloqueadas por outras transações sejam desbloqueadas; isso impede que ele leia quaisquer dados "sujos".<br /><br /> A transação mantém um bloqueio de leitura (se ele só lê linhas) ou bloqueio de gravação (se ele pode atualizar ou excluir linhas) na faixa de linhas que afeta. Por exemplo, se a transação incluir a declaração SQL **SELECT \* FROM Orders,** a faixa será toda a tabela Orders; a transação bloqueia a tabela e não permite que novas linhas sejam inseridas nela. Se a transação incluir a declaração SQL **DELETE FROM Orders WHERE Status = 'CLOSED',** o intervalo será todas as linhas com um Status de "CLOSED"; a transação bloqueia todas as linhas na tabela Ordens com um Status de "CLOSED" e não permite que nenhuma linha seja inserida ou atualizada de forma que a linha resultante tenha um Status de "CLOSED".<br /><br /> Como outras transações não podem atualizar ou excluir as linhas no intervalo, a transação atual evita leituras não repetíveis. Como outras transações não podem inserir nenhuma linha no intervalo, a transação atual evita quaisquer fantasmas. A transação libera seu bloqueio quando está comprometida ou revertida.|  
  
 É importante notar que o nível de isolamento da transação não afeta a capacidade de uma transação de ver suas próprias alterações; transações sempre podem ver quaisquer alterações que eles fazem. Por exemplo, uma transação pode consistir em duas demonstrações de **ATUALIZAÇÃO,** a primeira das quais aumenta o salário de todos os funcionários em 10% e a segunda estabelece o pagamento de qualquer funcionário sobre algum valor máximo a esse valor. Isso é bem sucedido como uma única transação apenas porque a segunda declaração **UPDATE** pode ver os resultados da primeira.
