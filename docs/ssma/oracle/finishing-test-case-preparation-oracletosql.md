---
title: "Concluindo a preparação do caso de teste (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: f6bf969705a049e03212500a3112e643fbe7654a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="finishing-test-case-preparation-oracletosql"></a>Concluindo a preparação do caso de teste (OracleToSQL)
A página final do assistente exibe a descrição do caso de teste e informações sobre os objetos envolvidos no teste. Além disso, nessa página você pode definir o teste de opções de execução.  
  
O **informações de caso de teste** seção mostra o nome do caso de teste e a descrição.  
  
O **objetos selecionado para ser testado** seção contém a lista nomeada de testado objetos agrupados por tipo de objeto.  
  
O **objetos afetados pelo teste que será analisado** seção exibe a lista nomeada de objetos devem ser comparadas quais alterações de dados após a execução de objetos testado.  
  
## <a name="test-case-settings"></a>Configurações de caso de teste  
No **configurações de caso de teste** seção, você pode definir opções de teste a execução do seguinte:  
  
### <a name="stop-test-execution-after-first-failure"></a>Interromper a execução de teste após a primeira falha  
Especifica para interromper o teste se ocorrer um erro durante a execução de teste.  
  
-   Se você escolher **Sim**, quebras de execução de teste, se ocorrer um erro.  
  
-   Se você escolher **não**, execução de teste continuará após um erro.  
  
### <a name="perform-data-rollback"></a>Executar reversão de dados  
Permite que a reversão automática de dados após a execução de teste.  
  
-   Se você escolher **Sim**, as alterações de dados serão perdidas após a execução de teste.  
  
-   Se você escolher **não**, todas as alterações de dados serão salvas a execução de teste.  
  
### <a name="auxiliary-tables-saving-mode"></a>Modo de economia de tabelas auxiliares  
Define o modo de gravação para tabelas auxiliares criados durante a execução de teste. Consulte a descrição de tabelas auxiliares do [casos de teste em execução &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md) tópico.  
  
-   Se você selecionar **sempre salvar**, dados de tabela auxiliar sempre serão armazenados para uso posterior.  
  
-   Se você selecionar **salvar se houve falha na comparação de tabela**, dados de tabela auxiliar serão armazenados somente se ocorrer um erro.  
  
-   Se você selecionar **sempre excluir**, tabelas auxiliares sempre ser excluído após a execução de teste.  
  
-   Se você selecionar **peça ao usuário se a falha na comparação de tabela**, o usuário pode selecionar a ação necessária, se ocorrer um erro.  
  
Clique o **concluir** botão para salvar o caso de teste preparado em [usando repositórios de teste (OracleToSQL)](http://msdn.microsoft.com/en-us/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4).  
  
## <a name="see-also"></a>Consulte Também  
[Uso de repositórios de teste &#40; OracleToSQL &#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[Executar casos de teste &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testando migrados objetos de banco de dados &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
