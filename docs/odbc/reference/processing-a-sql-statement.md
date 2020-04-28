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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349a62034d598c1bfb44b891b91359d5ff184b7e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280516"
---
# <a name="processing-a-sql-statement"></a>Processar uma instrução SQL
Antes de discutir as técnicas para usar o SQL programaticamente, é necessário discutir como uma instrução SQL é processada. As etapas envolvidas são comuns a todas as três técnicas, embora cada técnica as execute em momentos diferentes. A ilustração a seguir mostra as etapas envolvidas no processamento de uma instrução SQL, que são discutidas em todo o restante desta seção.  
  
 ![Etapas para processar uma instrução SQL](../../odbc/reference/media/pr01.gif "pr01")  
  
 Para processar uma instrução SQL, um DBMS executa as cinco etapas a seguir:  
  
1.  O DBMS primeiro analisa a instrução SQL. Ele quebra a instrução em palavras individuais, chamadas tokens, verifica se a instrução tem um verbo válido e cláusulas válidas e assim por diante. Erros de sintaxe e grafias incorretas podem ser detectados nesta etapa.  
  
2.  O DBMS valida a instrução. Ele verifica a instrução em relação ao catálogo do sistema. Todas as tabelas nomeadas na instrução existem no banco de dados? Todas as colunas existem e os nomes de coluna não são ambíguos? O usuário tem os privilégios necessários para executar a instrução? Certos erros semânticos podem ser detectados nesta etapa.  
  
3.  O DBMS gera um plano de acesso para a instrução. O plano de acesso é uma representação binária das etapas necessárias para executar a instrução; é o equivalente do DBMS do código executável.  
  
4.  O DBMS otimiza o plano de acesso. Ele explora várias maneiras de realizar o plano de acesso. Um índice pode ser usado para acelerar uma pesquisa? Se o DBMS primeiro aplicar um critério de pesquisa à tabela A e, em seguida, associá-lo à tabela B, ou se ele começar com a junção e usar a condição de pesquisa depois disso? Uma pesquisa sequencial em uma tabela pode ser evitada ou reduzida a um subconjunto da tabela? Depois de explorar as alternativas, o DBMS escolhe uma delas.  
  
5.  O DBMS executa a instrução executando o plano de acesso.  
  
 As etapas usadas para processar uma instrução SQL variam na quantidade de acesso ao banco de dados que precisam e na quantidade de tempo que demoram. A análise de uma instrução SQL não requer acesso ao banco de dados e pode ser feita muito rapidamente. A otimização, por outro lado, é um processo com uso intensivo de CPU e requer acesso ao catálogo do sistema. Para uma consulta multitabela complexa, o otimizador pode explorar milhares de diferentes maneiras de realizar a mesma consulta. No entanto, o custo da execução da consulta de forma ineficiente geralmente é tão alto que o tempo gasto na otimização é mais do que o que foi reobtido na velocidade de execução de consulta aumentada. Isso é ainda mais significativo se o mesmo plano de acesso otimizado puder ser usado repetidamente para executar consultas repetitivas.
