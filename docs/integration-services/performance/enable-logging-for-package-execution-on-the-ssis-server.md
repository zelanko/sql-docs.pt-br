---
title: "Habilitar o log para a execu&#231;&#227;o do pacote no servidor SSIS | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.SSIS.SSMS.ISMANAGECUSTOMIZEDLOGGINGLEVEL.F1"
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Habilitar o log para a execu&#231;&#227;o do pacote no servidor SSIS
  Este tópico descreve como definir ou alterar o nível de registro em log de um pacote quando você executa um pacote implantado no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O nível de registro em log que você define ao executar o pacote anula o registro em log do pacote configurado no momento do design no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Consulte [Habilitar o log de pacote no SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md) para obter mais informações.  
  
 Nas **Propriedades do Servidor** do SQL Server, na propriedade **Nível de registro em log do servidor**, você pode selecionar um nível de registro em log padrão para todo o servidor. Você pode escolher entre um dos níveis de registro em log internos descritos neste tópico, ou pode escolher um nível de registro em log personalizado existente. O nível de registro em log selecionado se aplica por padrão a todos os pacotes implantados no Catálogo do SSIS. Ele também se aplica por padrão a uma etapa de trabalho do SQL Agent, que executa um pacote do SSIS.  
  
 Você também pode especificar o nível de registro em log de um pacote individual usando um dos métodos a seguir. Este tópico aborda o primeiro método.  
  
-   Configuração de uma instância de uma execução de pacote usando a caixa de diálogo Executar Pacote  
  
-   Configuração de parâmetros para uma instância de uma execução usando o [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
-   Configuração de um trabalho do SQL Server Agent para uma execução de pacote usando a caixa de diálogo Nova Etapa de Trabalho.  
  
## Definir o nível de registro em log de um pacote usando a caixa de diálogo Executar Pacote  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], navegue até o pacote no Pesquisador de Objetos.  
  
2.  Clique com o botão direito do mouse no pacote e selecione **Executar**.  
  
3.  Selecione a guia **Avançado** na caixa de diálogo **Executar Pacote** .  
  
4.  Em **Nível de log**, selecione o nível de log. Este tópico contém uma descrição dos valores disponíveis.  
  
5.  Conclua qualquer outra configuração de pacote e clique em **OK** para executar o pacote.  
  
## Selecionar um nível de registro em log.  
 Os níveis de registro em log internos a seguir estão disponíveis. Você também pode selecionar um nível de registro em log existente personalizado. Este tópico contém uma descrição dos níveis de registro em log personalizados.  
  
|Nível de log|Description|  
|-------------------|-----------------|  
|Nenhum.|O log está desativado. Apenas o status da execução do pacote é registrado em log.|  
|Basic|Todos os eventos são registrados em log, menos personalizados e de diagnóstico. Este é o valor padrão.|  
|RuntimeLineage|Coleta os dados necessários para rastrear as informações de linhagem no fluxo de dados. Você pode analisar essas informações de linhagem para mapear o relacionamento de linhagem entre tarefas. ISVs e desenvolvedores podem compilar ferramentas de mapeamento de linhagem personalizadas com essas informações.|  
|Desempenho|Apenas estatísticas de desempenho e eventos OnError e OnWarning são registrados em log.<br /><br /> O relatório **Desempenho de Execução** mostra a hora ativa e o tempo total para os componentes de fluxo de dados do pacote. Estas informações estão disponíveis quando o nível de log da última execução do pacote foi definido como **desempenho** ou **detalhado**. Para saber mais, confira [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md).<br /><br /> A exibição [catalog.execution_component_phases](../../integration-services/system-views/catalog-execution-component-phases.md) mostra as horas de início e de término para os componentes de fluxo de dados, para cada fase de uma execução. Esta exibição mostra essas informações para esses componentes apenas quando o nível de log da execução do pacote é definido como **Desempenho** ou **Detalhado**.|  
|detalhado|Todos os eventos são registrados em log, inclusive eventos personalizados e de diagnóstico.<br /><br /> Eventos personalizados incluem os eventos registrados por tarefas do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para saber mais sobre eventos personalizados, confira [Custom Messages for Logging](../../integration-services/performance/custom-messages-for-logging.md).<br /><br /> Um exemplo de um evento de diagnóstico é o evento **DiagnosticEx** . Sempre que uma tarefa Executar Pacote executa um pacote filho, esse evento captura os valores de parâmetro passados para os pacotes filho.<br /><br /> O evento **DiagnosticEx** também ajuda você a obter os nomes das colunas nas quais ocorrem erros no nível da linha. Esse evento grava um mapa de linhagem de fluxo de dados no log. Em seguida, você pode procurar o nome da coluna nesse mapa de linhagem usando o identificador da coluna capturado por uma saída do erro.  Para obter mais informações, consulte [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md).<br /><br /> O valor da coluna de mensagem para **DiagnosticEx** é texto XML. Para exibir o texto da mensagem para uma execução de pacote, consulte a exibição [catalog.operation_messages &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md). Observe que o evento **DiagnosticEx** não preservar o espaço em branco em sua saída XML, a fim de reduzir o tamanho do log. Para melhorar a legibilidade, copie o log em um editor de XML, no Visual Studio, por exemplo, que ofereça suporte à formatação XML e ao realce de sintaxe.<br /><br /> A exibição [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) mostra uma linha cada vez que um componente de fluxo de dados envia dados a um componente downstream, para determinada execução do pacote. O nível de log deve ser definido como **Detalhado** para capturar essas informações na exibição.|  
  
## Criar e gerenciar níveis de registro em log personalizados usando a caixa de diálogo Gerenciamento de Nível de Registro em Log Personalizado  
 Você pode criar níveis de registro em log personalizados que coletam somente as estatísticas e eventos que você quiser. Opcionalmente, você também pode capturar o contexto de eventos, que inclui valores de variáveis, cadeias de conexão e propriedades do componente. Quando você executa um pacote, é possível selecionar um nível de registro em log personalizado sempre que você puder selecionar um nível de registro em log interno.  
  
> [!TIP]  
>  Para capturar os valores das variáveis do pacote, a propriedade **IncludeInDebugDump** das variáveis deve ser definida como **True**.  
  
1.  Para criar e gerenciar níveis de registro em log personalizados, no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no banco de dados SSISDB e selecione **Nível de Registro em Log Personalizado** para abrir a caixa de diálogo **Gerenciamento de Nível de Registro em Log Personalizado**. A lista **Níveis de Registro em Log Personalizados** contém todos os níveis de registro em log personalizados existentes.  
  
2.  Para **criar** um novo nível de registro em log personalizado, clique em **Criar**e forneça um nome e uma descrição. Nas guias **Estatísticas** e **Eventos** , selecione as estatísticas e eventos que você deseja coletar. Na guia **Eventos** , selecione opcionalmente **Incluir Contexto** para eventos individuais. Em seguida, clique em **Salvar**.  
  
3.  Para **atualizar** um nível de registro em log personalizado, selecione-o na lista, reconfigure-o e clique em **Salvar**.  
  
4.  Para **excluir** um nível de registro em log personalizado, selecione-o na lista e clique em **Excluir**.  
  
 **Permissões para níveis de registro em log personalizados.**  
  
-   Todos os usuários do banco de dados SSISDB podem ver os níveis de registro em log personalizados e selecionar um nível de registro em log personalizado ao executar pacotes.  
  
-   Somente os usuários na função ssis_admin ou sysadmin podem criar, atualizar ou excluir níveis de registro em log personalizados.  
  
## Consulte também  
 [Registro em Log do Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)   
 [Habilitar o log de pacote no SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)  
  
  