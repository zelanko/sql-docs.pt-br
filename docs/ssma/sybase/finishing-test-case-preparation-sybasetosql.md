---
title: Concluir a preparação do caso de teste (SybaseToSQL) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029144"
---
# <a name="finishing-test-case-preparation-sybasetosql"></a>Concluir a preparação do caso de teste (SybaseToSQL)
A página do assistente final exibe a descrição do caso de teste e informações sobre os objetos envolvidos no teste. Além disso, nesta página você pode definir o teste de opções de execução.  
  
O **informações de caso de teste** seção mostra o nome do caso de teste e a descrição.  
  
O **objetos de teste** seção contém a lista nomeada de objetos testados agrupados por tipo de objeto.  
  
O **afetados objetos a serem analisados** seção exibe a lista nomeada de objetos devem ser comparadas a quais alterações de dados após a execução de objetos testado.  
  
## <a name="test-case-settings"></a>Configurações de caso de teste  
No **configurações de caso de teste** seção, você pode definir opções de teste a execução a seguir:  
  
### <a name="stop-test-execution-after-first-failure"></a>Parar a execução de teste após a primeira falha  
Especifica para interromper o teste se ocorrer um erro durante a execução de teste.  
  
-   Se você escolher **Sim**, quebras de execução de teste, se ocorrer um erro.  
  
-   Se você escolher **não**, execução de teste continuará após um erro.  
  
### <a name="perform-data-rollback"></a>Executar a reversão de dados  
Habilite a reversão automática de dados após a execução de teste.  
  
-   Se você escolher **Sim**, as alterações de dados serão perdidas após a execução de teste.  
  
-   Se você escolher **não**, todas as alterações de dados serão salvas a execução de teste.  
  
### <a name="auxiliary-tables-saving-mode"></a>Tabelas auxiliares do modo de economia  
Define o modo de gravação para tabelas auxiliares criadas durante a execução de teste. Consulte a descrição de tabelas auxiliares na [casos de teste executando o &#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) tópico.  
  
-   Se você selecionar **sempre salvar**, dados de tabela auxiliar sempre serão armazenados para uso posterior.  
  
-   Se você selecionar **salvar se houve falha na comparação de tabela**, dados de tabela auxiliar serão armazenados somente se ocorrer um erro.  
  
-   Se você selecionar **sempre excluir**, tabelas auxiliares sempre ser excluído após a execução de teste.  
  
-   Se você selecionar **peça ao usuário se a falha na comparação de tabela**, o usuário pode selecionar a ação necessária, se ocorrer um erro.  
  
Clique o **terminar** botão para salvar o caso de teste preparado em [repositórios de teste usando o &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Usando repositórios de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[Executar casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testar objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
