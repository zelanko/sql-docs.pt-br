---
title: Processando uma instrução SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: edf912bf3b8073a05dd900cd00511715020ee0c2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808984"
---
# <a name="processing-a-sql-statement"></a>Processar uma instrução SQL
Antes de discutir as técnicas para usar o SQL por meio de programação, é necessário discutir como uma instrução SQL é processada. As etapas envolvidas são comuns a todas as três técnicas, embora cada técnica executa-los em momentos diferentes. A ilustração a seguir mostra as etapas envolvidas no processamento de uma instrução SQL, que são discutidos no restante desta seção.  
  
 ![Etapas para processar uma instrução SQL](../../odbc/reference/media/pr01.gif "pr01")  
  
 Para processar uma instrução SQL, um DBMS executa estas etapas:  
  
1.  O DBMS primeiro analisa a instrução SQL. Ele divide a instrução em palavras individuais, chamadas de tokens, torna-se de que a instrução tem um verbo válido e cláusulas válidas e assim por diante. Erros de ortografia e erros de sintaxe podem ser detectados nesta etapa.  
  
2.  O DBMS valida a instrução. Ele verifica a instrução no catálogo do sistema. Todas as tabelas nomeadas na instrução existem no banco de dados? Todas as colunas existem e são os nomes de coluna ambíguo? O usuário tem os privilégios necessários para executar a instrução? Determinados erros semânticos podem ser detectados nesta etapa.  
  
3.  O DBMS gera um plano de acesso para a instrução. O plano de acesso é uma representação binária das etapas que são necessárias para executar a instrução; é o equivalente do DBMS do código executável.  
  
4.  O DBMS otimiza o plano de acesso. Ele explora as várias maneiras de executar o plano de acesso. Um índice pode ser usado para acelerar uma pesquisa? Deve DBMS primeiro aplicar um critério de pesquisa a tabela A e, em seguida, associá-lo a tabela B, ou deve começar com a junção e usar o critério de pesquisa mais tarde? Uma pesquisa sequencial por meio de uma tabela pode ser evitada ou reduzida para um subconjunto da tabela? Depois de explorar as alternativas, o DBMS escolherá um deles.  
  
5.  O DBMS executa a instrução, executando o plano de acesso.  
  
 As etapas usadas para processar uma instrução SQL variam na quantidade de acesso de banco de dados que eles exigem e a quantidade de tempo que elas levam. Análise de uma instrução SQL não requer acesso ao banco de dados e pode ser feito muito rapidamente. Otimização, por outro lado, é um muito intensivo de CPU processar e requer acesso ao catálogo do sistema. Para uma consulta complexa, várias tabelas, o otimizador pode explorar milhares de diferentes maneiras de realizar a mesma consulta. No entanto, o custo da execução da consulta de maneira ineficiente geralmente é tão alto que o tempo gasto na otimização mais do que foi recuperado na velocidade de execução de consulta maior. Isso é ainda mais significativo se o mesmo plano otimizado de acesso pode ser usado repetidamente para realizar consultas repetitivas.
