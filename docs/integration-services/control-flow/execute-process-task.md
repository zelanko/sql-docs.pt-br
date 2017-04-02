---
title: "Tarefa Executar Processo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.executeprocesstask.f1"
helpviewer_keywords: 
  - "Tarefa Executar Processo [Integration Services]"
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
caps.latest.revision: 65
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 65
---
# Tarefa Executar Processo
  A tarefa Executar Processo executa um aplicativo ou arquivo de lote como parte de um fluxo de trabalho do pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Embora você possa usar a tarefa Executar Processo para abrir qualquer aplicativo padrão, como [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ou [!INCLUDE[ofprword](../../includes/ofprword-md.md)], você geralmente o utiliza para executar aplicativos de negócios ou arquivos de lote que trabalham em uma fonte de dados. Por exemplo, você pode usar a tarefa Executar Processo para expandir um arquivo de texto compactado. Depois, o pacote pode usar o arquivo de texto como uma fonte de dados para o fluxo de dados no pacote. Como outro exemplo, você pode usar a tarefa Executar Processo para executar um aplicativo [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] personalizado que gera um relatório de vendas diário. Em seguida, você pode anexar o relatório a uma tarefa Enviar Email e encaminhar o relatório para uma lista de distribuição.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui outras tarefas que realizam operações de fluxo de trabalho como executar pacotes. Para obter mais informações, consulte [Tarefa Executar Pacote](../../integration-services/control-flow/execute-package-task.md)  
  
## Entradas de log personalizadas disponíveis na tarefa Executar Processo  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Executar Processo. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md) e [Mensagens personalizadas para log](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|Fornece informações sobre o processo que a tarefa é configurada para executar.<br /><br /> São gravadas duas entradas de log. Uma contém informações sobre o nome e o local do executável que a tarefa executa e a outra registra a saída do executável.|  
|**ExecuteProcessVariableRouting**|Fornece informações sobre quais variáveis são encaminhadas para a entrada e as saídas do executável. As entradas de log são gravadas em stdin (a entrada), stdout (a saída) e stderr (a saída do erro).|  
  
## Configuração da Tarefa Executar Processo  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da Tarefa Executar Processo &#40;Página Geral&#41;](../../integration-services/control-flow/execute-process-task-editor-general-page.md)  
  
-   [Editor da Tarefa Executar Processo &#40;Página Processo&#41;](../../integration-services/control-flow/execute-process-task-editor-process-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
### Configurações de propriedades  
 Quando a tarefa Executar Processo executa um aplicativo personalizado, a tarefa fornece entrada para o aplicativo por meio de um ou de ambos estes métodos:  
  
-   Uma variável que você especifica na configuração da propriedade **StandardInputVariable**. Para obter mais informações sobre variáveis, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../Topic/Use%20Variables%20in%20Packages.md).  
  
-   Um argumento que você especifica na configuração de propriedade **Arguments**. Por exemplo, se a tarefa abrir um documento no Word, o argumento poderá nomear o arquivo .doc.  
  
 Para passar vários argumentos a um aplicativo personalizado em uma tarefa Executar Processo, use espaços para delimitar os argumentos. Um argumento não pode incluir um espaço; caso contrário, a tarefa não será executada. Você pode usar uma expressão para passar um valor variável como argumento. No exemplo a seguir, a expressão passa dois valores variáveis como argumentos e usa um espaço para delimitar os argumentos:  
  
 `@variable1 + " " + @variable2`  
  
 Você pode usar uma expressão para definir várias propriedades da tarefa Executar Processo.  
  
 Quando você usar a propriedade **StandardInputVariable** para configurar a tarefa Executar Processo para fornecer entrada, chame o método **Console.ReadLine** do aplicativo para ler a entrada. Para obter mais informações, consulte o tópico [Método Console.ReadLine](http://go.microsoft.com/fwlink/?LinkId=129201) na Biblioteca de Classes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
 Quando você usar a propriedade **Arguments** para configurar a tarefa Executar Processo para fornecer entrada, execute uma destas etapas para obter os argumentos:  
  
-   Se você usar Microsoft Visual Basic para escrever o aplicativo, defina a propriedade **My.Application.CommandLineArgs**. O exemplo a seguir define a propriedade **My.Application.CommandLineArgs** para recuperar dois argumentos:  
  
    ```  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     Para obter mais informações, consulte o tópico [Propriedade My.Application.CommandLineArgs](http://go.microsoft.com/fwlink/?LinkId=129200), na referência do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].  
  
-   Se você usar o Microsoft Visual C# para escrever o aplicativo, use o método **Main**.  
  
     Para obter mais informações, consulte o tópico [Argumentos de Linha de Comando (Guia de Programação C#)](http://go.microsoft.com/fwlink/?LinkId=129406), no Guia de Programação C#.  
  
 A tarefa Executar Processo também inclui as propriedades **StandardOutputVariable** e **StandardErrorVariable** para especificar as variáveis que consomem a saída padrão e a saída de erro do aplicativo, respectivamente.  
  
 Além disso, você pode configurar a tarefa Executar Processo para especificar um diretório de trabalho, um tempo-limite ou um valor para indicar que o executável foi executado com êxito. A tarefa também pode ser configurada para falhar se o código de retorno do executável não corresponder ao valor que indica êxito, ou se o executável não for encontrado no local especificado.  
  
## Configuração programática da Tarefa Executar Processo  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## Consulte também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  