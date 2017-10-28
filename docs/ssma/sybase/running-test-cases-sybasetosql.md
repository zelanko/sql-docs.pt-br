---
title: Executar casos de teste (SybaseToSQL) | Microsoft Docs
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
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 80c335253aef5dd676ece990cb34feb5d67da829
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="running-test-cases-sybasetosql"></a>Casos de teste em execução (SybaseToSQL)
Quando o SSMA Tester executa um caso de teste, ele executa os objetos selecionados para teste e cria um relatório sobre os resultados da verificação. Se os resultados forem idênticos em ambas as plataformas, o teste foi bem-sucedido. A correspondência de objetos entre Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é determinado de acordo com as configurações de mapeamento de esquema para o projeto atual do SSMA.  
  
Um requisito necessário para um teste bem-sucedido é que todos os objetos do Sybase são convertidos e carregados no banco de dados de destino. Além disso, os dados da tabela devem ser migrados para que o conteúdo das tabelas em ambas as plataformas sejam sincronizado.  
  
## <a name="run-test-case"></a>Execute o caso de teste  
Para executar o caso de teste preparada:  
  
1.  Clique o **executar** botão.  
  
2.  No **conectar-se ao Sybase** caixa de diálogo, insira as informações de conexão e, em seguida, clique em **conectar**.  
  
Quando o teste for concluído, o relatório de caso de teste é criado. Clique o **relatório** botão para exibir o [exibindo relatórios de caso de teste &#40; SybaseToSQL &#41; ](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md). O resultado do teste (relatório de casos de teste) é armazenado automaticamente no [usando repositórios de teste &#40; SybaseToSQL &#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md) para uso posterior.  
  
## <a name="test-case-execution-steps"></a>Etapas de execução do caso de teste  
  
### <a name="prerequisites"></a>Pré-requisitos  
O SSMA Tester verifica se todos os pré-requisitos são atendidos para a execução de teste antes do início do teste. Se algumas condições não forem atendidas, uma mensagem de erro é exibida.  
  
### <a name="initialization"></a>Inicialização  
Nesta etapa, SSMA Tester cria auxiliares objetos (tabelas, gatilhos e exibições) no Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Elas permitem que as alterações de rastreamento feitas nas tabelas afetadas escolhidas para verificar se o modo de comparações de tabela é **altera somente**.  
  
Suponha que a tabela verificada é denominada USER_TABLE. Para a tabela, os seguintes objetos auxiliares são criados no Sybase.  
  
Os seguintes objetos são criados no Sybase no banco de dados SSMATESTER2005db ou SSMATESTER2008db e em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no banco de dados ssmatesterdb_syb.  
  
|Nome|Tipo|Description|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|Gatilho|Gatilho auditando alterações na tabela verificada.|  
|USER_TABLE$ Aud|Table|Tabela onde as linhas excluídas e substituídas são salvos.|  
|USER_TABLE$ AudID|Table|Tabela onde as linhas novas e alteradas são salvos.|  
|USER_TABLE|Exibição|Representação simplificada de modificações de tabela.|  
|USER_TABLE$ novo|Exibição|Representação simplificada das linhas inseridas e substituídas.|  
|USER_TABLE$ new_id|Exibição|Identificação de linhas inseridas e alteradas.|  
|USER_TABLE$ antigo|Exibição|Representação simplificada das linhas excluídas e substituídas.|  
  
O objeto a seguir é criado no banco de dados da tabela verificado no Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
|Nome|Tipo|Description|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|Gatilho|Gatilho auditando alterações na tabela verificada.|  
  
### <a name="test-object-calls"></a>Chamadas de objeto de teste  
Nesta etapa, SSMA Tester invoca a cada objeto selecionado para o teste, compara os resultados e mostra o relatório.  
  
### <a name="finalization"></a>Finalização  
Durante a finalização SSMA Tester limpa os objetos auxiliares criados no **inicialização** etapa.  
  
## <a name="next-step"></a>Próxima etapa  
[Exibindo relatórios de caso de teste &#40; SybaseToSQL &#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Selecionando e Configurando objetos para teste &#40; SybaseToSQL &#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[Selecionar e configurar os objetos afetados &#40; SybaseToSQL &#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[Testando migrados objetos de banco de dados &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

