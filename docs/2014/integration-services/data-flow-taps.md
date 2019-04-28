---
title: Toques de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 2d847adf-4b3d-4949-a195-ef43de275077
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 171bb649f5e4f91df947ed2a0a3113786755efe4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828646"
---
# <a name="data-flow-taps"></a>Toques de Fluxo de Dados
  O [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] introduz um novo recurso que permite adicionar um toque de dados em um caminho de fluxo de dados de um pacote em tempo de execução e direcionar a saída do toque de dados para um arquivo externo. Para usar esse recurso, você deverá implantar seu projeto SSIS usando o modelo de implantação de projeto em um servidor SSIS. Depois que você implantar o pacote no servidor, precisará executar scripts T-SQL no banco de dados SSISDB para adicionar toques de dados antes de executar o pacote. Aqui está um cenário de exemplo:  
  
1.  Crie uma instância de execução de um pacote usando o procedimento armazenado [catalog.create_execution &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database).  
  
2.  Adicione um toque de dados usando o procedimento armazenado [catalog.add_data_tap](/sql/integration-services/system-stored-procedures/catalog-add-data-tap) ou [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid).  
  
3.  Inicie a instância de execução do pacote usando [catalog.start_execution &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database).  
  
 Veja um script SQL de exemplo que executa as etapas descritas no cenário anterior:  
  
```  
  
Declare @execid bigint  
EXEC [SSISDB].[catalog].[create_execution] @folder_name=N'ETL Folder', @project_name=N'ETL Project', @package_name=N'Package.dtsx', @execution_id=@execid OUTPUT  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt'  
EXEC [SSISDB].[catalog].[start_execution] @execid  
  
```  
  
 O nome da pasta, o nome do projeto, os parâmetros do nome do pacote do procedimento armazenado create_execution correspondem à pasta, ao projeto e aos nomes de pacote no catálogo do Integration Services. Você pode obter os nomes de pasta, projeto e pacote para usar na chamada de create_execution do SQL Server Management Studio como mostra a imagem a seguir. Se você não vir o seu projeto SSIS agora, isso significará que ainda poderá não ter implantado o projeto no servidor SSIS. Clique com o botão direito do mouse no projeto SSIS no Visual Studio e clique em Implantar para implantar o projeto no servidor SSIS esperado.  
  
 Em vez de digitar as instruções SQL, é possível gerar o script de pacote de execução realizando as seguintes etapas:  
  
1.  Clique com o botão direito do mouse em **Package.dtsx** e clique em **Executar**.  
  
2.  Clique no botão da barra de ferramentas **Script** para gerar o script.  
  
3.  Agora, adicione a instrução add_data_tap antes da chamada start_execution.  
  
 O parâmetro task_package_path do procedimento armazenado add_data_tap corresponde à propriedade PackagePath da tarefa de fluxo de dados no Visual Studio. No Visual Studio, clique com o botão direito do mouse em **Tarefa Fluxo de Dados**e clique em **Propriedades** para iniciar a janela Propriedades.  Observe o valor da propriedade **PackagePath** para usá-la como um valor para o parâmetro task_package_path da chamada de procedimento armazenado add_data_tap.  
  
 O parâmetro dataflow_path_id_string do procedimento armazenado add_data_tap corresponde à propriedade IdentificationString do caminho de fluxo de dados ao qual você deseja adicionar um toque de dados. Para obter dataflow_path_id_string, clique no caminho de fluxo de dados (seta entre as tarefas no fluxo de dados) e observe o valor da propriedade **IdentificationString** na janela Propriedades.  
  
 Quando você executa o script, o arquivo de saída é armazenado em \<Program Files>\Microsoft SQL Server\110\DTS\DataDumps. Se um arquivo com o mesmo nome já existir, um novo arquivo com um sufixo (por exemplo: output[1].txt) será criado.  
  
 Como mencionado anteriormente, você também pode usar o procedimento armazenado [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid)em vez de usar o procedimento armazenado add_data_tap. Esse procedimento armazenado utiliza a ID da tarefa de fluxo de dados como um parâmetro em vez de task_package_path. Você pode obter a ID da tarefa de fluxo de dados da janela de propriedades no Visual Studio.  
  
## <a name="removing-a-data-tap"></a>Removendo um toque de dados  
 Você pode remover um toque de dados antes de iniciar a execução usando o procedimento armazenado [catalog.remove_data_tap](/sql/integration-services/system-stored-procedures/catalog-remove-data-tap) . Esse procedimento armazenado utiliza a ID do toque de dados como um parâmetro, que você pode obter como uma saída do procedimento armazenado add_data_tap.  
  
```  
  
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
  
```  
  
## <a name="listing-all-data-taps"></a>Listando todos os toques de dados  
 Você também pode listar todos os toques de dados usando a exibição de catalog.execution_data_taps. O exemplo a seguir extrai toques de dados para uma instância de execução da especificação (ID: 54).  
  
```  
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
## <a name="performance-consideration"></a>Considerações sobre o desempenho  
 Habilitar o nível de log detalhado e adicionar toques de dados aumenta as operações de E/S executadas por sua solução de integração de dados. Consequentemente, recomendamos que você adicione toques de dados somente para fins de solução de problemas  
  
## <a name="video"></a>Vídeo  
 Esse [vídeo no TechNet](https://technet.microsoft.com/sqlserver/dn600163) demonstra como adicionar/usar toques de dados no catálogo SSISDB do SQL Server 2012 que ajudam a depurar pacotes programaticamente e capturar resultados parciais em tempo de execução. Ele também discute como listar/remover esses toques de dados e as práticas recomendadas para usar os toque de dados em pacotes SSIS.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Depurando fluxo de dados](troubleshooting/debugging-data-flow.md)  
  
 [Ferramentas de solução de problemas de execução de pacote](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
