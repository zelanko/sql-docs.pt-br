---
title: "Níveis de isolamento da transação | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 13997d3c8d4bb3c4ea5ff47ec6e8d4c95b303d21
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="transaction-isolation-levels"></a>Níveis de isolamento da transação
*Níveis de isolamento da transação* são uma medida da extensão para qual transação de isolamento é bem-sucedida. Em particular, os níveis de isolamento da transação são definidos pela presença ou ausência de fenômenos a seguir:  
  
-   **Sujas leituras** um *leitura suja* ocorre quando uma transação lê os dados que ainda não foram confirmados. Por exemplo, suponha que a transação 1 atualizações uma linha. Transação 2 lê a linha atualizada antes da transação 1 confirma a atualização. Se a transação 1 reverte a alteração, transação 2 têm lê dados que são considerados nunca ter existido.  
  
-   **Leituras não repetíveis** um *leitura não repetível* ocorre quando uma transação lê a mesma linha duas vezes, mas obtém dados diferentes a cada vez. Por exemplo, suponha que as leituras de transação 1 uma linha. Transação 2 atualiza ou exclui essa linha e confirma a atualização ou exclusão. Se a transação 1 relê a linha, ela recupera valores de linha diferente ou descobre que a linha foi excluída.  
  
-   **Fantasmas** um *fantasma* é uma linha que corresponde aos critérios de pesquisa, mas não é exibida inicialmente. Por exemplo, suponha que a transação 1 lê um conjunto de linhas que atenderem a alguns critérios de pesquisa. Transação 2 gera uma nova linha (por meio de uma atualização ou uma instrução insert) que corresponde aos critérios de pesquisa para a transação 1. Se a transação 1 reexecutes a instrução que lê as linhas, ele obtém um conjunto diferente de linhas.  
  
 Os níveis de isolamento de transação de quatro (conforme definido pelo SQL-92) são definidos em termos desses fenômenos. Na tabela a seguir, um "X" marca cada fenômeno que pode ocorrer.  
  
|Nível de isolamento da transação|Leituras sujas|Leituras não repetíveis|Fantasmas|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Leitura não confirmada|X|X|X|  
|Leitura confirmada|--|X|X|  
|Leitura repetida|--|--|X|  
|Serializável|--|--|--|  
  
 A tabela a seguir descreve as maneiras simples que um DBMS pode implementar os níveis de isolamento da transação.  
  
> [!IMPORTANT]  
>  DBMSs mais usam esquemas mais complexas que esses para aumentar a simultaneidade. Esses exemplos são fornecidos apenas para fins ilustrativos. Em particular, o ODBC não estabelece DBMSs específico como isolar transações entre si.  
  
|Isolamento de transação|Possível implementação|  
|---------------------------|-----------------------------|  
|Leitura não confirmada|As transações não são isoladas uma da outra. Se o DBMS for compatível com outros níveis de isolamento da transação, ele ignora qualquer mecanismo que ele usa para implementar os níveis. Para que elas não afetam negativamente outras transações, transações em execução em nível Read Uncommitted são geralmente somente leitura.|  
|Leitura confirmada|A transação aguarda até que o bloqueio de gravação por outras transações de linhas sejam desbloqueadas; Isso impede que ler todos os dados "sujos".<br /><br /> Mantém a transação que um bloqueio de leitura (se ele lê apenas a linha) ou de gravação de bloqueio (se ela atualiza ou exclui a linha) na linha atual para impedir que outras transações atualizem ou excluí-lo. A transação libera os bloqueios de leitura quando ele é movido para fora da linha atual. Ele mantém bloqueios de gravação até que ele é confirmado ou revertido.|  
|Leitura repetida|A transação aguarda até que o bloqueio de gravação por outras transações de linhas sejam desbloqueadas; Isso impede que ler todos os dados "sujos".<br /><br /> A transação mantém bloqueios de leitura em todas as linhas, que ele retorna para os bloqueios de aplicativo e gravar todas as linhas, ele inserções, atualizações ou exclui. Por exemplo, se a transação incluir a instrução SQL **selecione \* de pedidos**, os bloqueios de leitura de transação linhas como o aplicativo busca-los. Se a transação incluir a instrução SQL **excluir de pedidos onde Status = 'CLOSED'**, os bloqueios de gravação de transação conforme ele os exclui as linhas.<br /><br /> Como outras transações não podem atualizar ou excluir essas linhas, a transação atual evita qualquer leituras não repetíveis. A transação libera seus bloqueios quando ele for confirmado ou revertido.|  
|Serializável|A transação aguarda até que o bloqueio de gravação por outras transações de linhas sejam desbloqueadas; Isso impede que ler todos os dados "sujos".<br /><br /> A transação mantém um bloqueio de leitura (se ele lê apenas linhas) ou o bloqueio de gravação (se ele pode atualizar ou excluir linhas) no intervalo de linhas que ele afeta. Por exemplo, se a transação incluir a instrução SQL **selecione \* de pedidos**, o intervalo é de toda a tabela Orders; os bloqueios de leitura transação de tabela e não não permitir que as novas linhas a ser inserido nele. Se a transação incluir a instrução SQL **excluir de pedidos onde Status = 'CLOSED'**, o intervalo é de todas as linhas com um Status de "CLOSED"; os bloqueios de gravação de transação todas as linhas dos pedidos de tabela com um Status de "CLOSED" e não não permitir que qualquer linha a ser inserido ou atualizado, de modo que a linha resultante tem um Status de "CLOSED".<br /><br /> Porque outras transações não podem atualizar ou excluir as linhas no intervalo, a transação atual evita qualquer leituras não repetíveis. Porque outras transações não é possível inserir linhas no intervalo, a transação atual evita qualquer fantasmas. A transação libera o bloqueio quando ele for confirmado ou revertido.|  
  
 É importante observar que o nível de isolamento da transação não afeta a capacidade de uma transação para ver suas próprias alterações; as transações sempre podem ver qualquer alteração feita. Por exemplo, uma transação pode ser composto de dois **atualização** instruções, o primeiro deles gera o pagamento de todos os funcionários em 10 por cento e o segundo define o pagamento de funcionários por algum tempo máximo para esse valor. Essa operação é bem-sucedida como uma única transação porque a segunda **atualização** instrução pode ver os resultados da primeira.
