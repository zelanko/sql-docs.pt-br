---
title: "Exibindo relatórios de caso de teste (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: adc23466083df093d778d907e932dc6bc6a30549
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="viewing-test-case-reports-sybasetosql"></a>Exibindo relatórios de caso de teste (SybaseToSQL)
O relatório de caso de teste mostra os resultados da verificação de teste e as informações de teste geral. Em caso de falha de teste, informações sobre quaisquer dados incompatíveis em objetos verificados também são exibidas.  
  
## <a name="report-structure"></a>Estrutura de relatório  
A parte superior do relatório mostra essas estatísticas:  
  
-   O número total de objetos testados e o número de objetos para o qual o teste foi bem-sucedido.  
  
-   O número total de tabelas verificadas e chaves estrangeiras e o número de tabelas e chaves estrangeiras correspondentes com êxito.  
  
-   A hora de início, hora de término do caso de teste e o tempo total gasto para execução.  
  
O restante do relatório mostra informações em quatro categorias:  
  
**Erros de pré-requisitos**  
Exibe todos os erros que ocorreram no **pré-requisitos** etapa. Normalmente, ele é ignorado.  
  
**Inicialização**  
Mostra o status de execução como **êxito** ou **falha**.  
  
**Objetos de resultado de teste**  
Uma comparação de resultados (sucesso ou falha) e as incompatibilidades SSMA Tester detectado em caso de falha.  
  
**Finalização**  
Mostra o status de execução como **êxito** ou **falha**.  
  
## <a name="see-also"></a>Consulte também  
[Executar casos de teste &#40; SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testando migrados objetos de banco de dados &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
