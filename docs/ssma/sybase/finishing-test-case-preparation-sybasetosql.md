---
title: "Concluindo a preparação do caso de teste (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7568e7a78e0129204a23797cbc589139816ac13e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="finishing-test-case-preparation-sybasetosql"></a>Concluindo a preparação do caso de teste (SybaseToSQL)
A página final do assistente exibe a descrição do caso de teste e informações sobre os objetos envolvidos no teste. Além disso, nessa página você pode definir o teste de opções de execução.  
  
O **informações de caso de teste** seção mostra o nome do caso de teste e a descrição.  
  
O **teste objetos** seção contém a lista nomeada de testado objetos agrupados por tipo de objeto.  
  
O **objetos afetados a serem analisados** seção exibe a lista nomeada de objetos devem ser comparadas quais alterações de dados após a execução de objetos testado.  
  
## <a name="test-case-settings"></a>Configurações de caso de teste  
No **configurações de caso de teste** seção, você pode definir opções de teste a execução do seguinte:  
  
### <a name="stop-test-execution-after-first-failure"></a>Interromper a execução de teste após a primeira falha  
Especifica para interromper o teste se ocorrer um erro durante a execução de teste.  
  
-   Se você escolher **Sim**, quebras de execução de teste, se ocorrer um erro.  
  
-   Se você escolher **não**, execução de teste continuará após um erro.  
  
### <a name="perform-data-rollback"></a>Executar reversão de dados  
Habilite a reversão automática de dados após a execução de teste.  
  
-   Se você escolher **Sim**, as alterações de dados serão perdidas após a execução de teste.  
  
-   Se você escolher **não**, todas as alterações de dados serão salvas a execução de teste.  
  
### <a name="auxiliary-tables-saving-mode"></a>Modo de economia de tabelas auxiliares  
Define o modo de gravação para tabelas auxiliares criados durante a execução de teste. Consulte a descrição de tabelas auxiliares do [casos de teste em execução &#40; SybaseToSQL &#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) tópico.  
  
-   Se você selecionar **sempre salvar**, dados de tabela auxiliar sempre serão armazenados para uso posterior.  
  
-   Se você selecionar **salvar se houve falha na comparação de tabela**, dados de tabela auxiliar serão armazenados somente se ocorrer um erro.  
  
-   Se você selecionar **sempre excluir**, tabelas auxiliares sempre ser excluído após a execução de teste.  
  
-   Se você selecionar **peça ao usuário se a falha na comparação de tabela**, o usuário pode selecionar a ação necessária, se ocorrer um erro.  
  
Clique o **concluir** botão para salvar o caso de teste preparado em [repositórios de teste usando &#40; SybaseToSQL &#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Uso de repositórios de teste &#40; SybaseToSQL &#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[Executar casos de teste &#40; SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testando migrados objetos de banco de dados &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

