---
title: Concluindo a preparação do caso de teste (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c3085d17804866015a78e93556dd5373d3a1b8cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029144"
---
# <a name="finishing-test-case-preparation-sybasetosql"></a>Concluir a preparação do caso de teste (SybaseToSQL)
A página final do assistente exibe a descrição do caso de teste e informações sobre objetos envolvidos no teste. Além disso, nesta página, você pode definir as opções de execução de teste.  
  
A seção **informações do caso de teste** mostra o nome e a descrição do caso de teste.  
  
A seção **Test Objects** contém a lista nomeada de objetos testados agrupados por tipo de objeto.  
  
A seção **objetos afetados a serem analisados** exibe a lista nomeada de objetos que as alterações de dados devem ser comparadas após a execução dos objetos testados.  
  
## <a name="test-case-settings"></a>Configurações de caso de teste  
Na seção **configurações de caso de teste** , você pode definir as seguintes opções de teste de execução:  
  
### <a name="stop-test-execution-after-first-failure"></a>Parar a execução do teste após a primeira falha  
Especifica para interromper o teste se ocorrer um erro durante a execução do teste.  
  
-   Se você escolher **Sim**, o teste de execução será interrompido se ocorrer um erro.  
  
-   Se você escolher **não**, a execução do teste continuará após um erro.  
  
### <a name="perform-data-rollback"></a>Executar reversão de dados  
Habilitar reversão de dados automática após a execução do teste.  
  
-   Se você escolher **Sim**, as alterações de dados serão perdidas após a execução do teste.  
  
-   Se você escolher **não**, todas as alterações de dados de execução de teste serão salvas.  
  
### <a name="auxiliary-tables-saving-mode"></a>Modo de salvamento de tabelas auxiliares  
Define o modo de salvamento para tabelas auxiliares criadas durante a execução do teste. Consulte a descrição das tabelas auxiliares na seção [executando casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md) .  
  
-   Se você selecionar **sempre salvar**, os dados da tabela auxiliar sempre serão armazenados para uso posterior.  
  
-   Se você selecionar **salvar se a comparação de tabela falhar**, os dados da tabela auxiliar serão armazenados somente se ocorrer um erro.  
  
-   Se você selecionar **sempre excluir**, as tabelas auxiliares sempre serão excluídas após a execução do teste.  
  
-   Se você selecionar **perguntar ao usuário se a comparação de tabela falhar**, o usuário poderá selecionar a ação necessária se ocorrer um erro.  
  
Clique no botão **concluir** para salvar o caso de teste preparado em [usando repositórios de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Usando repositórios de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[Executando casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testando objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
