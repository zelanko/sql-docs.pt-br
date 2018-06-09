---
title: Executar casos de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 283dac366a8cfdf7e6fba39037a7c728945e0f67
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777902"
---
# <a name="running-test-cases-oracletosql"></a>Casos de teste em execução (OracleToSQL)
Quando o SSMA Tester executa um caso de teste, ele executa os objetos selecionados para teste e cria um relatório sobre os resultados da verificação. Se os resultados forem idênticos em ambas as plataformas, o teste foi bem-sucedido. A correspondência de objetos entre o Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é determinado de acordo com as configurações de mapeamento de esquema para o projeto atual do SSMA.  
  
Um requisito necessário para um teste bem-sucedido é que todos os objetos do Oracle são convertidos e carregados no banco de dados de destino. Além disso, os dados da tabela devem ser migrados para que o conteúdo das tabelas em ambas as plataformas sejam sincronizado.  
  
## <a name="run-test-case"></a>Execute o caso de teste  
Para executar o caso de teste preparada:  
  
1.  Clique o **executar** botão.  
  
2.  No **conectar-se ao Oracle** caixa de diálogo, insira as informações de conexão e, em seguida, clique em **conectar**.  
  
Quando o teste for concluído, o relatório de caso de teste é criado. Clique o **relatório** botão para exibir o [relatório casos de teste](http://msdn.microsoft.com/en-us/8da14323-9dd6-4019-bf79-3e8b972a9bc0). O resultado do teste (relatório de casos de teste) é armazenado automaticamente no [repositório de resultados de teste](http://msdn.microsoft.com/en-us/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4) para uso posterior.  
  
## <a name="test-case-execution-steps"></a>Etapas de execução do caso de teste  
  
### <a name="prerequisites"></a>Prerequisites  
O SSMA Tester verifica se todos os pré-requisitos são atendidos para a execução de teste antes do início do teste. Se algumas condições não forem atendidas, uma mensagem de erro é exibida.  
  
### <a name="initialization"></a>Inicialização  
Nesta etapa, o testador SSMA cria auxiliares objetos (tabelas, gatilhos e exibições) no esquema SSMATESTER_ORACLE do servidor Oracle. Elas permitem que as alterações de rastreamento feitas nos objetos afetados escolhidos para verificação.  
  
Suponha que a tabela verificada é denominada USER_TABLE. Para a tabela, os seguintes objetos auxiliares são criados no Oracle.  
  
||||  
|-|-|-|  
|Nome|Tipo|Description|  
|USER_TABLE$ Trg|gatilho|Gatilho auditando alterações na tabela verificada.|  
|USER_TABLE$ AUD|table|Tabela onde as linhas excluídas e substituídas são salvos.|  
|USER_TABLE$ AUDID|table|Tabela onde as linhas novas e alteradas são salvos.|  
|USER_TABLE|exibição|Representação simplificada de modificações de tabela.|  
|USER_TABLE$ NOVO|exibição|Representação simplificada das linhas inseridas e substituídas.|  
|USER_TABLE$ NEW_ID|exibição|Identificação de linhas inseridas e alteradas.|  
|USER_TABLE$ ANTIGO|exibição|Representação simplificada das linhas excluídas e substituídas.|  
  
O seguinte objeto é criado no esquema da tabela verificado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
||||  
|-|-|-|  
|Nome|Tipo|Description|  
|USER_TABLE$ Trg|gatilho|Gatilho auditando alterações na tabela verificada.|  
  
E os seguintes objetos são criados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]no banco de dados ssmatesterdb.  
  
||||  
|-|-|-|  
|Nome|Tipo|Description|  
|USER_TABLE$ Aud|table|Tabela onde as linhas excluídas e substituídas são salvos.|  
|USER_TABLE$ AudID|table|Tabela onde as linhas novas e alteradas são salvos.|  
|USER_TABLE|exibição|Representação simplificada de modificações de tabela.|  
|USER_TABLE$ novo|exibição|Representação simplificada das linhas inseridas e substituídas.|  
|USER_TABLE$ new_id|exibição|Identificação de linhas inseridas e alteradas.|  
|USER_TABLE$ antigo|exibição|Representação simplificada das linhas excluídas e substituídas.|  
  
### <a name="test-object-calls"></a>Chamadas de objeto de teste  
Nesta etapa, SSMA Tester invoca a cada objeto selecionado para o teste, compara os resultados e mostra o relatório.  
  
### <a name="finalization"></a>Finalização  
Durante a finalização SSMA Tester limpa os objetos auxiliares criados no **inicialização** etapa.  
  
## <a name="next-step"></a>Próxima etapa  
[Exibindo relatórios de caso de teste &#40;OracleToSQL&#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Selecionando e Configurando objetos para teste &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[Selecionar e configurar objetos afetados &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[Teste de objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
