---
description: Exibir relatórios de caso de teste (OracleToSQL)
title: Exibindo relatórios de caso de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8da14323-9dd6-4019-bf79-3e8b972a9bc0
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 62dfe8db323cfbf640ca1dc0f7df5e0c78aec3a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88320032"
---
# <a name="viewing-test-case-reports-oracletosql"></a>Exibir relatórios de caso de teste (OracleToSQL)
O relatório de caso de teste mostra os resultados da verificação de teste e as informações gerais de teste. No caso de uma falha de teste, as informações sobre quaisquer dados incompatíveis em objetos verificados também são exibidas.  
  
## <a name="report-structure"></a>Estrutura do relatório  
A parte superior do relatório mostra essas estatísticas:  
  
-   O número total de objetos testados e o número de objetos para os quais o teste foi bem-sucedido.  
  
-   O número total de tabelas verificadas e chaves estrangeiras e o número de tabelas e chaves estrangeiras correspondentes com êxito.  
  
-   A hora de início, a hora de término do caso de teste e o tempo total gasto para execução.  
  
O restante do relatório mostra informações em quatro categorias:  
  
**Erros de pré-requisitos**  
Mostra os erros que ocorreram na **etapa de pré-requisitos.** Normalmente, ele é ignorado.  
  
**Initialization**  
Mostra o status de execução como **êxito** ou **falha**.  
  
**Resultado dos objetos de teste**  
Uma comparação de resultados (êxito ou falha) e as incompatibilidades que o SSMA Tester detectou em caso de falha.  
  
**Finalização**  
Mostra o status de execução como **êxito** ou **falha**.  
  
## <a name="see-also"></a>Consulte Também  
[Executando casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testando objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
