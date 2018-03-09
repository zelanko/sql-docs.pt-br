---
title: Depurando o fluxo de dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3491077486daf90c414a00eec3d382ae1537284a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="debugging-data-flow"></a>Depurando fluxo de dados
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e o Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] incluem recursos e ferramentas que você pode usar para solucionar problemas de fluxos de dados em um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] O Designer fornece visualizadores de dados.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] O Designer e as transformações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornecem contagens de linha.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece relatórios de progresso em tempo de execução.  
  
## <a name="data-viewers"></a>Visualizadores de dados  
 Os visualizadores de dados exibem dados entre dois componentes em um fluxo de dados. Os visualizadores de dados podem exibir dados quando os dados são extraídos de uma fonte de dados e entram primeiro um fluxo de dados, antes e depois de uma transformação atualizar os dados, e antes dos dados serem carregados em seu destino.  
  
 Para visualizar os dados, você anexa os visualizadores de dados ao caminho que conecta dois componentes de fluxo de dados. A habilidade de visualizar os dados entre componentes de fluxo de dados, facilita a identificação de valores de dados inesperados, a visualização de como uma transformação altera os valores das colunas, e a descoberta da razão pela qual uma transformação falha. Por exemplo, você pode descobrir uma falha na pesquisa em uma tabela de referência e, para corrigir isso, você pode desejar adicionar uma transformação que forneça dados padrão para colunas em branco.  
  
 Um visualizador de dados pode exibir dados em uma grade. Ao usar uma grade, você seleciona as colunas a serem exibidas. Os valores das colunas selecionadas são exibidos em um formato tabular.  
  
 Você também pode incluir vários visualizadores de dados em um caminho. Você pode exibir os mesmos dados em diferentes formatos, por exemplo, criar uma exibição de gráfico e uma exibição de grade dos dados, ou criar visualizadores de dados para diferentes colunas de dados.  
  
 Quando você adiciona um visualizador de dados a um caminho, o Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] adiciona um ícone de visualização de dados à superfície de design da guia **Fluxo de Dados** , ao lado do caminho. As transformações que podem tem múltiplas saídas, tais como as transformações Divisão Condicional, podem incluir um visualizador em cada caminho.  
  
 Em tempo de execução, uma janela **Visualizador de Dados** é aberta e exibe as informações especificadas pelo formato do visualizador de dados. Por exemplo, um visualizador de dados que utiliza o formato de grade exibe os dados das colunas selecionadas, o número de linhas de saída transmitidas ao componente de fluxo de dados e o número de linhas exibidas. As informações exibem buffer por buffer e, dependendo da largura das linhas no fluxo de dados, um buffer pode conter mais ou menos linhas.  
  
 Na caixa de diálogo **Visualizador de Dados** , você pode copiar os dados para a Área de Transferência, limpar todos os dados da tabela, configurar novamente o visualizador de dados, retomar o fluxo de dados e desanexar ou anexar o visualizador de dados.  
  
#### <a name="to-add-a-data-viewer"></a>Para adicionar um visualizador de dados  
  
-   [Adicionar um visualizador de dados a um fluxo de dados](#add_viewer)  
  
## <a name="row-counts"></a>Contagens de linhas  
 O número de linhas que passaram por um caminho é exibido na superfície de design da guia **Fluxo de Dados** no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , ao lado do caminho. O número é atualizado periodicamente enquanto os dados se movimentam pelo caminho.  
  
 Você também pode adicionar uma transformação Contagem de Linhas ao fluxo de dados para capturar a contagem final de linhas em uma variável. Para obter mais informações, consulte [Row Count Transformation](../../integration-services/data-flow/transformations/row-count-transformation.md).  
  
## <a name="progress-reporting"></a>Relatório de progresso  
 Quando você executa um pacote, o Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] descreve o progresso na superfície de design da guia **Fluxo de Dados** , exibindo cada componente de fluxo de dados em uma cor que indica seu status. Quando cada componente começa a executar sua função, ele muda para a cor amarelo, e quando ele termina com sucesso, sua cor muda para verde. A cor vermelha indica que o componente falhou.  
  
 A tabela a seguir descreve a codificação de cores.  
  
|Color|Description|  
|-----------|-----------------|  
|Nenhuma cor|Esperando ser chamado pelo mecanismo de fluxo de dados.|  
|Amarelo|Executando uma transformação, extraindo dados ou carregando dados.|  
|Verde|Executado com êxito.|  
|vermelha|Executado com erros.|  

## <a name="analysis-of-data-flow"></a>Análise do Fluxo de Dados
  Você pode usar a exibição [execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) **SSISDB** database view to analyze the data flow of packages. Esta exibição exibe uma linha a cada vez que um componente de fluxo de dados envia dados a um componente downstream. As informações podem ser usadas para obter um entendimento mais profundo das linhas que são enviadas para cada componente.  
  
> [!NOTE]  
>  O nível de log deve ser definido para **Detalhado** para capturar as informações com a exibição de catalog.execution_data_statistics.  
  
 O exemplo a seguir exibe o número de linhas enviadas entre componentes de um pacote.  
  
```sql
use SSISDB  
select package_name, task_name, source_component_name, destination_component_name, rows_sent  
from catalog.execution_data_statistics  
where execution_id = 132  
order by source_component_name, destination_component_name   
```  
  
 O exemplo a seguir calcula o número de linhas por milissegundo enviadas por cada componente para uma execução específica. Os valores calculados são:  
  
-   **total_rows** – a soma de todas as linhas enviadas pelo componente  
  
-   **wall_clock_time_ms** – o tempo de execução decorrido total, em milissegundos, para cada componente  
  
-   **num_rows_per_millisecond** – o número de linhas por milissegundo enviadas por cada componente  
  
 A cláusula **HAVING** é usada para impedir um erro de divisão por zero nos cálculos.  
  
```sql  
use SSISDB  
select source_component_name, destination_component_name,  
    sum(rows_sent) as total_rows,  
    DATEDIFF(ms,min(created_time),max(created_time)) as wall_clock_time_ms,  
    ((0.0+sum(rows_sent)) / (datediff(ms,min(created_time),max(created_time)))) as [num_rows_per_millisecond]  
from [catalog].[execution_data_statistics]  
where execution_id = 132  
group by source_component_name, destination_component_name  
having (datediff(ms,min(created_time),max(created_time))) > 0  
order by source_component_name desc  
```  

## <a name="configure-an-error-output-in-a-data-flow-component"></a>Configurar uma saída de erro em um componente de fluxo de dados
  Muitos componentes de fluxo de dados dão suporte a saídas de erro e, dependendo do componente, o [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer fornece diferentes modos de configurar uma saída de erro. Além de configurar uma saída de erro, você pode configurar também as colunas de uma saída de erro. Isto inclui a configuração das colunas **ErrorCode** e **ErrorColumn** que são adicionadas pelo componente.  
  
### <a name="configuring-an-error-output"></a>Configurando uma saída de erro  
 Para configurar uma saída de erro, você tem duas opções:  
  
-   Use a caixa de diálogo **Configurar Saída de Erro** . Você pode usar esta caixa de diálogo para configurar uma saída de erro em qualquer componente de fluxo de dados que ofereça suporte a saídas de erro.  
  
-   Use a caixa de diálogo do editor para o componente. Alguns componentes permitem que você configure saídas de erro diretamente na caixa de diálogo do editor. Entretanto, você não pode configurar saídas de erros da caixa de diálogo do editor para a origem do ADO NET, a transformação de Importar Coluna e do Comando OLE DB ou para o destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Os procedimentos a seguir descrevem como usar estas caixas de diálogo para configurar saídas de erro.  
  
#### <a name="to-configure-an-error-output-using-the-configure-error-output-dialog-box"></a>Para configurar uma saída de erro que usa a caixa de diálogo Configurar Saída de Erro  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique na guia **Fluxo de Dados** .  
  
4.  Arraste a saída de erro, representada pela seta vermelha, do componente que é a fonte dos erros para outro componente no fluxo de dados.  
  
5.  Na caixa de diálogo **Configurar Saída de Erro** , selecione uma ação nas colunas **Erro** e **Truncamento** para cada coluna da entrada de componente.  
  
6.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
#### <a name="to-add-an-error-output-using-the-editor-dialog-box-for-the-component"></a>Para adicionar uma saída de erro que usa a caixa de diálogo do editor para o componente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique na guia **Fluxo de Dados** .  
  
4.  Clique duas vezes nos componentes de fluxo de dados em que você deseja configurar uma saída de erro e, dependendo do componente, siga uma destas etapas:  
  
    -   Clique em **Configurar Saída de Erro**.  
  
    -   Clique em **Saída de Erro**.  
  
5.  Defina a opção **Erro** para cada coluna.  
  
6.  Defina a opção **Truncamento** para cada coluna.  
  
7.  Clique em **OK**.  
  
8.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
### <a name="configuring-error-output-columns"></a>Configurando colunas de saída de erro  
 Para configurar colunas de saída de erro, você deve usar a guia **Propriedades de Entrada e Saída** na caixa de diálogo **Editor Avançado** .  
  
#### <a name="to-configure-error-output-columns"></a>Para configurar colunas de saída de erro  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique na guia **Fluxo de Dados** .  
  
4.  Clique com o botão direito do mouse no componente cujas colunas de saída de erro você deseja configurar e clique em **Mostrar Editor Avançado**.  
  
5.  Clique na guia **Propriedades de Entrada e Saída** e expanda **Saída de Erro do \<component name>** e, em seguida, expanda **Colunas de Saída**.  
  
6.  Clique em uma coluna e atualize suas propriedades.  
  
    > [!NOTE]  
    >  A lista de colunas inclui as colunas na entrada do componente, as colunas **ErrorCode** e **ErrorColumn** adicionadas pelas saídas de erros anteriores e as colunas **ErrorCode** e **ErrorColumn** adicionadas por este componente.  
  
7.  Clique em **OK.**  
  
8.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  

## <a name="add_viewer"></a> Adicionar um visualizador de dados a um fluxo de dados
  Este tópico descreve como adicionar e configurar um visualizador de dados em um fluxo de dados. Um visualizador de dados exibe dados que estão se movendo entre dois componentes de fluxo de dados. Por exemplo, um visualizador de dados pode exibir os dados extraídos de uma fonte antes de uma transformação no fluxo de dados modificar os dados.  
  
 Um caminho conecta componentes em um fluxo de dados conectando a saída de um componente de fluxo de dados à entrada de outro componente.  
  
 Antes de adicionar visualizadores de dados, um pacote deve incluir uma tarefa Fluxo de Dados e pelo menos dois componentes de fluxo de dados que estejam conectados.  
  
 Adicione um visualizador de dados a uma saída de erro para ver a descrição do erro e o nome da coluna na qual ocorreu o erro. Por padrão, a saída de erro inclui somente identificadores numéricos para o erro e a coluna.  
  
### <a name="to-add-a-data-viewer-to-a-data-flow"></a>Para adicionar um visualizador de dados a um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** , se ainda não estiver ativada.  
  
4.  Clique na tarefa Fluxo de Dados do fluxo de dados ao qual você deseja conectar um visualizador de dados e, em seguida, clique na guia **Fluxo de Dados** .  
  
5.  Clique com o botão direito do mouse em um caminho entre dois componentes de fluxo de dados e clique em **Editar**.  
  
6.  Na página **Geral** , você pode exibir e editar propriedades do caminho. Por exemplo, na lista suspensa **PathAnnotation** , você pode selecionar a anotação que aparece ao lado do caminho.  
  
7.  Na página **Metadados** , você pode exibir os metadados da coluna e copiar os metadados na Área de Transferência.  
  
8.  Na página **Visualizador de Dados** , clique em **Habilitar visualizador de dados**.  
  
9. Na área Colunas para exibição, selecione as colunas a serem exibidas no visualizador de dados. Por padrão, todas as colunas disponíveis são selecionadas e relacionadas na lista **Colunas Exibidas** . Mova as colunas que não deseja usar para a lista **Coluna Não Usada** selecionando-as e clicando na seta para a esquerda.  
  
    > [!NOTE]  
    >  Na grade, os valores que representam os tipos de dados DT_DATE, DT_DBTIME2, DT_FILETIME, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET aparecem como cadeias de caracteres formatadas conforme o ISO 8601 e um separador de espaço substitui o separador **T** . Os valores que representam os tipos de dados DT_DATE e DT_FILETIME incluem sete dígitos para os segundos fracionários. Como o tipo de dados DT_FILETIME armazena somente três dígitos de segundos fracionários, a grade exibe zeros nos quatro dígitos restantes. Os valores que representam o tipo de dados DT_DBTIMESTAMP incluem três dígitos para os segundos fracionários. Para os valores que representam os tipos de dados DT_DBTIME2, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET, o número de dígitos para os segundos fracionários corresponde à escala especificada para o tipo de dados da coluna. Para obter mais informações sobre os formatos ISO 8601, consulte [Formatos de data e hora](http://msdn.microsoft.com/library/bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39). Para obter mais informações sobre tipos de dados, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
10. Clique em **OK**.  

## <a name="data-flow-taps"></a>Toques de Fluxo de Dados
 É possível adicionar um toque de dados em um caminho de fluxo de dados de um pacote em tempo de execução e direcionar a saída do toque de dados para um arquivo externo. Para usar esse recurso, você deverá implantar seu projeto SSIS usando o modelo de implantação de projeto em um servidor SSIS. Depois que você implantar o pacote no servidor, precisará executar scripts T-SQL no banco de dados SSISDB para adicionar toques de dados antes de executar o pacote. Aqui está um cenário de exemplo:  
  
1.  Crie uma instância de execução de um pacote usando o procedimento armazenado [catalog.create_execution &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
2.  Adicione um toque de dados usando o procedimento armazenado [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md) ou [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md).  
  
3.  Inicie a instância de execução do pacote usando [catalog.start_execution &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).  
  
 Veja um script SQL de exemplo que executa as etapas descritas no cenário anterior:  
  
```sql
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
  
 Como mencionado anteriormente, você também pode usar o procedimento armazenado [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)em vez de usar o procedimento armazenado add_data_tap. Esse procedimento armazenado utiliza a ID da tarefa de fluxo de dados como um parâmetro em vez de task_package_path. Você pode obter a ID da tarefa de fluxo de dados da janela de propriedades no Visual Studio.  
  
### <a name="removing-a-data-tap"></a>Removendo um toque de dados  
 Você pode remover um toque de dados antes de iniciar a execução usando o procedimento armazenado [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md) . Esse procedimento armazenado utiliza a ID do toque de dados como um parâmetro, que você pode obter como uma saída do procedimento armazenado add_data_tap.  
  
```sql
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
```  
  
### <a name="listing-all-data-taps"></a>Listando todos os toques de dados  
 Você também pode listar todos os toques de dados usando a exibição de catalog.execution_data_taps. O exemplo a seguir extrai toques de dados para uma instância de execução da especificação (ID: 54).  
  
```sql 
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
### <a name="performance-consideration"></a>Considerações sobre o desempenho  
 Habilitar o nível de log detalhado e adicionar toques de dados aumenta as operações de E/S executadas por sua solução de integração de dados. Consequentemente, recomendamos que você adicione toques de dados somente para fins de solução de problemas  
  
### <a name="video"></a>Vídeo  
 Esse [vídeo no TechNet](http://technet.microsoft.com/sqlserver/dn600163) demonstra como adicionar/usar toques de dados no catálogo SSISDB do SQL Server 2012 que ajudam a depurar pacotes programaticamente e capturar resultados parciais em tempo de execução. Ele também discute como listar/remover esses toques de dados e as práticas recomendadas para usar os toque de dados em pacotes SSIS.  
 
## <a name="see-also"></a>Consulte Também  
 [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
  
