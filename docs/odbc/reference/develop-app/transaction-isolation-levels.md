---
title: Níveis de isolamento de transação (ODBC) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e11a0d76fc4a2daece7b6f4f50761d40933792be
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637219"
---
# <a name="transaction-isolation-levels-odbc"></a>Níveis de isolamento da transação (ODBC)
*Os níveis de isolamento da transação* são uma medida da extensão para a qual o isolamento da transação é executado com sucesso. Em particular, os níveis de isolamento da transação são definidos pela presença ou ausência dos seguintes fenômenos:  
  
-   **Leituras sujas** Uma *leitura suja* ocorre quando uma transação lê dados que ainda não foram confirmados. Por exemplo, suponha que a transação 1 atualize uma linha. A transação 2 lê a linha atualizada antes que a transação 1 confirme a atualização. Se a transação 1 reverter a alteração, a transação 2 terá dados de leitura que são considerados nunca existentes.  
  
-   **Leituras não repetíveis** Uma *leitura não reproduzível* ocorre quando uma transação lê a mesma linha duas vezes, mas obtém dados diferentes a cada vez. Por exemplo, suponha que a transação 1 Leia uma linha. A transação 2 atualiza ou exclui essa linha e confirma a atualização ou exclusão. Se a transação 1 reler a linha, ela recuperará valores de linha diferentes ou descobrirá que a linha foi excluída.  
  
-   **Fantasmas** Um *fantasma* é uma linha que corresponde aos critérios de pesquisa, mas que não é visto inicialmente. Por exemplo, suponha que a transação 1 Leia um conjunto de linhas que atendam a alguns critérios de pesquisa. A transação 2 gera uma nova linha (por meio de uma atualização ou uma inserção) que corresponde aos critérios de pesquisa para a transação 1. Se a transação 1 executar novamente a instrução que lê as linhas, ela obterá um conjunto diferente de linhas.  
  
 Os quatro níveis de isolamento da transação (conforme definido pelo SQL-92) são definidos em termos desses fenômenos. Na tabela a seguir, um "X" marca cada fenômeno que pode ocorrer.  
  
|Nível de isolamento da transação|Leituras sujas|Leituras não repetíveis|Fantasmas|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Leitura não confirmada|X|X|X|  
|Leitura confirmada|--|X|X|  
|Leitura repetida|--|--|X|  
|Serializable|--|--|--|  
  
 A tabela a seguir descreve maneiras simples de um DBMS implementar os níveis de isolamento da transação.  
  
> [!IMPORTANT]  
>  A maioria dos DBMSs usa esquemas mais complexos do que isso para aumentar a simultaneidade. Esses exemplos são fornecidos apenas para fins ilustrativos. Em particular, o ODBC não prescreve como DBMSs específicos isolam transações entre si.  
  
|Isolamento de transação|Implementação possível|  
|---------------------------|-----------------------------|  
|Leitura não confirmada|As transações não são isoladas umas das outras. Se o DBMS der suporte a outros níveis de isolamento de transação, ele ignorará qualquer mecanismo usado para implementar esses níveis. Para que eles não afetem negativamente outras transações, as transações em execução no nível de leitura não confirmada normalmente são somente leitura.|  
|Leitura confirmada|A transação aguarda até que as linhas de gravação bloqueadas por outras transações sejam desbloqueadas; Isso impede que ele leia os dados "sujos".<br /><br /> A transação mantém um bloqueio de leitura (se ele lê apenas a linha) ou o bloqueio de gravação (se ele atualizar ou excluir a linha) na linha atual para impedir que outras transações sejam atualizadas ou excluídas. A transação libera bloqueios de leitura quando ele sai da linha atual. Ela mantém bloqueios de gravação até que seja confirmada ou revertida.|  
|Leitura repetida|A transação aguarda até que as linhas de gravação bloqueadas por outras transações sejam desbloqueadas; Isso impede que ele leia os dados "sujos".<br /><br /> A transação mantém bloqueios de leitura em todas as linhas que ele retorna para o aplicativo e os bloqueios de gravação em todas as linhas que ele insere, atualiza ou exclui. Por exemplo, se a transação incluir a instrução SQL, **selecione \* de Orders**, a transação Read-Locks Rows enquanto o aplicativo as busca. Se a transação incluir a instrução SQL **delete de Orders, em que status = ' Closed '** , a transação Write-bloqueará as linhas à medida que excluí-las.<br /><br /> Como outras transações não podem atualizar ou excluir essas linhas, a transação atual evita quaisquer leituras não repetíveis. A transação libera seus bloqueios quando ela é confirmada ou revertida.|  
|Serializable|A transação aguarda até que as linhas de gravação bloqueadas por outras transações sejam desbloqueadas; Isso impede que ele leia os dados "sujos".<br /><br /> A transação mantém um bloqueio de leitura (se apenas lê linhas) ou bloqueio de gravação (se puder atualizar ou excluir linhas) no intervalo de linhas que ele afeta. Por exemplo, se a transação incluir a instrução SQL, **selecione \* de pedidos**, o intervalo será a tabela de pedidos inteira; a transação de leitura-bloqueia a tabela e não permite que nenhuma nova linha seja inserida nela. Se a transação incluir a instrução SQL **delete de Orders, em que status = ' Closed '** , o intervalo será todas as linhas com o status "closed"; a transação Write-bloqueia todas as linhas na tabela Orders com o status "CLOSED" e não permite que nenhuma linha seja inserida ou atualizada, de modo que a linha resultante tenha o status "CLOSED".<br /><br /> Como outras transações não podem atualizar ou excluir as linhas no intervalo, a transação atual evita quaisquer leituras não repetíveis. Como outras transações não podem inserir nenhuma linha no intervalo, a transação atual evita quaisquer fantasmas. A transação libera seu bloqueio quando é confirmada ou revertida.|  
  
 É importante observar que o nível de isolamento da transação não afeta a capacidade de uma transação de ver suas próprias alterações; as transações sempre podem ver quaisquer alterações feitas. Por exemplo, uma transação pode consistir em duas instruções **Update** , a primeira que eleva o pagamento de todos os funcionários em 10% e o segundo, que define o pagamento de qualquer funcionário em relação a um valor máximo para essa quantidade. Isso é bem sucedido como uma única transação somente porque a segunda instrução **Update** pode ver os resultados da primeira.
