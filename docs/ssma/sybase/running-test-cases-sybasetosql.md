---
description: Executar casos de teste (SybaseToSQL)
title: Executando casos de teste (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: ea2b250f59a29a16bc77ad23e28b0823461a8ace
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468747"
---
# <a name="running-test-cases-sybasetosql"></a>Executar casos de teste (SybaseToSQL)
Quando o SSMA Tester executa um caso de teste, ele executa os objetos selecionados para teste e cria um relatório sobre os resultados da verificação. Se os resultados forem idênticos em ambas as plataformas, o teste foi bem-sucedido. A correspondência de objetos entre o Sybase e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é determinada de acordo com as configurações de mapeamento de esquema para o projeto do SSMA atual.  
  
Um requisito necessário para um teste bem-sucedido é que todos os objetos Sybase são convertidos e carregados no banco de dados de destino. Além disso, os dados da tabela devem ser migrados para que o conteúdo das tabelas em ambas as plataformas seja sincronizado.  
  
## <a name="run-test-case"></a>Executar caso de teste  
Para executar o caso de teste preparado:  
  
1.  Clique no botão **Executar**.  
  
2.  Na caixa de diálogo **conectar ao Sybase** , insira as informações de conexão e, em seguida, clique em **conectar**.  
  
Quando o teste for concluído, o relatório de caso de teste será criado. Clique no botão **relatório** para exibir os [relatórios de caso de teste de exibição &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md). O resultado do teste (relatório de caso de teste) é armazenado automaticamente nos [repositórios de teste do Using &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md) para uso posterior.  
  
## <a name="test-case-execution-steps"></a>Etapas de execução de caso de teste  
  
### <a name="prerequisites"></a>Pré-requisitos  
O SSMA Tester verifica se todos os pré-requisitos foram atendidos para a execução de teste antes do início do teste. Se algumas condições não forem satisfeitas, uma mensagem de erro será exibida.  
  
### <a name="initialization"></a>Inicialização  
Nesta etapa, o SSMA Tester cria objetos auxiliares (tabelas, gatilhos e exibições) no Sybase e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Eles permitem que as alterações de rastreamento feitas nas tabelas afetadas escolhidas para verificação se o modo de comparações de tabela são **apenas alterações**.  
  
Suponha que a tabela verificada seja nomeada USER_TABLE. Para essa tabela, os seguintes objetos auxiliares são criados no Sybase.  
  
Os seguintes objetos são criados em Sybase no banco de dados SSMATESTER2005db ou SSMATESTER2008db e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados ssmatesterdb_syb.  
  
|Nome|Type|Descrição|  
|--------|--------|---------------|  
|USER_TABLE $ trg|Gatilho|Disparar a auditoria das alterações na tabela verificada.|  
|USER_TABLE $ AUD|Tabela|Tabela na qual as linhas excluídas e substituídas são salvas.|  
|USER_TABLE $ AudID|Tabela|Tabela na qual as linhas novas e alteradas são salvas.|  
|USER_TABLE|Exibir|Representação simplificada das modificações da tabela.|  
|USER_TABLE $ New|Exibir|Representação simplificada de linhas inseridas e substituídas.|  
|USER_TABLE $ new_id|Exibir|Identificação de linhas inseridas e alteradas.|  
|USER_TABLE $ Old|Exibir|Representação simplificada de linhas excluídas e substituídas.|  
  
O objeto a seguir é criado no banco de dados da tabela verificada no Sybase e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Nome|Type|Descrição|  
|--------|--------|---------------|  
|USER_TABLE $ trg|Gatilho|Disparar a auditoria das alterações na tabela verificada.|  
  
### <a name="test-object-calls"></a>Testar chamadas de objeto  
Nesta etapa, o SSMA Tester invoca cada objeto selecionado para o teste, compara os resultados e mostra o relatório.  
  
### <a name="finalization"></a>Finalização  
Durante a finalização, o testador do SSMA limpa os objetos auxiliares criados na etapa de **inicialização** .  
  
## <a name="next-step"></a>Próxima etapa  
[Exibindo relatórios de caso de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Selecionando e configurando objetos para testar &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[Selecionando e configurando objetos afetados &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[Testando objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
