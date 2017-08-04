---
title: Criar um fluxo de trabalho personalizado (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 8e4403e9-595c-4b6b-9d0c-f6ae1b2bc99d
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dacc515af7f4d05fc2bad2fd43535bc27c13ea76
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-custom-workflow-master-data-services"></a>Criar um fluxo de trabalho personalizado (Master Data Services)
  O [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] usa regras de negócio para criar soluções de fluxo de trabalho básicas, como atualizar automaticamente e validar dados e obter o envio de notificações por email, com base nas condições especificadas. Quando você requer processamento mais complexo do que o oferecido pelas ações de fluxo de trabalho internas, use um fluxo de trabalho personalizado. Um fluxo de trabalho personalizado é um assembly .NET que você cria. Quando seu assembly de fluxo de trabalho é chamado, seu código pode executar qualquer ação que sua situação exija. Por exemplo, se seu fluxo de trabalho exigir o processamento de eventos complexos, como aprovações em várias camadas ou árvores de decisão complicadas, você poderá configurar o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para iniciar um fluxo de trabalho personalizado que analisa os dados e determina para onde enviá-lo para aprovação.  
  
## <a name="how-custom-workflows-are-processed"></a>Como os fluxos de trabalho personalizados são processados  
 Há três componentes principais envolvidos no processamento de fluxos de trabalho personalizados: o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server e o assembly de manipulador de fluxo de trabalho. Esses componentes processam um fluxo de trabalho personalizado da seguinte forma:  
  
1.  Você usa o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] para validar uma entidade que inicia um fluxo de trabalho.  
  
2.  O [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] envia membros que conhecem as condições de regra de negócio a uma fila do Service Broker no banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
3.  Em intervalos regulares, o Serviço de Integração de Fluxo de trabalho MDS do SQL Server chama um procedimento armazenado no banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
4.  Quando esse procedimento armazenado localiza registros na fila do Service Broker, retorna-os ao Serviço de Integração de Fluxo de Trabalho MDS do SQL Server.  
  
5.  O Serviço de Integração de Fluxo de Trabalho MDS do SQL Server encaminha os dados para seu assembly de manipulador de fluxo de trabalho.  
  
> [!NOTE]  
>  Observação: o Serviço de Integração de Fluxo de Trabalho do MDS do SQL Server deve disparar processos simples. Se seu código personalizado exigir processamento complexo, conclua seu processamento em um thread separado ou fora do processo de fluxo de trabalho.  
  
## <a name="configure-master-data-services-for-custom-workflows"></a>Configurar Master Data Services para fluxos de trabalho personalizados  
 A criação de um fluxo de trabalho personalizado requer gravação de um código personalizado e configuração do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para transmitir dados de fluxo de trabalho a seu manipulador de fluxo de trabalho. Siga estas etapas para habilitar o processamento de fluxo de trabalho personalizado:  
  
1.  Crie um assembly .NET que implementa <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>.  
  
2.  Configure o Serviço de Integração de Fluxo de trabalho MDS do SQL Server para conectar a seu banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e associar uma marca a um manipulador de fluxo de trabalho.  
  
3.  Iniciar o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server  
  
4.  Crie uma regra de negócios no [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] que inicie um fluxo de trabalho marcado com o nome do seu manipulador de fluxo de trabalho.  
  
5.  Aplique a regra de negócio a um membro que dispara seu fluxo de trabalho personalizado.  
  
### <a name="create-the-workflow-handler-assembly"></a>Crie o assembly de manipulador de fluxo de trabalho  
 Um fluxo de trabalho personalizado é um assembly de biblioteca de classe .NET que implementa a interface <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>. O Serviço de Integração de Fluxo de Trabalho MDS do SQL Server chama o método <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> para executar seu código. Por exemplo de código que implementa <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>, consulte [exemplo de fluxo de trabalho personalizado &#40; Master Data Services &#41; ](../../master-data-services/develop/create-a-custom-workflow-example.md).  
  
 Siga estas etapas para usar o Visual Studio 2010 para criar um assembly que o Serviço de Integração de Fluxo de trabalho MDS do SQL Server possa chamar para tratar um fluxo de trabalho personalizado:  
  
1.  No Visual Studio 2010, crie um novo **biblioteca de classes** projeto que usa o idioma de sua escolha. Para criar uma biblioteca de classes do c#, selecione a **Visual C# \Windows** tipos de projeto e selecione o **biblioteca de classes** modelo. Insira um nome para seu projeto, como **MDSWorkflowTest**e clique em **Okey**.  
  
2.  Adicione uma referência a Microsoft.MasterDataServices.WorkflowTypeExtender.dll. Este assembly pode ser encontrado na \<sua pasta de instalação > \Master Data Services\WebApplication\bin.  
  
3.  Adicione 'using Microsoft.MasterDataServices.Core.Workflow;' ao seu arquivo de código C#.  
  
4.  Herde de <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> em sua declaração de classe. A declaração de classe deve ser semelhante a: ‘public class WorkflowTester : IWorkflowTypeExtender’.  
  
5.  Implemente a interface <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>. O método <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> é chamado pelo Serviço de Integração de Fluxo de Trabalho MDS SQL Server para iniciar o fluxo de trabalho.  
  
6.  Copie o assembly para o local do serviço SQL Server MDS fluxo de trabalho de integração do executável, denominado Microsoft.MasterDataServices.Workflow.exe, em \<sua pasta de instalação > \Master Data Services\WebApplication\bin.  
  
### <a name="configure-sql-server-mds-workflow-integration-service"></a>Configurar o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server  
 Edite o arquivo de configuração do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para incluir informações de conexão do seu banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e associe uma marca a seu assembly de manipulador de fluxo de trabalho seguindo estas etapas:  
  
1.  Localize Microsoft.masterdataservices.Workflow.exe em \<sua pasta de instalação > \Master Data Services\WebApplication\bin.  
  
2.  Adicione as informações de conexão de banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] à configuração "ConnectionString". Se a sua instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar agrupamento com diferenciação de maiúsculas e minúsculas, o nome do banco de dados deverá ser inserido exatamente da mesma forma que no banco de dados. Por exemplo, a marca de configuração completa poderia se parecer com:  
  
    ```xml  
    <setting name="ConnectionString" serializeAs="String">  
        <value>Server=myServer;Database=myDatabase;Integrated Security=True</value>  
    </setting>  
    ```  
  
3.  Sob a configuração "ConnectionString" adicione uma configuração "WorkflowTypeExtenders" para associar um nome de marca a seu assembly de manipulador de fluxo de trabalho. Por exemplo:  
  
    ```xml  
    <setting name="WorkflowTypeExtenders" serializeAs="String">  
        <value>TEST=MDSWorkflowTestLib.WorkflowTester, MDSWorkflowTestLib</value>  
    </setting>  
    ```  
  
     O texto interno do \<valor > marca está na forma de \<Workflow tag > =\<nome de tipo qualificado de assembly de fluxo de trabalho >. \<Marcação de fluxo de trabalho > é um nome que você usa para identificar o assembly de manipulador de fluxo de trabalho quando você cria uma regra de negócio em [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. \<nome de tipo qualificado de assembly de fluxo de trabalho > é o nome qualificado de namespace da classe do fluxo de trabalho, seguido por uma vírgula, seguido do nome de exibição do assembly. Se seu assembly usar um nome forte, você também terá que incluir informações de versão e seu PublicKeyToken. Você pode incluir vários \<Configuração > marcas se você tiver criado vários manipuladores de fluxo de trabalho para diferentes tipos de fluxos de trabalho.  
  
> [!NOTE]  
>  Dependendo da configuração do seu servidor, você poderá visualizar um erro do tipo "Acesso negado" ao tentar salvar o arquivo Microsoft.MasterDataServices.Workflow.exe.config. Se isso ocorrer, desabilite temporariamente o UAC (Controle de Conta de Usuário) no servidor. Para fazer isso, abra o painel de controle, clique em **sistema e segurança**. Em **Central de ações**, clique em **alterar configurações de controle de conta de usuário**. No **configurações de controle de conta de usuário** caixa de diálogo, deslize a barra na parte inferior para que você nunca seja notificado. Reinicie seu computador e repita as etapas anteriores para editar seu arquivo de configuração. Depois de salvar o arquivo, reinicie suas configurações de UAC no nível padrão.  
  
### <a name="start-sql-server-mds-workflow-integration-service"></a>Iniciar o serviço de integração de fluxo de trabalho MDS do SQL Server  
 Por padrão, o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server não é instalado. Você deve instalar o serviço antes de usá-lo. Para obter a segurança máxima, crie um usuário local para o serviço e conceda a ele apenas as permissões necessárias para executar operações de fluxo de trabalho. Para criar um usuário, instale e inicie o serviço e siga estas etapas:  
  
1.  Use o gerenciador Usuários e Grupos Locais para criar um usuário local denominado, por exemplo, mds_workflow_service.  
  
2.  Use o SQL Server Management Studio para conceder a permissão de usuário a mds_workflow_service para executar o procedimento armazenado [mdm]. [udpExternalActionsGet]. Para fazer isso, crie um novo logon para a conta mds_workflow_service, crie um novo usuário no banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], mapeie esse usuário para o logon de mds_workflow_service e conceda ao usuário a permissão de EXECUTE para o procedimento armazenado [mdm]. [udpExternalActionsGet].  
  
3.  Conceda a permissão de usuário a mds_workflow_service para executar o assembly de manipulador de fluxo de trabalho. Para fazer isso, adicione o usuário mds_workflow_service o **segurança** guia o **propriedades** do fluxo de trabalho assembly de manipulador e conceda ao usuário mds_workflow_service permissões READ e EXECUTE.  
  
4.  Conceda a permissão de usuário a mds_workflow_service para executar o executável do Serviço de Integração de Fluxo de Trabalho MDS do SQL Server. Para fazer isso, adicione o usuário mds_workflow_service o **segurança** guia do **propriedades** de Microsoft.MasterDataServices.Workflow.exe, em \<sua pasta de instalação > \Master Data Services\WebApplication\bin e conceda ao usuário mds_workflow_service permissões READ e EXECUTE.  
  
5.  Instale o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server usando o utilitário de instalação .NET, denominado InstallUtil.exe. InstallUtil.exe pode ser encontrado na pasta de instalação .NET, como C:\Windows\Microsoft.NET\Framework\v4.0.30319\\. Instale o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server inserindo o seguinte em um prompt de comando elevado:  
  
    ```  
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil Microsoft.MasterDataServices.Workflow.exe  
    ```  
  
     Especifique o usuário mds_workflow_service quando solicitado durante a instalação.  
  
6.  Inicie o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server usando o snap-in Serviços. Para fazer isso, localizar o serviço de integração de fluxo de trabalho do SQL Server MDS no snap-in Serviços, selecione-o e clique no **iniciar** link.  
  
### <a name="create-a-workflow-business-rule"></a>Criar uma regra de negócio de fluxo de trabalho  
 Use o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] para criar e publicar uma regra de negócio que iniciará o fluxo de trabalho quando aplicada. Você deve assegurar que sua regra de negócio contenha ações que alteram valores de atributo, de forma que a regra seja avaliada como falsa depois de ser aplicada uma vez. Por exemplo, sua regra de negócio pode ser avaliada como verdadeira quando um valor do atributo Price for maior que 500 e o valor do atributo Approved estiver em branco. A regra pode incluir duas ações: uma para definir o valor do atributo Approved como Pending e uma para iniciar o fluxo de trabalho. Alternativamente, talvez você queira criar uma regra que use a condição "has changed" e adicionar seus atributos a grupos de controle de alterações. Para obter mais informações sobre regras de negócio, consulte [regras de negócio &#40; Master Data Services &#41; ](../../master-data-services/business-rules-master-data-services.md).  
  
 Crie uma regra de negócio que inicie um fluxo de trabalho personalizado no [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] seguindo estas etapas:  
  
1.  No editor de regras de negócios de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], depois de especificar as condições da regra de negócio, arraste o **Iniciar fluxo de trabalho** ação do **ações externas** lista para o **, em seguida,** do painel **ação** rótulo.  
  
2.  No **Editar ação** painel, no **tipo de fluxo de trabalho** , digite a marca que identifica seu assembly de manipulador de fluxo de trabalho. Essa é a marca que você especificou no arquivo de configuração do assembly, por exemplo TEST.  
  
3.  Opcionalmente, selecione o **incluir dados de membro** caixa de seleção. Escolha essa opção para incluir nomes de atributo e valores no XML transmitido ao manipulador de fluxo de trabalho.  
  
4.  No **site de fluxo de trabalho** , digite o nome de um site. Talvez isso não se aplique ao seu fluxo de trabalho personalizado, mas pode ser usado para contexto adicionado.  
  
5.  No **nome do fluxo de trabalho** , digite o nome do fluxo de trabalho do Visual Studio. Talvez isso não se aplique ao seu fluxo de trabalho personalizado, mas pode ser usado para contexto adicionado.  
  
6.  Salve e publique a regra de negócio.  
  
### <a name="apply-business-rules-to-start-a-workflow"></a>Aplicar regras de negócios para iniciar um fluxo de trabalho  
 Aplique a regra de negócio a seus dados para iniciar o fluxo de trabalho. Para fazer isso, use o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] para editar a entidade que contém os membros que você deseja validar. Clique em **aplicar regras de negócio**. Em resposta à regra de negócio, o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] popula a fila do Service Broker do banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Quando Serviço de Integração de Fluxo de Trabalho MDS do SQL Server verificar a fila, enviará os dados ao assembly de manipulador de fluxo de trabalho especificado e limpará a fila. O assembly de manipulador de fluxo de trabalho executa qualquer ação que você tenha codificado para ele.  
  
## <a name="troubleshoot-custom-workflows"></a>Solucionar problemas fluxos de trabalho personalizados  
 Se seu assembly de manipulador de fluxo de trabalho não receber dados, você poderá tentar depurar o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server ou exibir a fila do Service Broker.  
  
### <a name="debug-sql-server-mds-workflow-integration-service"></a>Depurar o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server  
 Para depurar o Serviço de Integração de Fluxo de Trabalho MDS do SQL Server, siga estas etapas:  
  
1.  Use o snap-in Serviços para parar o serviço.  
  
2.  Abra um prompt de comando, navegue para local do serviço e execute o serviço no modo de console inserindo: Microsoft.MasterDataServices.Workflow.exe - console.  
  
3.  No [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], atualize seu membro e aplique regras de negócios novamente. Logs detalhados são exibidos na janela do console.  
  
### <a name="view-the-service-broker-queue"></a>Exibir a fila do Service Broker  
 A fila do Service Broker que contém os dados mestre transmitidos como parte do fluxo de trabalho é: mdm.microsoft/mdm/queue/externalaction. As filas podem ser encontradas no **Pesquisador de objetos** do SQL Management Studio sob o nó do Service Broker do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] banco de dados. Esteja ciente de que, se o serviço limpou a fila corretamente, ela fila estará vazia.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de fluxo de trabalho personalizado &#40; Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)   
 [Descrição do fluxo de trabalho personalizado XML &#40; Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md)  
  
  
