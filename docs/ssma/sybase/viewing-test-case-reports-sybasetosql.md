---
title: Exibindo relatórios de caso de teste (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 99bad46468ff0138c07f531c9e32cdecc4fda5be
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934520"
---
# <a name="viewing-test-case-reports-sybasetosql"></a>Exibir relatórios de caso de teste (SybaseToSQL)
O relatório de caso de teste mostra os resultados da verificação de teste e as informações gerais de teste. No caso de uma falha de teste, as informações sobre quaisquer dados incompatíveis em objetos verificados também são exibidas.  
  
## <a name="report-structure"></a>Estrutura do relatório  
A parte superior do relatório mostra essas estatísticas:  
  
-   O número total de objetos testados e o número de objetos para os quais o teste foi bem-sucedido.  
  
-   O número total de tabelas verificadas e chaves estrangeiras e o número de tabelas e chaves estrangeiras correspondentes com êxito.  
  
-   A hora de início, a hora de término do caso de teste e o tempo total gasto para execução.  
  
O restante do relatório mostra informações em quatro categorias:  
  
**Erros de pré-requisitos**  
Mostra os erros que ocorreram na etapa de **pré-requisitos** . Normalmente, ele é ignorado.  
  
**Initialization**  
Mostra o status de execução como **êxito** ou **falha**.  
  
**Resultado dos objetos de teste**  
Uma comparação de resultados (êxito ou falha) e as incompatibilidades que o SSMA Tester detectou em caso de falha.  
  
**Finalização**  
Mostra o status de execução como **êxito** ou **falha**.  
  
## <a name="see-also"></a>Consulte Também  
[Executando casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testando objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
