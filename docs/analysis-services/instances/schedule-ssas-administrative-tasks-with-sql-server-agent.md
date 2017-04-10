---
title: "Agendar tarefas administrativas do SSAS com o SQL Server Agent | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d1484b3-51d9-48a0-93d2-0c3e4ed22b87
caps.latest.revision: 12
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 12
---
# Agendar tarefas administrativas do SSAS com o SQL Server Agent
  Usando o serviço SQL Server Agent, você pode agendar tarefas administrativas do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para executar na ordem e nos horários em que você precisa. As tarefas agendadas ajudam a automatizar os processos que são executados em ciclos regulares ou previsíveis. Você pode agendar a execução de tarefas administrativas, como o processamento de cubos, nas horas de menor atividade comercial. Pode também estabelecer a ordem em que essas tarefas devem ser executadas criando etapas em um trabalho do SQL Server Agent. Por exemplo, é possível processar um cubo e, em seguida, fazer o backup do cubo.  
  
 Com etapas de trabalho, você tem controle sobre o fluxo de execução. Em caso de falha de um trabalho, é possível configurar o SQL Server Agent para continuar executando as demais tarefas ou interromper a execução. Você também pode configurar o SQL Server Agent para enviar notificações sobre o sucesso ou a falha da execução do trabalho.  
  
 Este tópico é um passo a passo que mostra dois modos de usar o SQL Server Agent para executar um script XMLA. O primeiro exemplo demonstra como agendar o processamento de uma única dimensão. O segundo exemplo mostra como combinar tarefas de processamento em um único script executado com base em uma agenda. Para concluir essas etapas, você precisará atender aos pré-requisitos a seguir.  
  
## Pré-requisitos  
 O serviço SQL Server Agent deve ser instalado.  
  
 Por padrão, os trabalhos são executados na conta de serviço. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], a conta padrão do SQL Server Agent é NT Service\SQLAgent$\<nome_da_instância>. Para executar um backup ou uma tarefa de processamento, essa conta deve ser um administrador do sistema na instância do Analysis Services. Para obter mais informações, consulte [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
 Você também deveria ter um banco de dados de teste. Você pode implantar o banco de dados de exemplo multidimensional do AdventureWorks ou um projeto do tutorial multidimensional do Analysis Services para usar neste passo a passo. Para obter mais informações, consulte [Install Sample Data and Projects for the Analysis Services Multidimensional Modeling Tutorial](../../analysis-services/install sample data and projects.md).  
  
## Exemplo 1: Processando uma dimensão em uma tarefa agendada  
 Este exemplo demonstra como criar e agendar um trabalho que processa uma dimensão.  
  
 Uma tarefa agendada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é um script XMLA inserido em um trabalho do SQL Server Agent. A execução desse trabalho é agendada para as horas e com a frequência desejadas. Como o SQL Server Agent faz parte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você trabalha com o Mecanismo de Banco de Dados e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para criar e agendar uma tarefa administrativa.  
  
###  <a name="bkmk_CreateScript"></a> Criar um script para processar uma dimensão em um trabalho do SQL Server Agent  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Abra uma pasta de banco de dados e localize uma dimensão. Clique com o botão direito do mouse na dimensão e selecione **Processar**.  
  
2.  Na caixa de diálogo **Processar Dimensão** , na coluna **Opções de Processo** na **Lista de objetos**, verifique se a opção dessa coluna é **Processar Completo**. Se essa opção não estiver selecionada, em **Opções de Processo**, clique na opção e selecione **Processar Completo** na lista suspensa.  
  
3.  Clique em **Script**.  
  
     Essa etapa abre a janela **Consulta XML** que contém o script XMLA que processa a dimensão.  
  
4.  Na caixa de diálogo **Processar Dimensão**, clique em **Cancelar** para fechar a caixa de diálogo.  
  
5.  Na janela **Consulta XMLA**, realce o script XMLA, clique com o botão direito do mouse no script realçado e selecione **Copiar**.  
  
     Essa etapa copia o script XMLA para a Área de Transferência do Windows. Você pode deixar o script XMLA na Área de Transferência ou colá-lo no Bloco de Notas ou em outro editor de texto. Este é um exemplo de script XMLA:  
  
    ```  
    <Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Account</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
###  <a name="bkmk_ProcessJob"></a> Criar e agendar o trabalho de processamento de dimensão  
  
1.  Conecte-se a uma instância do Mecanismo de Banco de Dados e abra o Pesquisador de Objetos.  
  
2.  Expanda o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse em **Trabalho** e selecione **Novo Trabalho**.  
  
4.  Na caixa de diálogo **Novo Trabalho**, digite um nome de trabalho em **Nome**.  
  
5.  Em **Selecionar uma página**, selecione **Etapas** e clique em **Novo**.  
  
6.  Na caixa de diálogo **Nova Etapa do Trabalho**, digite um nome de etapa em **Nome da Etapa**.  
  
7.  Em **Servidor**, digite **localhost** como instância padrão de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e **localhost\\**\<*nome da instância*> como instância nomeada.  
  
     Se você pretende executar o trabalho de um computador remoto, use o nome de servidor e nome de instância onde o trabalho será executado. Use o formato \<*nome do servidor*> para uma instância padrão e \<*nome do servidor*>\\<*nome de instância*> para uma instância nomeada.  
  
8.  Em **Tipo**, selecione **Comando do SQL Server Analysis Services**.  
  
9. Em **Comando**, clique com o botão direito do mouse e selecione **Colar**. O script XMLA gerado na etapa anterior deve aparecer na janela de comando.  
  
10. Clique em **OK**.  
  
11. Em **Selecionar uma página**, clique em **Agendas** e clique em **Novo**.  
  
12. Na caixa de diálogo **Nova Agenda de Trabalho**, digite um nome de agenda em **Nome** e clique em **OK**.  
  
     Essa etapa cria uma agenda para Domingo às 12:00 AM. A próxima etapa mostra como executar o trabalho manualmente. Você também pode especificar uma agenda que executará o trabalho durante o seu monitoramento.  
  
13. Na caixa de diálogo **Novo Trabalho**, clique em **OK**.  
  
14. No **Pesquisador de Objetos**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho criado e selecione **Iniciar Trabalho na Etapa**.  
  
     Como o trabalho tem apenas uma etapa, ele será executado imediatamente. Se o trabalho contiver mais de uma etapa, você poderá selecionar a etapa em que o trabalho deve iniciar.  
  
15. Quando o trabalho for concluído, clique em **Fechar**.  
  
## Exemplo 2: Processando uma dimensão e uma partição em lote em uma tarefa agendada  
 Os procedimentos deste exemplo demonstram como criar e agendar um trabalho que processa uma dimensão de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em lote e, ao mesmo tempo, processa uma partição de cubo que depende da dimensão para agregação. Para obter mais informações sobre processamento em lote de objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Processamento em lote &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md).  
  
###  <a name="bkmk_BatchProcess"></a> Criar um script para processamento de uma dimensão e uma partição em lote em um trabalho do SQL Server Agent  
  
1.  Usando o mesmo banco de dados, expanda **Dimensões**, clique com o botão direito do mouse na dimensão **Cliente** e selecione **Processo**.  
  
2.  Na caixa de diálogo **Processar Dimensão**, na coluna **Opções de Processo** da **Lista de objetos**, verifique se a opção dessa coluna é **Processar Completo**.  
  
3.  Clique em **Script**.  
  
     Essa etapa abre a janela **Consulta XML** que contém o script XMLA que processa a dimensão.  
  
4.  Na caixa de diálogo **Processar Dimensão**, clique em **Cancelar** para fechar a caixa de diálogo.  
  
5.  Expanda **Cubos**, **Adventure Works**, **Grupos de Medidas**, **Vendas pela Internet**, **Partições**, e clique com o botão direito do mouse na última partição da lista e selecione **Processar**.  
  
6.  Na caixa de diálogo **Processar Partição**, na coluna **Opções de Processo** da **Lista de objetos**, verifique se a opção dessa coluna é **Processar Completo**.  
  
7.  Clique em **Script**.  
  
     Essa etapa abre uma segunda janela **Consulta XML** que contém o script XMLA que processa a partição.  
  
8.  Na caixa de diálogo **Processar Partição**, clique em **Cancelar** para fechar o editor.  
  
     Neste ponto, você deve mesclar os dois scripts e assegurar que a dimensão seja processada primeiro.  
  
    > [!WARNING]  
    >  Se a partição for processada primeiro, o processamento da dimensão subsequente fará com que a partição se torne não processada. A partição exigiria um segundo processamento para atingir um estado processado.  
  
9. Na janela **Consulta XMLA** que contém o script XMLA que processa a partição, realce o código dentro das tags `Batch` e `Parallel`, clique com o botão direito do mouse no script e selecione **Copiar**.  
  
    ```  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID> Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
    ```  
  
10. Abra a janela **Consulta XMLA** que contém o script XMLA que processa a dimensão. Clique com o botão direito do mouse no script à esquerda da marca `</Process>` e selecione **Colar**.  
  
     O exemplo a seguir mostra o script XMLA revisado.  
  
    ```  
    <Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Customer</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
11. Realce o script XMLA revisado, clique com o botão direito do mouse no script realçado e selecione **Copiar.**  
  
12. Essa etapa copia o script XMLA para a Área de Transferência do Windows. Você pode deixar o script XMLA na Área de Transferência, salvá-lo em um arquivo ou colá-lo no Bloco de Notas ou em outro editor de texto.  
  
###  <a name="bkmk_Scheduling"></a> Criar e agendar o trabalho de processamento em lote  
  
1.  Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e abra o Pesquisador de Objetos.  
  
2.  Expanda o **SQL Server Agent**. Inicie o serviço caso ele ainda não esteja em execução.  
  
3.  Clique com o botão direito do mouse em **Trabalho** e selecione **Novo Trabalho**.  
  
4.  Na caixa de diálogo **Novo Trabalho**, digite um nome de trabalho em **Nome**.  
  
5.  Em **Etapas**, clique em **Nova**.  
  
6.  Na caixa de diálogo **Nova Etapa do Trabalho**, digite um nome de etapa em **Nome da Etapa**.  
  
7.  Em **Tipo**, selecione **Comando do SQL Server Analysis Services**.  
  
8.  Em **Executar como**, selecione a **Conta de Serviço do SQL Server Agent**. Lembre-se, a partir da seção Pré-requisitos, de que essa conta deve ter permissões administrativas no Analysis Services.  
  
9. Em **Servidor**, especifique o nome do servidor da instância do Analysis Services.  
  
10. Em **Comando**, clique com o botão direito do mouse e selecione **Colar**.  
  
11. Clique em **OK**.  
  
12. Na página **Agendas**, clique em **Nova**.  
  
13. Na caixa de diálogo **Nova Agenda de Trabalho**, digite um nome de agenda em **Nome** e clique em **OK**.  
  
     Essa etapa cria uma agenda para Domingo às 12:00 AM. A próxima etapa mostra como executar o trabalho manualmente. Você também pode selecionar uma agenda que executará o trabalho durante o seu monitoramento.  
  
14. Clique em **OK** para fechar a caixa de diálogo.  
  
15. No **Pesquisador de Objetos**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho criado e selecione **Iniciar Trabalho na Etapa**.  
  
     Como o trabalho tem apenas uma etapa, ele será executado imediatamente. Se o trabalho contiver mais de uma etapa, você poderá selecionar a etapa em que o trabalho deve iniciar.  
  
16. Quando o trabalho for concluído, clique em **Fechar**.  
  
## Consulte também  
 [Processando opções e configurações &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)   
 [Script de tarefas administrativas no Analysis Services](../../analysis-services/instances/script-administrative-tasks-in-analysis-services.md)  
  
  