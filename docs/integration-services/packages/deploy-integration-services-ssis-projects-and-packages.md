---
description: Implantar projetos e pacotes do Integration Services (SSIS)
title: Implantar projetos e pacotes do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: vanto
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.bids.converttolegacydeployment.f1
- sql13.ssis.deploymentwizard.f1
- sql13.ssis.ssms.isenvprop.permissions.f1
- sql13.ssis.ssms.isenvprop.general.f1
- sql13.ssis.ssms.iscreateenv.f1
- sql13.ssis.ssms.isenvprop.variables.f1
- sql13.ssis.migrationwizard.f1
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 90fdfd4a64d77d3fa51ef7dc4c39ccf11b1fb9f3
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130068"
---
# <a name="deploy-integration-services-ssis-projects-and-packages"></a>Implantar projetos e pacotes do Integration Services (SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dá suporte a dois modelos de implantação, o modelo de implantação de projeto e o modelo de implantação de pacote herdado. O modelo de implantação de projeto permite que você implante seus projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
Para obter mais informações sobre o modelo de implantação de pacote herdado, consulte [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
> [!NOTE]  
>  O modelo de implantação do projeto foi introduzido no [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]. Com esse modelo de implantação, não era possível implantar um ou mais pacotes sem implantar todo o projeto. O [!INCLUDE[ssISversion13](../../includes/ssisversion13-md.md)] introduziu o recurso de Implantação Incremental de Pacotes, que permite implantar um ou mais pacotes, sem implantar o projeto inteiro.

> [!NOTE]
> Este artigo descreve como implantar pacotes do SSIS em geral e como implantar pacotes localmente. Também é possível implantar pacotes do SSIS para as seguintes plataformas:
> - **A nuvem do Microsoft Azure**. Para obter mais informações, consulte [Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).
> - **Linux**. Para obter mais informações, consulte [Extrair, transformar e carregar dados no Linux com o SSIS](../../linux/sql-server-linux-migrate-ssis.md).

## <a name="compare-project-deployment-model-and-legacy-package-deployment-model"></a>Compare o modelo de implantação de projeto e o modelo de implantação de pacote herdado

 O tipo de modelo de implantação que você escolhe para um projeto determina quais opções de desenvolvimento e administrativas estão disponíveis para aquele projeto. A tabela a seguir mostra as diferenças e as semelhanças entre o uso do modelo de implantação de projeto e o uso do modelo de implantação de pacote.  
  
|Ao usar o modelo de implantação de projeto|Quando usar o modelo de implantação de pacote herdado|  
|---------------------------------------------|----------------------------------------------------|  
|Um projeto é a unidade de implantação.|Um pacote é a unidade de implantação.|  
|Parâmetros são usados para atribuir valores a propriedades de pacote.|As configurações são usadas para atribuir valores a propriedades de pacote.|  
|Um projeto, que contém pacotes e parâmetros, é compilado em um arquivo de implantação de projeto (extensão .ispac).|Os pacotes (extensão .dtsx) e as configurações (extensão .dtsConfig) são salvos individualmente no sistema de arquivos.|  
|Um projeto que contém pacotes e parâmetros é implantado no catálogo do SSISDB em uma instância do SQL Server.|Os pacotes e as configurações são copiados no sistema de arquivos em outro computador. Os pacotes também podem ser salvos no banco de dados MSDB ou em uma instância do SQL Server.|  
|A integração CLR é necessária no mecanismo de banco de dados.|A integração CLR não é necessária no mecanismo de banco de dados.|  
|Os valores dos parâmetros específicos ao ambiente são armazenados em variáveis de ambiente.|Os valores de configuração específicos ao ambiente são armazenados nos arquivos de configuração.|  
|Os projetos e pacotes do catálogo podem ser validados no servidor antes da execução. Você pode usar o SQL Server Management Studio, procedimentos armazenados ou código gerenciado para executar a validação.|Os pacotes são validados antes da execução. Você também pode validar um pacote com o código gerenciado dtExec.|  
|Os pacotes são executados com o início de uma execução no mecanismo de banco de dados. Um identificador de projeto, valores de parâmetros explícitos (opcional) e referências ao ambiente (opcional) são atribuídos a uma execução antes de ela ser iniciada.<br /><br /> Também é possível executar pacotes usando **dtExec**.|Os pacotes são executados com os utilitários de execução **dtExec** e **DTExecUI** . As configurações aplicáveis são identificadas por argumentos de prompt de comando (opcional).|  
|Durante a execução, os eventos produzidos pelo pacote são capturados automaticamente e salvos no catálogo. Você pode consultar esses eventos com exibições Transact-SQL.|Durante a execução, os eventos produzidos por um pacote não são capturados automaticamente. Um provedor de log deve ser adicionado ao pacote para capturar eventos.|  
|Os pacotes são executados em um processo separado do Windows.|Os pacotes são executados em um processo separado do Windows.|  
|O SQL Server Agent é usado para agendar a execução do pacote.|O SQL Server Agent é usado para agendar a execução do pacote.|  


## <a name="features-of-project-deployment-model"></a>Recursos do modelo de implantação de projeto  
 A tabela a seguir lista os recursos que estão disponíveis para projetos desenvolvidos apenas para o modelo de implantação de projeto.  
  
|Recurso|Descrição|  
|-------------|-----------------|  
|Parâmetros|Um parâmetro especifica os dados que serão usados por um pacote. Você pode definir o escopo dos parâmetros no nível do pacote ou do projeto com parâmetros de pacote e de projeto, respectivamente. Os parâmetros podem ser usados em expressões ou tarefas. Quando o projeto é implantado no catálogo, você pode atribuir um valor literal para cada parâmetro ou usar o valor padrão que foi atribuído em tempo de design. Em lugar de um valor literal, você também pode fazer referência a uma variável de ambiente. Os valores de variáveis de ambiente são resolvidos na hora da execução do pacote.|  
|Ambientes|Um ambiente é um contêiner de variáveis que podem ser referenciadas por projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Cada projeto pode ter várias referências de ambiente, mas uma única instância de execução de pacote pode fazer referência apenas a variáveis de um único ambiente. Os ambientes permitem organizar os valores que você atribui a um pacote. Por exemplo, você pode ter ambientes denominados "Desenvolvimento", "Teste" e "Produção".|  
|Variáveis de ambiente|Uma variável de ambiente define um valor literal que pode ser atribuído a um parâmetro durante a execução do pacote. Para usar uma variável de ambiente, crie uma referência de ambiente (no projeto que corresponde ao ambiente que tem o parâmetro), atribua um valor de parâmetro ao nome da variável de ambiente e especifique a referência de ambiente correspondente ao configurar uma instância de execução.|  
|Catálogo do SSISDB|Todos os objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são armazenados e gerenciados em uma instância do SQL Server em um banco de dados chamado de catálogo do SSISDB. O catálogo permite usar pastas para organizar seus projetos e ambientes. Cada instância do SQL Server pode ter um catálogo. Cada catálogo pode ter zero ou mais pastas. Cada pasta pode ter zero ou mais projetos e zero ou mais ambientes. Uma pasta do catálogo também pode ser usada como um limite para permissões para objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|Procedimentos armazenados e exibições do catálogo|Um grande número de procedimentos armazenados e exibições pode ser usado para gerenciar objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no catálogo. Por exemplo, você pode especificar valores para parâmetros e variáveis de ambiente, criar e iniciar execuções e monitorar operações do catálogo. É possível até ver exatamente quais valores serão usados por um pacote antes do início da execução.|  
  
## <a name="project-deployment"></a>Implantação de projeto  
 No centro do modelo de implantação do projeto está o arquivo de implantação do projeto (extensão .ispac). O arquivo de implantação do projeto é uma unidade independente de implantação que inclui apenas as informações essenciais sobre os pacotes e parâmetros do projeto. O arquivo de implantação do projeto não captura todas as informações contidas no arquivo do projeto do Integration Services (extensão .dtproj). Por exemplo, arquivos de texto adicionais que você usa para escrever observações não são armazenados no arquivo de implantação do projeto e, portanto, não são implantados no catálogo.  

## <a name="permissions-required-to-deploy-ssis-projects-and-packages"></a>Permissões necessárias para implantar projetos e pacotes do SSIS

Se você alterar a conta de serviço do SSIS do padrão, precisará conceder permissões adicionais para a conta de serviço não padrão antes de implantar pacotes com êxito. Se a conta de serviço não padrão não tiver as permissões necessárias, você poderá ver a mensagem de erro a seguir.

`A .NET Framework error occurred during execution of user-defined routine or aggregate "deploy_project_internal":
System.ComponentModel.Win32Exception: A required privilege is not held by the client.`

Esse erro normalmente é o resultado de permissões DCOM ausentes. Para corrigir o erro, faça o seguinte:

1.  Abra o console **Serviços de Componentes** (ou execute Dcomcnfg.exe).
2.  No console **Serviços de Componentes**, expanda **Serviços de Componentes** > **Computadores** > **Meu Computador** > **Configuração do DCOM**.
3.  Na lista, localize **Microsoft SQL Server Integration Services xx.0** na versão do SQL Server que está sendo usada. Por exemplo, o SQL Server 2016 é a versão 13.
4.  Clique com o botão direito do mouse e selecione **Propriedades**.
5.  Na caixa de diálogo **Propriedades do Microsoft SQL Server Integration Services 13.0**, selecione a guia **Segurança**.
6.  Para cada um dos três conjuntos de permissões – Inicialização e Ativação, Acesso e Configuração – selecione **Personalizar** e, em seguida, **Editar** para abrir a caixa de diálogo **Permissão**.
7.  Na caixa de diálogo **Permissão**, adicione a conta de serviço não padrão e conceda permissões **Permitir**, conforme necessário. Normalmente, uma conta tem as permissões **Inicialização Local** e **Ativação Local**.
8.  Clique em **OK** duas vezes e, em seguida, feche o console **Serviços de Componentes**.

Para obter mais informações sobre o erro descrito nesta seção e sobre as permissões necessárias para a conta de serviço do SSIS, confira a seguinte postagem no blog:
 
- [System.ComponentModel.Win32Exception: o cliente não tem um privilégio obrigatório durante a Implantação de Projeto do SSIS](/archive/blogs/dataaccesstechnologies/system-componentmodel-win32exception-a-required-privilege-is-not-held-by-the-client-while-deploying-ssis-project)

## <a name="deploy-projects-to-integration-services-server"></a>Implantar projetos no servidor do Integration Services
  Na versão atual do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode implantar seus projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite gerenciar pacotes, executar pacotes, e configura valores de runtime para pacotes por meio de ambientes.  
  
> [!NOTE]  
>  Como nas versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], na versão atual você também pode implantar seus pacotes em uma instância do SQL Server e usar o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para executar e gerenciar os pacotes. Você usa o modelo de implantação de pacote. Para obter mais informações, consulte [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
 Para implantar um projeto no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , conclua as tarefas a seguir:  
  
1.  Criar um catálogo do SSISDB se ainda não tiver criado. Para obter mais informações, consulte [Catálogo do SSIS](../../integration-services/catalog/ssis-catalog.md).  
  
2.  Converta o projeto no modelo de implantação de projeto executando o **Assistente de Conversão de Projeto do Integration Services**. Para obter mais informações, confira as seguintes instruções: [Para converter um projeto no modelo de implantação de projeto](#convert)  
  
    -   Se você criou o projeto no [!INCLUDE[ssISversion12](../../includes/ssisversion12-md.md)] ou posterior, por padrão, o projeto usa o modelo de implantação de projeto.  
  
    -   Se você criou o projeto em uma versão anterior do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], depois que abrir o arquivo de projeto no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], converta o projeto no modelo de implantação de projeto.  
  
        > [!NOTE]  
        >  Se o projeto contiver uma ou mais fontes de dados, as fontes de dados serão removidas quando a conversão de projeto estiver concluída. Para criar uma conexão com uma fonte de dados que pode ser compartilhada pelos pacotes no projeto, adicione um gerenciador de conexões no nível de projeto. Para obter mais informações, consulte [adicionar, excluir ou compartilhar um Gerenciador de Conexão em um pacote](/previous-versions/sql/sql-server-2016/ms140237(v=sql.130)).  
  
         Dependendo em se você executa o **Assistente de Conversão de Projeto do Integration Services** no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o assistente executa tarefas de conversão diferentes.  
  
        -   Se você executar o assistente de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], os pacotes contidos no projeto serão convertidos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 2005, 2008 ou 2008 R2 no formato usado pela versão atual do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. O projeto original (.dtproj) e os arquivos de pacotes (.dtsx) são atualizados.  
  
        -   Se você executar o assistente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ele gerará um arquivo de implantação de projeto (.ispac) de pacotes e configurações contidos no projeto. Os arquivos de pacote original (.dtsx) não são atualizados.  
  
             Você pode selecionar um arquivo existente ou criar um novo arquivo, na página **Destino de Seleção** do assistente.  
  
             Para atualizar arquivos de pacotes quando um projeto é convertido, execute o **Assistente de Conversão de Projeto do Integration Services** de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Para atualizar os arquivos de pacotes separadamente de uma conversão de projeto, execute o **Assistente de Conversão de Projeto do Integration Services** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e, em seguida, execute o **Assistente de Atualização de Pacotes SSIS**. Se você atualizar os arquivos de pacotes separadamente, verifique se você salvou as alterações. Caso contrário, quando você converter o projeto no modelo de implantação de projeto, todas as alterações não salvas no pacote não serão convertidas.  
  
     Para obter mais informações sobre a atualização de pacotes, consulte [Atualizar pacotes do Integration Services](../../integration-services/install-windows/upgrade-integration-services-packages.md) e [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
3.  Implante o projeto no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações, confira as instruções abaixo: [Para implantar um projeto no Servidor do Integration Services](#deploy).  
  
4.  (Opcional) Crie um ambiente para o projeto implantado. 
  
###  <a name="to-convert-a-project-to-the-project-deployment-model"></a><a name="convert"></a> Para converter um projeto no modelo de implantação de projeto  
  
1.  Abra o projeto no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]e, no Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Converter em Modelo de Implantação de Projeto**.  
  
     - ou -  
  
     No Pesquisador de Objetos, no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], clique com o botão direito do mouse no nó **Projetos** e selecione **Importar Pacotes**.  
  
2.  Conclua o assistente.
  
###  <a name="to-deploy-a-project-to-the-integration-services-server"></a><a name="deploy"></a> Para implantar um projeto no Servidor do Integration Services  
  
1.  Abra o projeto no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]e, em seguida, no menu **Projeto** , selecione **Implantar** para implantar o **Assistente de Implantação do Integration Services**.  
  
     ou  
  
     No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] > **SSISDB** no Pesquisador de Objetos e localize a pasta Projetos do projeto que você deseja implantar. Clique com o botão direito do mouse na pasta **Projetos** e clique em **Implantar Projeto**.  
  
     ou  
  
     No prompt de comando, execute **isdeploymentwizard.exe** de **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn**. Em computadores de 64 bits, há também uma versão de 32 bits da ferramenta em **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn**.  
  
2.  Na página **Selecionar Origem** , clique em **Arquivo de implantação de projeto** para selecionar o arquivo de implantação do projeto.  
  
     ou  
  
     Clique em **Catálogo do Integration Services** para selecionar um projeto que já foi implantado no catálogo do SSISDB.  
  
3.  Conclua o assistente. 

## <a name="deploy-packages-to-integration-services-server"></a>Implantar pacotes no Servidor do Integration Services
  O recurso de implantação de pacotes incremental introduzido no  [!INCLUDE[ssISversion13](../../includes/ssisversion13-md.md)] permite que você implante um ou mais pacotes para um projeto novo ou existente, sem implantar o projeto inteiro.  
  
###  <a name="deploy-packages-by-using-the-integration-services-deployment-wizard"></a><a name="DeployWizard"></a> Implantar pacotes usando o Assistente de implantação do Integration Services  
  
1.  No prompt de comando, execute **isdeploymentwizard.exe** de **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn**. Em computadores de 64 bits, há também uma versão de 32 bits da ferramenta em **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn**.  
  
2.  Na página **Selecionar fonte** , mude para **Modelo de implantação do pacote**. Em seguida, selecione a pasta que contém pacotes de origem e configure os pacotes.  
  
3.  Conclua o assistente. Siga as etapas restantes descritas em [Modelo de Implantação do Pacote](#PackageModel).  
  
###  <a name="deploy-packages-by-using-sql-server-management-studio"></a><a name="SSMS"></a> Implantar pacotes usando o SQL Server Management Studio  
  
1.  No SQL Server Management Studio, expanda o nó **Catálogos do Integration Services** > **SSISDB** no Pesquisador de Objetos.  
  
2.  Clique com o botão direito do mouse na pasta **Projetos** e clique em **Implantar Projetos**.  
  
3.  Se você vir a página **Introdução** clique em **Avançar** para continuar.  
  
4.  Na página **Selecionar fonte** , mude para **Modelo de implantação do pacote**. Em seguida, selecione a pasta que contém pacotes de origem e configure os pacotes.  
  
5.  Conclua o assistente. Siga as etapas restantes descritas em [Modelo de Implantação do Pacote](#PackageModel).  
  
###  <a name="deploy-packages-by-using-sql-server-data-tools-visual-studio"></a><a name="SSDT"></a> Implantar pacotes usando o SQL Server Data Tools (Visual Studio)  
  
1.  No Visual Studio, com um projeto do Integration Services aberto, selecione o pacote ou pacotes que você quer implantar.  
  
2.  Clique com o botão direito do mouse e selecione **Implantar Pacote**. O Assistente de implantação é aberto com os pacotes selecionados configurados como pacotes de código-fonte.  
  
3.  Conclua o assistente. Siga as etapas restantes descritas em [Modelo de Implantação do Pacote](#PackageModel).  
  
###  <a name="deploy-packages-by-using-the-deploy_packages-stored-procedure"></a><a name="StoredProcedure"></a> Implantar pacotes usando o procedimento armazenado deploy_packages  
 Você pode usar o procedimento armazenado **[catalog].[ deploy_packages]** para implantar um ou mais pacotes do SSIS no catálogo do SSIS. O exemplo de código a seguir demonstra o uso desse procedimento armazenado para implantar pacotes em um servidor SSIS. Para obter mais informações, consulte [catalog.deploy_packages](../../integration-services/system-stored-procedures/catalog-deploy-packages.md).  
  
```cs
  
private static void Main(string[] args)  
{  
    // Connection string to SSISDB  
    var connectionString = "Data Source=.;Initial Catalog=SSISDB;Integrated Security=True;MultipleActiveResultSets=false";  
  
    using (var sqlConnection = new SqlConnection(connectionString))  
    {  
        sqlConnection.Open();  
  
        var sqlCommand = new SqlCommand  
        {  
            Connection = sqlConnection,  
            CommandType = CommandType.StoredProcedure,  
            CommandText = "[catalog].[deploy_packages]"  
        };  
  
        var packageData = Encoding.UTF8.GetBytes(File.ReadAllText(@"C:\Test\Package.dtsx"));  
  
        // DataTable: name is the package name without extension and package_data is byte array of package.  
        var packageTable = new DataTable();  
        packageTable.Columns.Add("name", typeof(string));  
        packageTable.Columns.Add("package_data", typeof(byte[]));  
        packageTable.Rows.Add("Package", packageData);  
  
        // Set the destination project and folder which is named Folder and Project.  
        sqlCommand.Parameters.Add(new SqlParameter("@folder_name", SqlDbType.NVarChar, ParameterDirection.Input, "Folder", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@project_name", SqlDbType.NVarChar, ParameterDirection.Input, "Project", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@packages_table", SqlDbType.Structured, ParameterDirection.Input, packageTable, -1));  
  
        var result = sqlCommand.Parameters.Add("RetVal", SqlDbType.Int);  
        result.Direction = ParameterDirection.ReturnValue;  
  
        sqlCommand.ExecuteNonQuery();  
    }  
}  
  
```  
  
###  <a name="deploy-packages-using-the-management-object-model-api"></a><a name="MOMApi"></a> Implantar pacotes usando a API do Modelo de objeto de gerenciamento  
 O exemplo de código a seguir demonstra o uso da API do Modelo de objeto de gerenciamento para implantar pacotes no servidor.  
  
```cs 
  
static void Main()  
 {  
     // Before deploying packages, make sure the destination project exists in SSISDB.  
     var connectionString = "Data Source=.;Integrated Security=True;MultipleActiveResultSets=false";  
     var catalogName = "SSISDB";  
     var folderName = "Folder";  
     var projectName = "Project";  
  
     // Get the folder instance.  
     var sqlConnection = new SqlConnection(connectionString);  
     var store = new Microsoft.SqlServer.Management.IntegrationServices.IntegrationServices(sqlConnection);  
     var folder = store.Catalogs[catalogName].Folders[folderName];  
  
     // Key is package name without extension and value is package binaries.  
     var packageDict = new Dictionary<string, string>();  
  
     var packageData = File.ReadAllText(@"C:\Folder\Package.dtsx");  
     packageDict.Add("Package", packageData);  
  
     // Deploy package to the destination project.  
     folder.DeployPackages(projectName, packageDict);  
 }  
  
```

## <a name="convert-to-package-deployment-model-dialog-box"></a>Caixa de diálogo Converter em Modelo de Implantação de Pacote
  A caixa de diálogo **Converter em Modelo de Implantação de Pacote** permite converter um pacote para o modelo de implantação de pacote depois de verificar se o projeto e cada pacote do projeto são compatíveis com esse modelo. Se um pacote usar recursos exclusivos para o modelo de implantação de projeto, como parâmetros, o pacote não poderá ser convertido.  

 Converter um pacote para o modelo de implantação de pacote exige duas etapas.  
  
1.  Quando você seleciona o comando **Converter em Modelo de Implantação de Pacote** no menu **Project** , o projeto e cada pacote do projeto terão a compatibilidade verificada com esse modelo. Os resultados são exibidos na tabela **Resultados** .  
  
     Se o projeto ou pacote falhar no teste de compatibilidade, clique em **Falha** na coluna **Resultado** para obter mais informações. Clique em **Salvar Relatório** para salvar uma cópia destas informações em um arquivo de texto.  
  
2.  Se o projeto e todos os pacotes passarem no teste de compatibilidade, clique em **OK** para converter o pacote.  
  
> [!NOTE]
> Para converter um projeto no modelo de implantação de projeto, use o **Assistente de Conversão de Projeto do Integration Services**. Para obter mais informações, consulte [Integration Services Project Conversion Wizard](deploy-integration-services-ssis-projects-and-packages.md).  

## <a name="integration-services-deployment-wizard"></a>Assistente de Implantação do Integration Services
  O **Assistente de Implantação do Integration Services** dá suporte a dois modelos de implantação:
   - Modelo de implantação de projeto
   - Modelo de implantação do pacote 
   
 O **modelo de Implantação do Projeto** permite implantar um projeto do SSIS (SQL Server Integration Services) como uma única unidade no Catálogo do SSIS.
 
 O **modelo de Implantação do Pacote** permite implantar pacotes que você atualizou no Catálogo do SSIS sem precisar implantar o projeto todo. 
 
 > [!NOTE]
 > A implantação padrão do Assistente é o modelo de Implantação do Projeto.  
  
### <a name="launch-the-wizard"></a>Iniciar o assistente
Inicie o assistente:

 - Digitando **“Assistente de Implantação do SQL Server”** no Windows Search 

 ou

 - Pesquisando o arquivo executável **ISDeploymentWizard.exe** na pasta de instalação do SQL Server; por exemplo: "C:\Arquivos de Programas (x86)\Microsoft SQL Server\130\DTS\Binn". 
 
 > **OBSERVAÇÃO:** se a página **Introdução** for exibida, clique em **Avançar** para mudar para a página **Selecionar Fonte** . 
 
 As configurações nessa página são diferentes para cada modelo de implantação. Siga as etapas na seção [Project Deployment Model](#ProjectModel) ou na seção [Package Deployment Model](#PackageModel) de acordo com o modelo selecionado nessa página.  
  
###  <a name="project-deployment-model"></a><a name="ProjectModel"></a> Project Deployment Model  
  
#### <a name="select-source"></a>Selecionar fonte

 Para implantar um arquivo de implantação do projeto que você criou, selecione **Arquivo de implantação do projeto** e insira o caminho para o arquivo .ispac. Para implantar um projeto residente no catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , selecione **Catálogo do Integration Services** e insira o nome do servidor e o caminho para o projeto no catálogo. Clique em **Avançar** para ver a página **Selecionar Destino** .  
  
#### <a name="select-destination"></a>Selecionar Destino

 Para selecionar a pasta de destino para o projeto no catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , insira a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou clique em **Procurar** para selecionar de uma lista de servidores. Digite o caminho do projeto no SSISDB ou clique em **Procurar** para selecioná-lo. Clique em **Avançar** para ver a página **Revisar** .  
  
#### <a name="review-and-deploy"></a>Revisar (e implantar)

 A página permite revisar as configurações que você selecionou. Você pode alterar suas seleções clicando em **Anterior** ou clicando em qualquer uma das etapas no painel esquerdo. Clique em **Implantar** para começar o processo de implantação.  
  
#### <a name="results"></a>Resultados

 Depois que o processo de implantação estiver concluído, você deverá ver a página **Resultados** . Essa página exibe o êxito ou a falha de cada ação. Se a ação falhar, clique em **Com falha** na coluna **Resultado** para exibir uma explicação do erro. Clique em **Salvar Relatório...** para salvar os resultados em um arquivo XML ou clique em **Fechar** para sair do assistente.
  
###  <a name="package-deployment-model"></a><a name="PackageModel"></a> Package Deployment Model  
  
#### <a name="select-source"></a>Selecionar fonte

 A página **Selecionar Origem** no **Assistente de Implantação do Integration Services** mostra configurações específicas ao modelo de implantação do pacote quando você selecionou a opção **Implantação do Pacote** para o **modelo de implantação**.  
  
 Para selecionar os pacotes de origem, clique no botão **Procurar…** para selecionar a **pasta** que contém os pacotes ou digite o caminho da pasta na caixa de texto **Caminho da pasta de pacotes** e clique no botão **Atualizar** na parte inferior da página. Agora, você deve ver todos os pacotes na pasta especificada na caixa de listagem. Por padrão, todos os pacotes são selecionados. Clique na **caixa de seleção** na primeira coluna para escolher quais pacotes você quer que sejam implantados no servidor.  
  
 Consulte as colunas **Status** e **Mensagem** para verificar o status do pacote. Se o status estiver definido como **Pronto** ou **Aviso**, o assistente de implantação não bloqueará o processo de implantação. Se o status for definido como **Erro**, o assistente não prosseguirá para implantar os pacotes selecionados. Para exibir as mensagens de Aviso ou Erro detalhadas, clique no link da coluna **Mensagem**.  
  
 Se os dados confidenciais ou dados de pacote forem criptografados com uma senha, digite-a na coluna **Senha** e clique no botão **Atualizar** para verificar se ela é aceita. Se a senha estiver correta, o status mudará para **Pronto** e a mensagem de aviso desaparecerá. Se houver vários pacotes com a mesma senha, selecione os pacotes com a mesma senha de criptografia, digite a senha na caixa de texto **Senha** e selecione o botão **Aplicar**. A senha deve ser aplicada aos pacotes selecionados.  
  
 Se o status de todos os pacotes selecionados não estiver definido como **Erro**, o botão **Avançar** será habilitado para que você possa continuar com o processo de implantação do pacote.  
  
#### <a name="select-destination"></a>Selecionar Destino

 Após a seleção das origens do pacote, clique no botão **Avançar** para alternar para a página **Selecionar Destino**. Os pacotes devem ser implantados em um projeto no Catálogo do SSIS (SSISDB). Antes de implantar pacotes, verifique se o projeto de destino já existe no Catálogo do SSIS. Crie um projeto vazio se não houver um projeto. Na página **Selecionar Destino**, digite o nome do servidor na caixa de texto **Nome do Servidor** ou clique no botão **Procurar...** para selecionar uma instância de servidor. Em seguida, clique no botão **Procurar...** ao lado da caixa de texto **Caminho** para especificar o projeto de destino. Se o projeto não existir, clique no botão **Novo projeto...** para criar um projeto vazio como o projeto de destino. O projeto precisa ser criado em uma pasta.  
  
#### <a name="review-and-deploy"></a>Revisar e implantar

 Clique em **Avançar** na página **Selecionar Destino** para acessar a página **Revisar** no **Assistente de Implantação do Integration Services**. Na página de revisão, revise o relatório de resumo sobre a ação de implantação. Após a verificação, clique no botão **Implantar** para executar a ação de implantação.  
  
#### <a name="results"></a>Resultados

 Depois que a implantação estiver concluída, você deverá ver a página **Resultados** . Na página **Resultados**, examine os resultados de cada etapa no processo de implantação. Clique em **Salvar Relatório** para salvar o relatório de implantação ou em **Fechar** para fechar o assistente.  

## <a name="create-and-map-a-server-environment"></a>Criar e mapear um ambiente de servidor

  Você cria um ambiente de servidor para especificar valores de runtime para pacotes contidos em um projeto que você implantou no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Você pode mapear as variáveis de ambiente para parâmetros, para um pacote específico, para pacotes de ponto de entrada ou para todos os pacotes em um projeto específico. Um pacote de ponto de entrada é geralmente um pacote pai que executa um pacote filho.  
  
> [!IMPORTANT]  
>  Para uma execução específica, um pacote pode ser executado somente com os valores contidos em um único ambiente de servidor.  
  
 Você pode consultar as exibições para uma lista de ambientes de servidor, referências de ambiente e variáveis de ambiente. Você também pode chamar procedimentos armazenados para adicionar, excluir, alterar e modificar ambientes, referências de ambiente e variáveis de ambiente. Para obter mais informações, confira a seção **Ambientes de servidor, variáveis de servidor e referências de ambiente de servidor** no [Catálogo do SSIS](../../integration-services/catalog/ssis-catalog.md).  
  
### <a name="to-create-and-use-a-server-environment"></a>Para criar e usar um ambiente de servidor  
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], expanda o nó [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Catálogos **SSISDB** no Pesquisador de Objetos e localize a pasta **Ambientes** do projeto por meio do qual deseja criar um ambiente.  
  
2.  Clique com o botão direito do mouse na pasta **Ambientes** e clique em **Criar Ambiente**.  
  
3.  Digite um nome para o ambiente e, opcionalmente, adicione uma descrição. Clique em **OK**.  
  
4.  Clique com o botão direito do mouse no novo ambiente e clique em **Propriedades**.  
  
5.  Na página **Variáveis** , faça o seguinte para adicionar uma variável.  
  
    1.  Selecione o **Tipo** da variável. O nome da variável não precisa corresponder ao nome do parâmetro do projeto que você mapeará para a variável.  
  
    2.  Digite uma **Descrição** opcional para a variável.  
  
    3.  Digite o **Valor** para a variável de ambiente.  
  
         Para obter informações sobre as regras para nomes de variável de ambiente, consulte a seção **Variável do ambiente** em [SSIS Catalog](../../integration-services/catalog/ssis-catalog.md).  
  
    4.  Indica se a variável contém o valor confidencial, marcando ou desmarcando a caixa de seleção **Confidencial** .  
  
         Se você selecionar **Confidencial**, o valor da variável não será exibido no campo **Valor** .  
  
         Os valores confidenciais são criptografados no catálogo do SSISDB. Para obter mais informações sobre a criptografia SSL, consulte [SSIS Catalog](../../integration-services/catalog/ssis-catalog.md).  
  
6.  Na página **Permissões** , conceda ou negue permissões para usuários e funções selecionados fazendo o seguinte.  
  
    1.  Clique em **Procurar** e selecione um ou mais usuários e funções na caixa de diálogo **Procurar Todas as Entidades de Segurança** .  
  
    2.  Na área **Logons ou funções** , selecione o usuário ou função ao qual você quer conceder ou negar permissões.  
  
    3.  Na área **Explícita**, selecione **Conceder** ou **Negar** ao lado de cada permissão.  
  
7.  Para criar o script do ambiente, clique em **Script**. Por padrão, o script é exibido em uma nova janela do Editor de Consultas.  
  
    > [!TIP]  
    >  Você precisará clicar em **Script** depois de ter feito uma ou mais alterações às propriedades do ambiente, como adicionar uma variável e antes de clicar em **OK** na caixa de diálogo **Propriedades do Ambiente**. Caso contrário, um script não será gerado.  
  
8.  Clique em **OK** para salvar suas alterações nas propriedades de ambiente.  
  
9. No nó **SSISDB** no Pesquisador de Objetos, expanda a pasta **Projetos** , clique com o botão direito do mouse no projeto e, depois, clique em **Configurar**.  
  
10. Na página **Referências** , clique em **Adicionar** para adicionar um ambiente e, depois, em **OK** para salvar a referência para o ambiente.  
  
11. Clique novamente com o botão direito do mouse no projeto e clique em **Configurar**.  
  
12. Para mapear a variável de ambiente para um parâmetro adicionado ao pacote em tempo de design ou para um parâmetro gerado quando você converteu o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no modelo de implantação de projeto, faça o seguinte:
  
    1.  Na guia **Parâmetros** na página **Parâmetros** , clique no botão Procurar ao lado do campo **Valor** .  
  
    2.  Clique em **Usar variável de ambiente** e selecione a variável de ambiente que você criou.  
  
13. Para mapear a variável de ambiente para uma propriedade de gerenciador de conexões, siga os procedimentos a seguir. Os parâmetros são gerados automaticamente no servidor do SSIS para as propriedades do gerenciador de conexões.  
  
    1.  Na guia **Gerenciadores de Conexões** na página **Parâmetros**, clique no botão **Procurar** ao lado do campo **Valor**.  
  
    2.  Clique em **Usar variável de ambiente** e selecione a variável de ambiente que você criou.  
  
14. Clique em **OK** duas vezes para salvar as alterações.  

## <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>Implantar e executar pacotes SSIS usando procedimentos armazenados

  Quando configura um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para usar o modelo de implantação de projeto, você pode usar procedimentos armazenados no catálogo do [!INCLUDE[ssIS](../../includes/ssis-md.md)] para implantar o projeto e executar os pacotes. Para obter informações sobre o modelo de implantação de projeto, consulte [Implantação de projetos e pacotes](deploy-integration-services-ssis-projects-and-packages.md#compare-project-deployment-model-and-legacy-package-deployment-model).  
  
 Você também pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para implantar o projeto e executar os pacotes. Para obter mais informações, consulte os tópicos na seção **Consulte também** .  
  
> [!TIP]
>  Você pode facilmente gerar as instruções Transact-SQL para os procedimentos armazenados listados no procedimento abaixo, com exceção de catalog.deploy_project, fazendo o seguinte:
> 
>  1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó **Catálogos do Integration Services** no Pesquisador de Objetos e navegue até o pacote que deseja executar.  
> 2.  Clique com o botão direito do mouse no pacote e clique em **Executar**.  
> 3.  Conforme necessário, defina valores de parâmetros, propriedades do gerenciador de conexões e opções na guia **Avançado** , como nível de log.  
> 
>      Para obter mais informações sobre os níveis de log, veja [Habilitar o log para a execução do pacote no servidor SSIS](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
> 4.  Antes de clicar em **OK** para executar o pacote, clique em **Script**. O Transact-SQL é exibido em uma janela do Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>Para implantar e executar um pacote usando procedimentos armazenados  
  
1.  Chame [catalog.deploy_project &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md) para implantar o projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote para o servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     Para recuperar o conteúdo binário do arquivo de implantação do projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], para o parâmetro _\@project_stream_, use uma instrução SELECT com a função OPENROWSET e o provedor de conjunto de linhas BULK. O conjuntos de linhas BULK permite a você ler dados de um arquivo. O argumento SINGLE_BLOB do provedor de conjuntos de linhas BULK retorna o conteúdo do arquivo de dados como uma única linha, um conjunto de linhas de coluna única do tipo varbinary(max). Para obter mais informações, consulte [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
     No exemplo a seguir, o projeto SSISPackages_ProjectDeployment é implantado na pasta Pacotes SSIS no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Os dados binários são lidos no arquivo de projeto (SSISPackage_ProjectDeployment.ispac) e armazenados no parâmetro _\@ProjectBinary do tipo varbinary(max). O valor do parâmetro _\@ProjectBinary_ é atribuído ao parâmetro _\@project_stream_.  
  
    ```sql
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  Chame [catalog.create_execution &amp;#40;Banco de Dados SSISDB&amp;#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) para criar uma instância da execução do pacote e, opcionalmente, chame [catalog.set_execution_parameter_value &amp;#40;Banco de Dados SSISDB&amp;#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) Para definir valores de parâmetro de runtime.  
  
     No exemplo a seguir, catalog.create_execution cria uma instância de execução para package.dtsx que está contida no projeto SSISPackage_ProjectDeployment. O projeto está localizado na pasta Pacotes SSIS. A execution_id retornada pelo procedimento armazenado é usado na chamada para catalog.set_execution_parameter_value. Esse segundo procedimento armazenado define o parâmetro LOGGING_LEVEL como 3 (log detalhado) e define um parâmetro de pacote denominado Parameter1 com um valor de 1.  
  
     Para parâmetros como LOGGING_LEVEL, o valor de object_type é 50. Para parâmetros de pacote, o valor de object_type é 30.  
  
    ```sql
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  Chame [catalog.start_execution &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) para executar o pacote.  
  
     No exemplo a seguir, uma chamada a catalog.start_execution é adicionada ao Transact-SQL para iniciar a execução do pacote. A execution_id retornada pelo procedimento armazenado catalog.create_execution é usada.  
  
    ```sql
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    EXEC [SSISDB].[catalog].[start_execution] @execution_id  
    GO  
  
    ```  
  
### <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>Para implantar um projeto de servidor para servidor usando procedimentos armazenados

 Você pode implantar um projeto de servidor para servidor usando os procedimentos armazenados [catalog.get_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md) e [catalog.deploy_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md).  
  
 Você precisa fazer o seguinte antes de executar os procedimentos armazenados:  
  
-   Crie um objeto de servidor vinculado. Para obter mais informações, consulte [Criar servidores vinculados &#40;Mecanismo de Banco de Dados do SQL Server&#41;](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md).  
  
     Na página **Opções do Servidor** da caixa de diálogo **Propriedades do Servidor Vinculado** , defina **RPC** e **RPC Out** como **True**. Além disso, defina **Habilitar Promoção de Transações Distribuídas para RPC** como **False**.  
  
-   Habilite parâmetros dinâmicos para o provedor selecionado para o servidor vinculado expandindo o nó **Provedores** sob **Servidores Vinculados** no Pesquisador de Objetos, clicando com o botão direito do mouse no provedor e clicando em **Propriedades**. Selecione **Habilitar** ao lado de **Parâmetro dinâmico**.  
  
-   Confirme se o DTC (Distributed Transaction Coordinator) foi iniciado em ambos os servidores.  
  
 Chame catalog.get_project para retornar o binário do projeto e chame catalog.deploy_project. O valor retornado por catalog.get_project é inserido em uma variável de tabela do tipo varbinary(max). O servidor vinculado não pode retornar os resultados que são varbinary(max).  
  
 No exemplo a seguir, catalog.get_project retorna um binário para o projeto SSISPackages no servidor vinculado. O catalog.deploy_project implanta o projeto no servidor local, na pasta chamada DestFolder.  
  
```sql
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  

## <a name="integration-services-project-conversion-wizard"></a>Assistente de Conversão de Projeto do Integration Services
  O **Assistente de Conversão de Projeto do Integration Services** converte um projeto no modelo de implantação de projeto.  
  
> [!NOTE]  
>  Se o projeto contiver uma ou mais fontes de dados, as fontes de dados serão removidas quando a conversão de projeto estiver concluída. Para criar uma conexão com uma fonte de dados que pode ser compartilhada pelos pacotes no projeto, adicione um gerenciador de conexões no nível de projeto. Para obter mais informações, consulte [adicionar, excluir ou compartilhar um Gerenciador de Conexão em um pacote](/previous-versions/sql/sql-server-2016/ms140237(v=sql.130)).  
  
 **O que você deseja fazer?**  
  
-   [Abrir o Assistente de Conversão de Projeto do Integration Services](#open_dialog)  
  
-   [Definir opções na página Localizar Pacotes](#locate)  
  
-   [Definir opções na página Selecionar Pacotes](#selectPackages)  
  
-   [Definir opções na página Selecionar Destino](#destination)  
  
-   [Definir opções na página Especificar Propriedades do Projeto](#projectProperties)  
  
-   [Definir opções na página Atualizar a Tarefa Executar Pacote](#executePackage)  
  
-   [Definir opções na página Selecionar Configurações](#configurations)  
  
-   [Definir opções na página Criar Parâmetros](#createParameters)  
  
-   [Definir opções na página Configurar Parâmetros](#configureParameters)  
  
-   [Definir as opções na página Revisão](#review)  
  
-   [Definir as opções em Executar Conversão](#conversion)  
  
###  <a name="open-the-integration-services-project-conversion-wizard"></a><a name="open_dialog"></a> Abrir o Assistente de Conversão de Projeto do Integration Services  
 Siga um destes procedimentos para abrir o **Assistente de Conversão de Projeto do Integration Services** .  
  
-   Abra o projeto no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]e, no Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Converter em Modelo de Implantação de Projeto**.  
  
-   Por meio do Pesquisador de Objetos no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], clique com o botão direito do mouse no nó **Projetos** no **Catálogo do Integration Services** e selecione **Importar Pacotes**.  
  
 Dependendo em se você executa o **Assistente de Conversão de Projeto do Integration Services** no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o assistente executa tarefas de conversão diferentes.   
  
###  <a name="set-options-on-the-locate-packages-page"></a><a name="locate"></a> Definir opções na página Localizar Pacotes  
  
> [!NOTE]  
>   A página **Localizar Pacotes** somente está disponível quando você executa o assistente de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 A opção a seguir é exibida na página quando você seleciona **Sistema de arquivos** na lista suspensa **Origem** . Selecione esta opção quando o pacote estiver no sistema de arquivos.  
  
 **Pasta**  
 Digite o caminho do pacote ou navegue para o pacote clicando em **Procurar**.  
  
 As opções a seguir são exibidas na página quando você seleciona **Repositório de Pacotes SSIS** na lista suspensa **Origem**. Para obter mais informações sobre o repositório de pacotes, consulte [Gerenciamento de Pacotes &#40;Serviço SSIS&#41;](../../integration-services/service/package-management-ssis-service.md).  
  
 **Servidor**  
 Digite o nome do servidor ou selecione o servidor.  
  
 **Pasta**  
 Digite o caminho do pacote ou navegue para o pacote clicando em **Procurar**.  
  
 As opções a seguir são exibidas na página quando você seleciona **Microsoft SQL Server** na lista suspensa **Origem** . Selecione esta opção quando o pacote estiver no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Servidor**  
 Digite o nome do servidor ou selecione o servidor.  
  
 **Usar a autenticação do Windows**  
 O modo de Autenticação do Microsoft Windows permite que um usuário se conecte por meio de uma conta de usuário do Windows. Se usar Autenticação do Windows, não será preciso fornecer um nome de usuário nem senha.  
  
 **Usar Autenticação do SQL Server**  
 Quando um usuário se conecta com um nome de logon e senha especificados em uma conexão não confiável, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autentica a conexão verificando se foi definida uma conta de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se a senha especificada corresponde a uma senha registrada previamente. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tiver uma conta de logon definida, ocorrerá falha na autenticação e o usuário receberá uma mensagem de erro.  
  
 **Nome de usuário**  
 Especifique um nome de usuário quando você estiver usando a Autenticação do SQL Server.  
  
 **Senha**  
 Forneça uma senha quando você estiver usando a Autenticação do SQL Server.  
  
 **Pasta**  
 Digite o caminho do pacote ou navegue para o pacote clicando em **Procurar**.  
  
###  <a name="set-options-on-the-select-packages-page"></a><a name="selectPackages"></a> Definir opções na página Selecionar Pacotes  
 **Nome do Pacote**  
 Lista o arquivo do pacote.  
  
 **Status**  
 Indica se um pacote está pronto para ser convertido ao modelo de implantação de projeto.  
  
 **Message**  
 Exibe uma mensagem associada ao pacote.  
  
 **Senha**  
 Exibe uma senha associada ao pacote. O texto da senha está oculto.  
  
 **Aplicar à seleção**  
 Clique para aplicar a senha na caixa de texto **Senha** , para o pacote ou pacotes selecionados.  
  
 **Atualizar**  
 Atualiza a lista de pacotes.  
  
###  <a name="set-options-on-the-select-destination-page"></a><a name="destination"></a> Definir opções na página Selecionar Destino  
 Nessa página, especifique o nome e o caminho de um novo arquivo de implantação de projeto (.ispac) ou selecione um arquivo existente.  
  
> [!NOTE]  
>   A página **Selecionar destino** somente está disponível quando você executa o assistente de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **Caminho de saída**  
 Digite o caminho para o arquivo de implantação ou navegue para o arquivo clicando em **Procurar**.  
  
 **Nome do projeto**  
 Digite o nome do projeto.  
  
 **Nível de proteção**  
 Selecione o nível de proteção. Para obter mais informações, consulte [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md).  
  
 **Descrição do projeto**  
 Digite uma descrição opcional para o projeto.  
  
###  <a name="set-options-on-the-specify-project-properties-page"></a><a name="projectProperties"></a> Definir opções na página Especificar Propriedades do Projeto  
  
> [!NOTE]  
>   A página **Especificar Propriedades do Projeto** somente está disponível quando você executa o assistente de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 **Nome do projeto**  
 Lista o nome do projeto.  
  
 **Nível de proteção**  
 Selecione um nível de proteção para os pacotes contidos no projeto. Para obter mais informações sobre níveis de proteção, consulte [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md).  
  
 **Descrição do projeto**  
 Digite uma descrição de projeto opcional.  
  
###  <a name="set-options-on-the-update-execute-package-task-page"></a><a name="executePackage"></a> Definir opções na página Atualizar a Tarefa Executar Pacote  
 Atualizar as Tarefas Executar Pacote contidas nos pacotes, para usar uma referência baseada em projeto. Para obter mais informações, consulte [Execute Package Task Editor](../control-flow/execute-package-task.md).  
  
 **Pacote pai**  
 Lista o nome do pacote que executa o pacote filho usando a tarefa Executar Pacote.  
  
 **Nome da tarefa**  
 Lista o nome da tarefa Executar Pacote.  
  
 **Referência original**  
 Lista o caminho atual do pacote filho.  
  
 **Atribuir referência**  
 Selecione um pacote filho armazenado no projeto.  
  
###  <a name="set-options-on-the-select-configurations-page"></a><a name="configurations"></a> Definir opções na página Selecionar Configurações  
 Selecione as configurações de pacote que você deseja substituir por parâmetros.  
  
 **Pacote**  
 Lista o arquivo do pacote.  
  
 **Tipo**  
 Lista o tipo de configuração, como um arquivo de configuração XML.  
  
 **Cadeia de Caracteres de Configuração**  
 Lista o caminho do arquivo de configuração.  
  
 **Status**  
 Exibe uma mensagem de status para a configuração. Clique na mensagem para exibir o texto inteiro da mensagem.  
  
 **Adicionar configurações**  
 Adicione configurações de pacote contidas em outros projetos à lista de configurações disponíveis que você deseja substituir por parâmetros. Você pode selecionar configurações armazenadas em um sistema de arquivos ou armazenados no SQL Server.  
  
 **Atualizar**  
 Clique para atualizar a lista de configurações.  
  
 **Remover configurações de todos os pacotes após a conversão**  
 É recomendável remover todas as configurações do projeto selecionando essa opção.  
  
 Se você não selecionar essa opção, somente as configurações selecionadas para substituir por parâmetros serão removidas.  
  
###  <a name="set-options-on-the-create-parameters-page"></a><a name="createParameters"></a> Definir opções na página Criar Parâmetros  
 Selecione o nome do parâmetro e o escopo para cada propriedade de configuração.  
  
 **Pacote**  
 Lista o arquivo do pacote.  
  
 **Nome do parâmetro**  
 Lista o nome do parâmetro.  
  
 **Escopo**  
 Selecione o escopo do parâmetro, pacote ou projeto.  
  
###  <a name="set-options-on-the-configure-parameters-page"></a><a name="configureParameters"></a> Definir opções na página Configurar Parâmetros  
 **Nome**  
 Lista o nome do parâmetro.  
  
 **Escopo**  
 Lista o escopo do parâmetro.  
  
 **Valor**  
 Lista o valor do parâmetro.  
  
 Clique no botão de reticências ao lado do campo de valor para configurar as propriedades do parâmetro.  
  
 Na caixa de diálogo **Definir Detalhes de Parâmetros** , edite o valor do parâmetro. Você também pode especificar se o valor do parâmetro deve ser fornecido quando você executar o pacote.  
  
 Você pode modificar o valor na página **Parâmetros** da caixa de diálogo **Configurar** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], clique no botão Procurar ao lado do parâmetro. A caixa de diálogo **Definir Valor do Parâmetro** é exibida.  
  
 A caixa de diálogo **Definir Detalhes de Parâmetros** também lista o tipo de dados do valor de parâmetro e a origem do parâmetro.  
  
###  <a name="set-the-options-on-the-review-page"></a><a name="review"></a> Definir as opções na página Revisão  
 Use a página **Revisão** para confirmar as opções selecionadas para a conversão do projeto.  
  
 **Anterior**  
 Clique para alterar uma opção.  
  
 **Converter**  
 Clique para converter o projeto no modelo de implantação de projeto.  
  
###  <a name="set-the-options-on-the-perform-conversion"></a><a name="conversion"></a> Definir as opções em Executar Conversão  
 A página Executar Conversão mostra o status da conversão do projeto.  
  
 **Ação**  
 Lista uma etapa de conversão específica.  
  
 **Resultado**  
 Lista o status de cada etapa de conversão. Clique na mensagem de status para obter mais informações.  
  
 A conversão de projeto não será salva até que o projeto seja salvo no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 **Salvar relatório**  
 Clique para salvar um resumo da conversão de projeto em um arquivo .xml.