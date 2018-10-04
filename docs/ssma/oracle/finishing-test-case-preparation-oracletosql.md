---
title: Concluir a preparação do caso de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 1b66f63b66066831d7e0276049d774136c1b5138
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743814"
---
# <a name="finishing-test-case-preparation-oracletosql"></a>Concluir a preparação do caso de teste (OracleToSQL)
A página do assistente final exibe a descrição do caso de teste e informações sobre os objetos envolvidos no teste. Além disso, nesta página você pode definir o teste de opções de execução.  
  
O **informações de caso de teste** seção mostra o nome do caso de teste e a descrição.  
  
O **objetos selecionados para serem testados** seção contém a lista nomeada de objetos testados agrupados por tipo de objeto.  
  
O **objetos afetados pelo teste que serão analisados** seção exibe a lista nomeada de objetos devem ser comparadas a quais alterações de dados após a execução de objetos testado.  
  
## <a name="test-case-settings"></a>Configurações de caso de teste  
No **configurações de caso de teste** seção, você pode definir opções de teste a execução a seguir:  
  
### <a name="stop-test-execution-after-first-failure"></a>Parar a execução de teste após a primeira falha  
Especifica para interromper o teste se ocorrer um erro durante a execução de teste.  
  
-   Se você escolher **Sim**, quebras de execução de teste, se ocorrer um erro.  
  
-   Se você escolher **não**, execução de teste continuará após um erro.  
  
### <a name="perform-data-rollback"></a>Executar a reversão de dados  
Permite que a reversão automática de dados após a execução de teste.  
  
-   Se você escolher **Sim**, as alterações de dados serão perdidas após a execução de teste.  
  
-   Se você escolher **não**, todas as alterações de dados serão salvas a execução de teste.  
  
### <a name="auxiliary-tables-saving-mode"></a>Tabelas auxiliares do modo de economia  
Define o modo de gravação para tabelas auxiliares criadas durante a execução de teste. Consulte a descrição de tabelas auxiliares na [casos de teste executando o &#40;OracleToSQL&#41; ](../../ssma/oracle/running-test-cases-oracletosql.md) tópico.  
  
-   Se você selecionar **sempre salvar**, dados de tabela auxiliar sempre serão armazenados para uso posterior.  
  
-   Se você selecionar **salvar se houve falha na comparação de tabela**, dados de tabela auxiliar serão armazenados somente se ocorrer um erro.  
  
-   Se você selecionar **sempre excluir**, tabelas auxiliares sempre ser excluído após a execução de teste.  
  
-   Se você selecionar **peça ao usuário se a falha na comparação de tabela**, o usuário pode selecionar a ação necessária, se ocorrer um erro.  
  
Clique o **terminar** botão para salvar o caso de teste preparado em [usando repositórios de teste (OracleToSQL)](http://msdn.microsoft.com/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4).  
  
## <a name="see-also"></a>Consulte também  
[Usando repositórios de teste &#40;OracleToSQL&#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[Executar casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testar objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
