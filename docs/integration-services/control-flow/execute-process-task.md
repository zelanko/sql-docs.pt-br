---
title: Tarefa executar processo | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.executeprocesstask.f1
- sql13.dts.designer.executeprocesstask.general.f1
- sql13.dts.designer.executeprocesstask.process.f1
helpviewer_keywords:
- Execute Process task [Integration Services]
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
caps.latest.revision: 65
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: e9b4a89e32139f359e049f1f9d3e46d5b27696b1
ms.contentlocale: pt-br
ms.lasthandoff: 08/11/2017

---
# <a name="execute-process-task"></a>Tarefa Executar Processo
  A tarefa Executar Processo executa um aplicativo ou arquivo de lote como parte de um fluxo de trabalho do pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Embora você possa usar a tarefa Executar Processo para abrir qualquer aplicativo padrão, como [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ou [!INCLUDE[ofprword](../../includes/ofprword-md.md)], você geralmente o utiliza para executar aplicativos de negócios ou arquivos de lote que trabalham em uma fonte de dados. Por exemplo, você pode usar a tarefa Executar Processo para expandir um arquivo de texto compactado. Depois, o pacote pode usar o arquivo de texto como uma fonte de dados para o fluxo de dados no pacote. Como outro exemplo, você pode usar a tarefa Executar Processo para executar um aplicativo [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] personalizado que gera um relatório de vendas diário. Em seguida, você pode anexar o relatório a uma tarefa Enviar Email e encaminhar o relatório para uma lista de distribuição.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui outras tarefas que realizam operações de fluxo de trabalho como executar pacotes. Para obter mais informações, consulte [Tarefa Executar Pacote](../../integration-services/control-flow/execute-package-task.md)  
  
## <a name="custom-log-entries-available-on-the-execute-process-task"></a>Entradas de log personalizadas disponíveis na tarefa Executar Processo  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Executar Processo. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|Fornece informações sobre o processo que a tarefa é configurada para executar.<br /><br /> São gravadas duas entradas de log. Uma contém informações sobre o nome e o local do executável que a tarefa executa e a outra registra a saída do executável.|  
|**ExecuteProcessVariableRouting**|Fornece informações sobre quais variáveis são encaminhadas para a entrada e as saídas do executável. As entradas de log são gravadas em stdin (a entrada), stdout (a saída) e stderr (a saída do erro).|  
  
## <a name="configuration-of-the-execute-process-task"></a>Configuração da Tarefa Executar Processo  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="property-settings"></a>Configurações de propriedades  
 Quando a tarefa Executar Processo executa um aplicativo personalizado, a tarefa fornece entrada para o aplicativo por meio de um ou de ambos estes métodos:  
  
-   Uma variável que você especifica na configuração da propriedade **StandardInputVariable**. Para obter mais informações sobre variáveis, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
-   Um argumento que você especifica na configuração de propriedade **Arguments**. Por exemplo, se a tarefa abrir um documento no Word, o argumento poderá nomear o arquivo .doc.  
  
 Para passar vários argumentos a um aplicativo personalizado em uma tarefa Executar Processo, use espaços para delimitar os argumentos. Um argumento não pode incluir um espaço; caso contrário, a tarefa não será executada. Você pode usar uma expressão para passar um valor variável como argumento. No exemplo a seguir, a expressão passa dois valores variáveis como argumentos e usa um espaço para delimitar os argumentos:  
  
 `@variable1 + " " + @variable2`  
  
 Você pode usar uma expressão para definir várias propriedades da tarefa Executar Processo.  
  
 Quando você usar a propriedade **StandardInputVariable** para configurar a tarefa Executar Processo para fornecer entrada, chame o método **Console.ReadLine** do aplicativo para ler a entrada. Para obter mais informações, consulte o tópico [Método Console.ReadLine](http://go.microsoft.com/fwlink/?LinkId=129201)na Biblioteca de Classes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
 Quando você usar a propriedade **Arguments** para configurar a tarefa Executar Processo para fornecer entrada, execute uma destas etapas para obter os argumentos:  
  
-   Se você usar Microsoft Visual Basic para escrever o aplicativo, defina a propriedade **My.Application.CommandLineArgs** . O exemplo a seguir define a propriedade **My.Application.CommandLineArgs** para recuperar dois argumentos:  
  
    ```vb  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     Para obter mais informações, consulte o tópico [Propriedade My.Application.CommandLineArgs](http://go.microsoft.com/fwlink/?LinkId=129200), na referência do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .  
  
-   Se você usar o Microsoft Visual C# para escrever o aplicativo, use o método **Main** .  
  
     Para obter mais informações, consulte o tópico [Argumentos de Linha de Comando (Guia de Programação C#)](http://go.microsoft.com/fwlink/?LinkId=129406), no Guia de Programação C#.  
  
 A tarefa Executar Processo também inclui as propriedades **StandardOutputVariable** e **StandardErrorVariable** para especificar as variáveis que consomem a saída padrão e a saída de erro do aplicativo, respectivamente.  
  
 Além disso, você pode configurar a tarefa Executar Processo para especificar um diretório de trabalho, um tempo-limite ou um valor para indicar que o executável foi executado com êxito. A tarefa também pode ser configurada para falhar se o código de retorno do executável não corresponder ao valor que indica êxito, ou se o executável não for encontrado no local especificado.  
  
## <a name="programmatic-configuration-of-the-execute-process-task"></a>Configuração programática da Tarefa Executar Processo  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## <a name="execute-process-task-editor-general-page"></a>Editor da Tarefa Executar Processo (página Geral)
  Use a página **Geral** da caixa de diálogo do **Editor da Tarefa Executar Processo** para nomear e descrever a tarefa Executar Processo.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Executar Processo. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Description**  
 Digite uma descrição para a tarefa Executar Processo.  
  
## <a name="execute-process-task-editor-process-page"></a>Execute Process Task Editor (Process Page)
  Use a página **Processo** da caixa de diálogo **Editor da Tarefa Executar Processo** , para configurar as opções que executam o processo. As opções incluem o executável a ser utilizado, seu local, argumentos do prompt de comando e as variáveis que fornecem entrada e capturam a saída.  
  
### <a name="options"></a>Opções  
 **RequireFullFileName**  
 Indique se a tarefa deve falhar se o executável não for localizado no local especificado.  
  
 **Executável**  
 Digite o nome do executável a utilizar.  
  
 **Argumentos**  
 Forneça argumentos do prompt de comando.  
  
 **WorkingDirectory**  
 Digite o caminho da pasta que contém o executável ou clique no botão Procurar **(…)** e localize a pasta.  
  
 **StandardInputVariable**  
 Selecione uma variável para fornecer entrada para o processo ou clique em \< **nova variável...** > para criar uma nova variável:  
  
 **Tópicos relacionados:** [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **StandardOutputVariable**  
 Selecione uma variável para capturar a saída do processo ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **StandardErrorVariable**  
 Selecione uma variável para capturar a saída de erro do processador ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 Indique se a tarefa deve falhar caso o código de saída do processo seja diferente do valor especificado em **SuccessValue**.  
  
 **SuccessValue**  
 Especifique o valor retornado pelo executável para indicar êxito. Por padrão, esse valor está definido como **0**.  
  
 **TimeOut**  
 Especifique o número de segundos em que o processo pode ser executado. Um valor **0** indica que não é usado nenhum valor de tempo limite e o processo é executado até ser concluído ou até ocorrer um erro.  
  
 **TerminateProcessAfterTimeOut**  
 Indique se o processo é forçado a terminar após o tempo limite especificado pela opção **TimeOut** . Esta opção só estará disponível se **TimeOut** não for **0**.  
  
 **WindowStyle**  
 Especifique o estilo de janela no qual executar o processo.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  

