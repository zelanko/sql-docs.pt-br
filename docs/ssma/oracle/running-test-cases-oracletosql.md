---
title: Executando casos de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 7905c76803bf637e581af934f473b070d44a6b09
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394855"
---
# <a name="running-test-cases-oracletosql"></a>Executar casos de teste (OracleToSQL)
Quando o SSMA Tester executa um caso de teste, ele executa os objetos selecionados para teste e cria um relatório sobre os resultados da verificação. Se os resultados forem idênticos em ambas as plataformas, o teste foi bem-sucedido. A correspondência de objetos entre o Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é determinada de acordo com as configurações de mapeamento de esquema para o projeto do SSMA atual.  
  
Um requisito necessário para um teste bem-sucedido é que todos os objetos Oracle são convertidos e carregados no banco de dados de destino. Além disso, os dados da tabela devem ser migrados para que o conteúdo das tabelas em ambas as plataformas seja sincronizado.  
  
## <a name="run-test-case"></a>Executar caso de teste  
Para executar o caso de teste preparado:  
  
1.  Clique no botão **Executar**.  
  
2.  Na caixa de diálogo **conectar ao Oracle** , insira as informações de conexão e, em seguida, clique em **conectar**.  
  
Quando o teste for concluído, o relatório de caso de teste será criado. Clique no botão **relatório** para exibir o [relatório de caso de teste](viewing-test-case-reports-oracletosql.md). O resultado do teste (relatório de caso de teste) é armazenado automaticamente no [repositório resultados de teste](using-test-repositories-oracletosql.md) para uso posterior.  
  
## <a name="test-case-execution-steps"></a>Etapas de execução de caso de teste  
  
### <a name="prerequisites"></a>Pré-requisitos  
O SSMA Tester verifica se todos os pré-requisitos foram atendidos para a execução de teste antes do início do teste. Se algumas condições não forem satisfeitas, uma mensagem de erro será exibida.  
  
### <a name="initialization"></a>Inicialização  
Nesta etapa, o SSMA Tester cria objetos auxiliares (tabelas, gatilhos e exibições) no esquema de SSMATESTER_ORACLE do servidor Oracle. Eles permitem o rastreamento de alterações feitas nos objetos afetados escolhidos para verificação.  
  
Suponha que a tabela verificada seja nomeada USER_TABLE. Para essa tabela, os seguintes objetos auxiliares são criados no Oracle.  
  
|Nome|Tipo|Descrição|  
|-|-|-|  
|USER_TABLE $ trg|gatilho|Disparar a auditoria das alterações na tabela verificada.|  
|USER_TABLE $ AUD|tabela|Tabela na qual as linhas excluídas e substituídas são salvas.|  
|USER_TABLE $ AUDID|tabela|Tabela na qual as linhas novas e alteradas são salvas.|  
|USER_TABLE|exibição|Representação simplificada das modificações da tabela.|  
|USER_TABLE $ NEW|exibição|Representação simplificada de linhas inseridas e substituídas.|  
|USER_TABLE $ NEW_ID|exibição|Identificação de linhas inseridas e alteradas.|  
|USER_TABLE $ OLD|exibição|Representação simplificada de linhas excluídas e substituídas.|  
  
O objeto a seguir é criado no esquema da tabela verificada em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Nome|Tipo|Descrição|  
|-|-|-|  
|USER_TABLE $ trg|gatilho|Disparar a auditoria das alterações na tabela verificada.|  
  
E os seguintes objetos são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados ssmatesterdb.  
  
|Nome|Tipo|Descrição|  
|-|-|-|  
|USER_TABLE $ AUD|tabela|Tabela na qual as linhas excluídas e substituídas são salvas.|  
|USER_TABLE $ AudID|tabela|Tabela na qual as linhas novas e alteradas são salvas.|  
|USER_TABLE|exibição|Representação simplificada das modificações da tabela.|  
|USER_TABLE $ New|exibição|Representação simplificada de linhas inseridas e substituídas.|  
|USER_TABLE $ new_id|exibição|Identificação de linhas inseridas e alteradas.|  
|USER_TABLE $ Old|exibição|Representação simplificada de linhas excluídas e substituídas.|  
  
### <a name="test-object-calls"></a>Testar chamadas de objeto  
Nesta etapa, o SSMA Tester invoca cada objeto selecionado para o teste, compara os resultados e mostra o relatório.  
  
### <a name="finalization"></a>Finalização  
Durante a finalização, o testador do SSMA limpa os objetos auxiliares criados na etapa de **inicialização** .  
  
## <a name="next-step"></a>Próxima etapa  
[Exibindo relatórios de caso de teste &#40;OracleToSQL&#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Selecionando e configurando objetos para testar &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[Selecionando e configurando objetos afetados &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[Testando objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
