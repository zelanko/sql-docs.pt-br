---
title: "Processando uma instrução SQL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 147d3a17b4041caf3a83ec819d65dc43af32312f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="processing-a-sql-statement"></a>Processando uma instrução SQL
Antes de discutir as técnicas para usar o SQL por meio de programação, é necessário discutir como uma instrução SQL é processada. As etapas envolvidas são comuns a todas as três técnicas, embora cada técnica executa-los em momentos diferentes. A ilustração a seguir mostra as etapas envolvidas no processamento de uma instrução SQL, que são abordados no restante desta seção.  
  
 ![Etapas para processar uma instrução SQL](../../odbc/reference/media/pr01.gif "pr01")  
  
 Para processar uma instrução SQL, um DBMS executa estas etapas:  
  
1.  O DBMS primeiro analisa a instrução SQL. Ele divide a instrução em palavras individuais, chamadas de tokens, certifica-se de que a instrução tem um verbo válido e cláusulas válidas e assim por diante. Erros de ortografia e erros de sintaxe podem ser detectados nesta etapa.  
  
2.  O DBMS valida a instrução. Verifica se a instrução no catálogo do sistema. Todas as tabelas nomeadas na instrução existem no banco de dados? Todas as colunas existentes e são os nomes de coluna ambíguo? O usuário tem os privilégios necessários para executar a instrução? Determinados erros semânticos podem ser detectados nesta etapa.  
  
3.  O DBMS gera um plano de acesso para a instrução. O plano de acesso é uma representação binária das etapas que são necessárias para executar a instrução; é o equivalente do DBMS de código executável.  
  
4.  O DBMS otimiza o plano de acesso. Ele explora várias maneiras de executar o plano de acesso. Um índice pode ser usado para acelerar a uma pesquisa? Deve DBMS primeiro aplicar um critério de pesquisa a tabela e, em seguida, associá-lo a tabela B, ou deve começar com a junção e usar o critério de pesquisa posteriormente? Uma pesquisa sequencial por meio de uma tabela pode ser evitada ou reduzida a um subconjunto da tabela? Depois de explorar as alternativas, o DBMS escolhe um deles.  
  
5.  O DBMS executa a instrução, executando o plano de acesso.  
  
 As etapas usadas para processar uma instrução SQL variam na quantidade precisam de acesso de banco de dados e a quantidade de tempo. A análise de uma instrução SQL não requer acesso ao banco de dados e pode ser feito rapidamente. Otimização, por outro lado, é um muito intensivo de CPU processar e requer acesso ao catálogo do sistema. Para uma consulta complexa, várias tabelas, o otimizador pode explorar milhares de diferentes maneiras de executar a mesma consulta. No entanto, o custo da execução da consulta ineficiente geralmente é tão alto que o tempo gasto na otimização mais de é recuperado em tempo de execução de consulta maior. Isso é ainda mais significativo se o mesmo plano otimizado de acesso pode ser usado repetidamente para realizar consultas repetitivas.
