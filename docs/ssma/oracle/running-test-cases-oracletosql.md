---
title: Executar casos de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 537865967d0e43b7dd9501f9fbb7b9605f5b9367
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696745"
---
# <a name="running-test-cases-oracletosql"></a>Executar casos de teste (OracleToSQL)
Quando o SSMA testador executa um caso de teste, ele executa os objetos selecionados para teste e cria um relatório sobre os resultados da verificação. Se os resultados são idênticos em ambas as plataformas, o teste foi bem-sucedido. A correspondência de objetos entre Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é determinado de acordo com as configurações de mapeamento de esquema para o projeto atual do SSMA.  
  
Um requisito necessário para um teste bem-sucedido é que todos os objetos do Oracle são convertidos e carregados no banco de dados de destino. Além disso, os dados da tabela devem ser migrados para que o conteúdo das tabelas nas duas plataformas sejam sincronizado.  
  
## <a name="run-test-case"></a>Executar casos de teste  
Para executar o caso de teste preparado:  
  
1.  Clique o **executar** botão.  
  
2.  No **conectar-se ao Oracle** caixa de diálogo, insira as informações de conexão e, em seguida, clique em **Connect**.  
  
Quando o teste for concluído, o relatório de caso de teste é criado. Clique o **relatório** botão para exibir o [relatório de caso de teste](viewing-test-case-reports-oracletosql.md). O resultado do teste (relatório de casos de teste) é armazenado automaticamente na [repositório de resultados do teste](using-test-repositories-oracletosql.md) para uso posterior.  
  
## <a name="test-case-execution-steps"></a>Etapas de execução do caso de teste  
  
### <a name="prerequisites"></a>Prerequisites  
O SSMA testador verifica se todos os pré-requisitos foram atendidos para a execução de teste antes do início do teste. Se algumas condições não forem atendidas, uma mensagem de erro é exibida.  
  
### <a name="initialization"></a>Inicialização  
Nesta etapa, o testador SSMA cria auxiliares objetos (tabelas, gatilhos e exibições) no esquema SSMATESTER_ORACLE do servidor Oracle. Eles permitem que o controle de alterações feitas nos objetos afetados escolhidos para verificação.  
  
Suponha que a tabela verificada é denominada USER_TABLE. Para essa tabela, os seguintes objetos auxiliares são criados no Oracle.  
  
||||  
|-|-|-|  
|Nome|Tipo|Description|  
|USER_TABLE$ Trg|gatilho|Gatilho de auditoria de alterações na tabela verificada.|  
|USER_TABLE$ AUD|table|Tabela onde as linhas excluídas e substituídas são salvos.|  
|USER_TABLE$ AUDID|table|Tabela onde as linhas novas e alteradas são salvos.|  
|USER_TABLE|exibição|Representação simplificada de modificações de tabela.|  
|USER_TABLE$ NOVO|exibição|Representação simplificada de linhas inseridas e substituídas.|  
|USER_TABLE$ NEW_ID|exibição|Identificação de linhas inseridas e alteradas.|  
|USER_TABLE$ ANTIGO|exibição|Representação simplificada de linhas excluídas e substituídas.|  
  
O seguinte objeto é criado no esquema da tabela verificado na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
||||  
|-|-|-|  
|Nome|Tipo|Description|  
|USER_TABLE$ Trg|gatilho|Gatilho de auditoria de alterações na tabela verificada.|  
  
E os seguintes objetos são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no banco de dados ssmatesterdb.  
  
||||  
|-|-|-|  
|Nome|Tipo|Description|  
|USER_TABLE$ Aud|table|Tabela onde as linhas excluídas e substituídas são salvos.|  
|USER_TABLE$ AudID|table|Tabela onde as linhas novas e alteradas são salvos.|  
|USER_TABLE|exibição|Representação simplificada de modificações de tabela.|  
|USER_TABLE$ novo|exibição|Representação simplificada de linhas inseridas e substituídas.|  
|USER_TABLE$ new_id|exibição|Identificação de linhas inseridas e alteradas.|  
|USER_TABLE$ antigo|exibição|Representação simplificada de linhas excluídas e substituídas.|  
  
### <a name="test-object-calls"></a>Chamadas de objeto de teste  
Nesta etapa, o SSMA testador invoca cada objeto selecionado para o teste, compara os resultados e mostra o relatório.  
  
### <a name="finalization"></a>Finalização  
Durante a finalização SSMA testador limpa os objetos auxiliares criados na **inicialização** etapa.  
  
## <a name="next-step"></a>Próxima etapa  
[Exibir relatórios de caso de teste &#40;OracleToSQL&#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Selecionando e Configurando objetos a testar &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[Selecionar e configurar os objetos afetados pelo &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[Testar objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
