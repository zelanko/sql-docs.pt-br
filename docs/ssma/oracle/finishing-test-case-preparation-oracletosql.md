---
title: Concluindo a preparação do caso de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 0cd80ee10d70b31f06c22e064d199c98cc1820b3
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934864"
---
# <a name="finishing-test-case-preparation-oracletosql"></a>Concluir a preparação do caso de teste (OracleToSQL)
A página final do assistente exibe a descrição do caso de teste e informações sobre objetos envolvidos no teste. Além disso, nesta página, você pode definir as opções de execução de teste.  
  
A seção **informações do caso de teste** mostra o nome e a descrição do caso de teste.  
  
A seção **objetos selecionados para teste** contém a lista nomeada de objetos testados agrupados por tipo de objeto.  
  
A seção **objetos afetados pelo teste que será analisado** exibe a lista nomeada de objetos que as alterações de dados devem ser comparadas após a execução dos objetos testados.  
  
## <a name="test-case-settings"></a>Configurações de caso de teste  
Na seção **configurações de caso de teste** , você pode definir as seguintes opções de teste de execução:  
  
### <a name="stop-test-execution-after-first-failure"></a>Parar a execução do teste após a primeira falha  
Especifica para interromper o teste se ocorrer um erro durante a execução do teste.  
  
-   Se você escolher **Sim**, o teste de execução será interrompido se ocorrer um erro.  
  
-   Se você escolher **não**, a execução do teste continuará após um erro.  
  
### <a name="perform-data-rollback"></a>Executar reversão de dados  
Habilita a reversão de dados automática após a execução do teste.  
  
-   Se você escolher **Sim**, as alterações de dados serão perdidas após a execução do teste.  
  
-   Se você escolher **não**, todas as alterações de dados de execução de teste serão salvas.  
  
### <a name="auxiliary-tables-saving-mode"></a>Modo de salvamento de tabelas auxiliares  
Define o modo de salvamento para tabelas auxiliares criadas durante a execução do teste. Consulte a descrição das tabelas auxiliares na seção [executando casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md) .  
  
-   Se você selecionar **sempre salvar**, os dados da tabela auxiliar sempre serão armazenados para uso posterior.  
  
-   Se você selecionar **salvar se a comparação de tabela falhar**, os dados da tabela auxiliar serão armazenados somente se ocorrer um erro.  
  
-   Se você selecionar **sempre excluir**, as tabelas auxiliares sempre serão excluídas após a execução do teste.  
  
-   Se você selecionar **perguntar ao usuário se a comparação de tabela falhar**, o usuário poderá selecionar a ação necessária se ocorrer um erro.  
  
Clique no botão **concluir** para salvar o caso de teste preparado em [usando repositórios de teste (OracleToSQL)](https://msdn.microsoft.com/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4).  
  
## <a name="see-also"></a>Consulte Também  
[Usando repositórios de teste &#40;OracleToSQL&#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[Executando casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testando objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
