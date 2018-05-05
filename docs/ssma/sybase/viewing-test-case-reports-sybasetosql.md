---
title: Exibindo relatórios de caso de teste (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 423726112ce1746695f2ee61f2c2668489b26555
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
[Casos de teste de execução &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Teste de objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
