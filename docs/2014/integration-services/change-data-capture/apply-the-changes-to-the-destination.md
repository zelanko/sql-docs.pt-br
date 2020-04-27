---
title: Aplicar as alterações ao destino | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],applying changes
ms.assetid: 338a56db-cb14-4784-a692-468eabd30f41
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe555d94eb8e00cddd147c2424d0cf60e1d47b34
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771612"
---
# <a name="apply-the-changes-to-the-destination"></a>Aplicar as alterações no destino
  No fluxo de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que executa uma carga incremental de dados de alteração, a terceira e a última tarefa servem para aplicar as alterações no seu destino. Você precisará de um componente para aplicar inserções, um para aplicar atualizações e um para aplicar exclusões.  
  
> [!NOTE]  
>  A segunda tarefa no desenvolvimento do fluxo de dados de um pacote que realiza uma carga incremental de dados de alteração serve para separar inserções, atualizações e exclusões. Para obter mais informações sobre este componente, consulte [Processar inserções, atualizações e exclusões](process-inserts-updates-and-deletes.md). Para obter uma descrição do processo geral para criar um pacote que realiza uma carga incremental de dados de alteração, consulte [Change Data Capture &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="applying-inserts"></a>Aplicando inserções  
 Para aplicar inserções, você usa um destino OLE DB, pois as linhas novas não requerem nenhuma manipulação especial.  
  
#### <a name="to-process-inserts-by-using-an-ole-db-destination"></a>Para processar inserções usando um destino OLE DB  
  
1.  Na guia **Fluxo de Dados** , adicione um destino OLE DB.  
  
2.  Conecte a saída que contém inserções da transformação de Divisão Condicional para o destino de OLE DB.  
  
3.  No **Editor de Destino de OLE DB**, na página **Gerenciador de Conexões** , selecione as seguintes opções:  
  
    1.  Selecione ou crie um Gerenciador de Conexões de OLE DB para o banco de dados de destino.  
  
    2.  Selecione uma opção **Modo de acesso dos dados** e selecione a tabela de destino ou digite uma instrução SQL que contenha as colunas de destino.  
  
4.  Na página **Mapeamentos** do editor, mapeie as colunas apropriadas a partir dos dados de alteração para a tabela de destino.  
  
## <a name="applying-updates"></a>Aplicando atualizações  
 Para aplicar atualizações, você usa uma transformação de Comando do OLE DB. Você usa essa transformação porque tem que usar uma instrução UPDATE com parâmetros para atualizar uma linha por vez com novos valores de coluna.  
  
> [!NOTE]  
>  Também é possível usar componentes de destino para aplicar atualizações. Ao usar esse método, você usa os componentes de destino para salvar as linhas em tabelas temporárias criadas para essa finalidade. Em seguida, você usa tarefas Executar SQL para realizar operações de atualização em massa e exclusão em massa no destino a partir das tabelas temporárias.  
  
#### <a name="to-process-updates-by-using-an-ole-db-command-transformation"></a>Para processar atualizações usando uma transformação de Comando OLE DB  
  
1.  Na guia **Fluxo de Dados** , adicione uma transformação de Comando OLE DB.  
  
2.  Conecte a saída que contém atualizações a partir da transformação de Divisão Condicional para a transformação de Comando OLE DB.  
  
3.  Em **Editor Avançado para o Comando OLE DB**, no **Gerenciador de Conexões** selecione ou crie um gerenciador de conexões OLE DB para o banco de dados de destino.  
  
4.  No **Editor Avançado para o Comando OLE DB**, na guia **Propriedades do Componente** , para **SqlCommand**, digite uma instrução UPDATE com parâmetros.  
  
     Por exemplo, uma instrução UPDATE para uma tabela Cliente poderia ter a sintaxe seguinte:  
  
    ```  
    update CDCSample.Customer  
    set TerritoryID  = ?,  
        CustomerType  = ?,  
        rowguid  = ?,  
        ModifiedDate  = ?  
    where CustomerID = ?  
  
    ```  
  
5.  Na página **Mapeamentos de Coluna** do editor, mapeie as colunas apropriadas a partir dos dados de alteração até os parâmetros na instrução UPDATE.  
  
## <a name="applying-deletes"></a>Aplicando exclusões  
 Para aplicar exclusões, você usa uma transformação de Comando OLE DB. Você usa essa transformação porque tem que usar uma instrução DELETE com parâmetros para excluir uma única linha por vez com base no valor da coluna que identifica com exclusividade a linha.  
  
> [!NOTE]  
>  Também é possível usar componentes de destino para aplicar exclusões. Ao usar esse método, você usa os componentes de destino para salvar as linhas em tabelas temporárias criadas para essa finalidade. Em seguida, você usa tarefas Executar SQL para realizar operações de atualização em massa e exclusão em massa no destino a partir das tabelas temporárias.  
  
#### <a name="to-process-deletes-by-using-an-ole-db-command-transformation"></a>Para processar exclusões usando uma transformação de Comando OLE DB  
  
1.  Na guia **Fluxo de Dados** , adicione uma transformação de Comando OLE DB ao fluxo de dados.  
  
2.  Conecte a saída que contém exclusões a partir da transformação de Divisão Condicional para a transformação de Comando OLE DB.  
  
3.  Abra o Editor Avançado para configurar a transformação.  
  
4.  Em **Editor Avançado para o Comando OLE DB**, no **Gerenciador de Conexões** selecione ou crie um gerenciador de conexões OLE DB para o banco de dados de destino.  
  
5.  No **Editor Avançado para o Comando OLE DB**, na guia **Propriedades do Componente** do editor, para **SqlCommand**, digite uma instrução DELETE com parâmetros.  
  
     Por exemplo, uma instrução DELETE para uma tabela Cliente poderia ter a sintaxe seguinte:  
  
    ```  
    delete from Customer where CustomerID = ?  
  
    ```  
  
6.  Na guia **Mapeamentos de Coluna** do editor, mapeie a coluna apropriada a partir dos dados de alteração até o parâmetro na instrução DELETE.  
  
## <a name="optimizing-inserts-and-updates-by-using-merge-functionality"></a>Aperfeiçoando inserções e atualizações usando a funcionalidade MERGE  
 É possível otimizar o processamento de inserções e atualizações combinando determinadas opções de captura de dados de alteração com o uso da palavra-chave Transact-SQL MERGE. Para obter mais informações sobre a palavra-chave MERGE, consulte [MERGE &#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql).  
  
 Na instrução Transact-SQL que recupera os dados de alteração, é possível especificar *all with merge* como o valor do parâmetro *row_filter_option* ao chamar a função **cdc.fn_cdc_get_net_changes_<capture_instance>** . Essa função de captura de dados de alteração opera com mais eficiência quando não tem que realizar o processamento extra, necessário para distinguir inserções de atualizações. Ao especificar o valor do parâmetro *all with merge* , o valor de **__$operation** dos dados de alteração é 1 para exclusões ou 5 para alterações causadas por inserções ou atualizações. Para obter mais informações sobre a função Transact-SQL usada para recuperar os dados de alteração, consulte [Recuperar e compreender os dados de alteração](retrieve-and-understand-the-change-data.md). Após recuperar as alterações com o valor de parâmetro *all with merge* , é possível aplicar exclusões e enviar as linhas restantes para uma tabela temporária ou uma tabela de preparo. Em seguida, em uma tarefa Executar SQL de downstream, é possível usar uma única instrução MERGE para aplicar todas as inserções ou atualizações da tabela de preparo para o destino.  
  
  
