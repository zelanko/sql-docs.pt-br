---
title: Processando uma declaração SQL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349a62034d598c1bfb44b891b91359d5ff184b7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280516"
---
# <a name="processing-a-sql-statement"></a>Processar uma instrução SQL
Antes de discutir as técnicas de uso de SQL programáticamente, é necessário discutir como uma declaração SQL é processada. As etapas envolvidas são comuns às três técnicas, embora cada técnica as realize em momentos diferentes. A ilustração a seguir mostra as etapas envolvidas no processamento de uma declaração SQL, que são discutidas ao longo do resto desta seção.  
  
 ![Etapas para processar uma instrução SQL](../../odbc/reference/media/pr01.gif "pr01")  
  
 Para processar uma declaração SQL, um DBMS executa os seguintes cinco passos:  
  
1.  O DBMS analisa primeiro a declaração SQL. Ele divide a declaração em palavras individuais, chamadas tokens, garante que a declaração tenha um verbo válido e cláusulas válidas, e assim por diante. Erros de sintaxe e erros ortográficos podem ser detectados nesta etapa.  
  
2.  O DBMS valida a declaração. Ele verifica a declaração contra o catálogo do sistema. Todas as tabelas nomeadas na declaração existem no banco de dados? Todas as colunas existem e os nomes das colunas são inequívocos? O usuário tem os privilégios necessários para executar a declaração? Certos erros semânticos podem ser detectados nesta etapa.  
  
3.  O DBMS gera um plano de acesso para a declaração. O plano de acesso é uma representação binária das etapas necessárias para a realização da declaração; é o equivalente dbms de código executável.  
  
4.  O DBMS otimiza o plano de acesso. Explora várias maneiras de realizar o plano de acesso. Um índice pode ser usado para acelerar uma pesquisa? O DBMS deve primeiro aplicar uma condição de pesquisa à Tabela A e, em seguida, junte-se à Tabela B, ou deve começar com a adesão e usar a condição de pesquisa depois? Uma pesquisa seqüencial através de uma tabela pode ser evitada ou reduzida a um subconjunto da tabela? Depois de explorar as alternativas, o DBMS escolhe uma delas.  
  
5.  O DBMS executa a declaração executando o plano de acesso.  
  
 As etapas utilizadas para processar uma declaração SQL variam na quantidade de acesso ao banco de dados que eles requerem e na quantidade de tempo que levam. Analisar uma declaração SQL não requer acesso ao banco de dados e pode ser feito muito rapidamente. A otimização, por outro lado, é um processo muito intensivo em CPU e requer acesso ao catálogo do sistema. Para uma consulta complexa e multilável, o otimizador pode explorar milhares de maneiras diferentes de realizar a mesma consulta. No entanto, o custo de execução da consulta de forma ineficiente geralmente é tão alto que o tempo gasto na otimização é mais do que recuperado em maior velocidade de execução de consultas. Isso é ainda mais significativo se o mesmo plano de acesso otimizado puder ser usado repetidamente para realizar consultas repetitivas.
