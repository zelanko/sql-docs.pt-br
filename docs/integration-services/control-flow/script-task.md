---
title: Tarefa Script | Microsoft Docs
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
- sql13.dts.designer.scripttask.f1
- sql13.dts.designer.scripttask.general.f1
- sql13.dts.designer.scripttask.script.f1
helpviewer_keywords:
- scripts [Integration Services], tasks
- Script task [Integration Services], about Script task
- Script task [Integration Services]
ms.assetid: f6cce7df-4bd6-4b75-9f89-6c37b4bb5558
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 02febb9ffc5fd20842bff97edc231005a64c30dc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="script-task"></a>Tarefa Script
  A tarefa Script fornece código para execução de funções que não estão disponíveis nas tarefas internas e transformações fornecidas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . A tarefa Script também pode combinar funções em um script em vez de usar tarefas e transformações múltiplas. A tarefa Script é usada para trabalho que deve ser feito uma vez em um pacote (ou uma vez por objeto enumerado), e não para trabalho a ser feito uma vez por linha de dados.  
  
 A tarefa Script pode ser usada para os seguintes propósitos:  
  
-   Acessar dados usando outras tecnologias para as quais os tipos de conexão interna não dão suporte. Por exemplo, um script pode usar o ADSI (Active Directory Service Interfaces) para acessar e extrair os nomes de usuário do Active Directory.  
  
-   Criar um contador de desempenho específico de pacote. Por exemplo, um script pode criar um contador de desempenho que é atualizado enquanto uma tarefa de desempenho complexo ou insatisfatório é executada.  
  
-   Identificar se os arquivos especificados estão vazios ou quantas filas eles contêm e com base nessa informação afetar o fluxo de controle em um pacote. Por exemplo, se um arquivo não contiver nenhuma linha, o valor de uma variável definido como 0, e uma restrição de precedência que avalia o valor impedir que uma tarefa Sistema de Arquivos copie o arquivo.  
  
 Se você tiver que usar o script para fazer o mesmo trabalho para cada linha de dados em um conjunto, use o componente Script no lugar da tarefa Script. Por exemplo, para avaliar a racionalidade de um valor de postagem e ignorar linhas de dados com valores muito altos ou baixos, use um componente Script. Para obter mais informações, consulte [Script Component](../../integration-services/data-flow/transformations/script-component.md).  
  
 Se mais de um pacote usar um script, considere gravar uma tarefa personalizada em vez de usar a tarefa Script. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
 Depois de decidir que a tarefa Script é a escolha apropriada para seu pacote, você precisa desenvolver o script usado pela tarefa e configurar a própria tarefa.  
  
## <a name="writing-and-running-the-script-that-the-task-uses"></a>Gravando e executando o Script usado pela tarefa  
 A tarefa Script usa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) como o ambiente no qual você grava os scripts e o mecanismo que executa esses scripts.  
  
 O VSTA fornece todos os recursos padrão do ambiente [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] , como o editor [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] codificado por cor, o IntelliSense e o **Pesquisador de Objetos**. O VSTA também usa o mesmo depurador usado por outras ferramentas de desenvolvimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Os pontos de interrupção no script funcionam de forma consistente com os pontos de interrupção em tarefas e contêineres do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O VSTA dá suporte às linguagens de programação [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic e [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Para executar um script é necessário ter VSTA instalado no computador onde o pacote é executado. Quando o pacote é executado, a tarefa carrega o mecanismo de script e executa o script. Você pode acessar assemblies .NET externos em scripts adicionando referências aos assemblies no projeto.  
  
> [!NOTE]  
>  Ao contrário das versões anteriores em que você podia indicar se os scripts eram pré-compilados, todos os scripts são pré-compilados no [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] e em versões posteriores. Quando um script é pré-compilado, o mecanismo de linguagem não é carregado no tempo de execução e o pacote é executado mais rapidamente. No entanto, arquivos binários pré-compilados consomem espaço significativo em disco.  
  
## <a name="configuring-the-script-task"></a>Configurando a tarefa Script  
 Você pode configurar a tarefa Script das seguintes formas:  
  
-   Forneça o script personalizado executado pela tarefa.  
  
-   Especifique o método no projeto VSTA que o tempo de execução [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] chama como o ponto de entrada no código da tarefa Script.  
  
-   Especifique a linguagem do script.  
  
-   Opcionalmente, forneça listas somente leitura e variáveis de leitura/gravação para uso no script.  
  
 Você pode definir essas propriedades com o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
### <a name="configuring-the-script-task-in-the-designer"></a>Configurando a tarefa Script no Designer  
 A tabela a seguir descreve o evento **ScriptTaskLogEntry** que pode ser registrado para a tarefa Script. O evento **ScriptTaskLogEntry** é selecionado para registro em log na guia **Detalhes** da caixa de diálogo **Configurar Logs de SSIS** . Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**ScriptTaskLogEntry**|Informa os resultados da implementação do registro em log no script. A tarefa grava uma entrada de log para cada chamada ao método **Log** do objeto **Dts** . A tarefa grava essas entradas quando o código é executado. Para obter mais informações, consulte [Registro em log na Tarefa Script](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md).|  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, consulte os tópicos a seguir:  
  
-   [Editor da Tarefa Script &#40;Página Geral&#41;](../../integration-services/control-flow/script-task-editor-general-page.md)  
  
-   [Editor da Tarefa Script &#40;Página Script&#41;](../../integration-services/control-flow/script-task-editor-script-page.md)  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, consulte o tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="configuring-the-script-task-programmatically"></a>Configurando a tarefa Script programaticamente  
 Para obter mais informações sobre como definir essas propriedades programaticamente, veja o tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask>  
  
## <a name="script-task-editor-general-page"></a>Editor da Tarefa Script (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Script** para nomear e descrever a tarefa Script.  
  
 Para obter mais informações sobre a tarefa Script, consulte [Script Task](../../integration-services/control-flow/script-task.md) e [Configurando a tarefa Script no Editor da Tarefa Script](../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md). Para obter informações sobre a programação da tarefa Script, consulte [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md).  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Script. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Script.  
  
## <a name="script-task-editor-script-page"></a>Editor da Tarefa Script (página Script)
  Use a página **Script** da caixa de diálogo **Editor da Tarefa Script** para definir propriedades de script e especificar variáveis que podem ser acessados pelo script.  
  
> [!NOTE]  
>  No [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] e versões posteriores, todos os scripts são pré-compilados. Em versões anteriores, devia ser definida uma propriedade **PrecompileScriptIntoBinaryCode** para especificar que o script estava pré-compilado.  
  
 Para obter mais informações sobre a tarefa Script, consulte [Script Task](../../integration-services/control-flow/script-task.md) e [Configurando a tarefa Script no Editor da Tarefa Script](../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md). Para obter informações sobre a programação da tarefa Script, consulte [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md).  
  
### <a name="options"></a>Opções  
 **ScriptLanguage**  
 Selecione a linguagem de criação de scripts para a tarefa, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Depois de criar um script para a tarefa, você não poderá alterar o valor da propriedade **ScriptLanguage** .  
  
 Para definir a linguagem de criação de scripts padrão para a tarefa Script, use a opção **Idiomas de script** na página **Geral** da caixa de diálogo **Opções** . Para obter mais informações, consulte [General Page](../../integration-services/control-flow/script-task-editor-general-page.md).  
  
 **EntryPoint**  
 Especifique o método a ser chamado pelo tempo de execução do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como ponto de entrada no código da tarefa Script. O método especificado deve estar na classe ScriptMain do projeto do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). ScriptMain é a classe padrão gerada pelos modelos de script.  
  
 Caso altere o nome do método no projeto do VSTA, será preciso alterar o valor da propriedade **EntryPoint** .  
  
 **ReadOnlyVariables**  
 Digite uma lista, separada por vírgulas, de variáveis somente leitura disponíveis para o script ou clique no botão de reticências (**...**) e selecione as variáveis na caixa de diálogo **Selecionar variáveis** .  
  
> [!NOTE]  
>  Nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.  
  
 **ReadWriteVariables**  
 Digite uma lista, separada por vírgulas, de variáveis de leitura/gravação disponíveis para o script ou clique no botão de reticências (**…**) e selecione as variáveis na caixa de diálogo **Selecionar variáveis** .  
  
> [!NOTE]  
>  Nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.  
  
 **Editar Script**  
 Abre o VSTA IDE, onde você pode criar ou modificar o script.  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Artigo técnico sobre [Como enviar email com notificação de entrega em C#](http://go.microsoft.com/fwlink/?LinkId=237625)no site shareourideas.com  
  
  
