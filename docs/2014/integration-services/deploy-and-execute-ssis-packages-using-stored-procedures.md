---
title: Implantar e executar pacotes SSIS usando procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 60914b0c-1f65-45f8-8132-0ca331749fcc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 56141595c62e5190bf3ef797059acd602f801ed7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059611"
---
# <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>Implantar e executar pacotes SSIS usando procedimentos armazenados
  Quando configura um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para usar o modelo de implantação de projeto, você pode usar procedimentos armazenados no catálogo do [!INCLUDE[ssIS](../includes/ssis-md.md)] para implantar o projeto e executar os pacotes. Para obter informações sobre o modelo de implantação de projeto, consulte [Implantação de projetos e pacotes](packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Você também pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para implantar o projeto e executar os pacotes. Para obter mais informações, consulte os tópicos na seção **Consulte também** .  
  
> [!TIP]
>  Você pode facilmente gerar as instruções Transact-SQL para os procedimentos armazenados listados no procedimento abaixo, com exceção de catalog.deploy_project, fazendo o seguinte:  
> 
>  1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], expanda o nó **Catálogos do Integration Services** no Pesquisador de Objetos e navegue até o pacote que deseja executar.  
> 2.  Clique com o botão direito do mouse no pacote e clique em **Executar**.  
> 3.  Conforme necessário, defina valores de parâmetros, propriedades do gerenciador de conexões e opções na guia **Avançado** , como nível de log.  
> 
>      Para obter mais informações sobre os níveis de log, veja [Habilitar o log para a execução do pacote no servidor SSIS](../../2014/integration-services/enable-logging-for-package-execution-on-the-ssis-server.md).  
> 4.  Antes de clicar em **OK** para executar o pacote, clique em **Script**. O Transact-SQL é exibido em uma janela do Editor de Consultas no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
## <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>Para implantar e executar um pacote usando procedimentos armazenados  
  
1.  Chame [catalog.deploy_project &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database) para implantar o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote para o servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
     Para recuperar o conteúdo binário do arquivo de implantação do projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , para o parâmetro *@project_stream* , use uma instrução SELECT com a função OPENROWSET e o provedor de conjunto de linhas BULK. O conjuntos de linhas BULK permite a você ler dados de um arquivo. O argumento SINGLE_BLOB do provedor de conjuntos de linhas BULK retorna o conteúdo do arquivo de dados como uma única linha, um conjunto de linhas de coluna única do tipo varbinary(max). Para obter mais informações, consulte [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
     No exemplo a seguir, o projeto SSISPackages_ProjectDeployment é implantado na pasta Pacotes SSIS no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Os dados binários são lidos no arquivo de projeto (SSISPackage_ProjectDeployment.ispac) e armazenados no parâmetro *@ProjectBinary* do tipo varbinary(max). O valor do parâmetro *@ProjectBinary* é atribuído ao parâmetro *@project_stream* .  
  
    ```  
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  Chame [catalog.create_execution &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) para criar uma instância da execução do pacote e, opcionalmente, chame [catalog.set_execution_parameter_value &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) Para definir valores de parâmetro de tempo de execução.  
  
     No exemplo a seguir, catalog.create_execution cria uma instância de execução para package.dtsx que está contida no projeto SSISPackage_ProjectDeployment. O projeto está localizado na pasta Pacotes SSIS. A execution_id retornada pelo procedimento armazenado é usado na chamada para catalog.set_execution_parameter_value. Esse segundo procedimento armazenado define o parâmetro LOGGING_LEVEL como 3 (log detalhado) e define um parâmetro de pacote denominado Parameter1 com um valor de 1.  
  
     Para parâmetros como LOGGING_LEVEL, o valor de object_type é 50. Para parâmetros de pacote, o valor de object_type é 30.  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  Chame [catalog.start_execution &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) para executar o pacote.  
  
     No exemplo a seguir, uma chamada a catalog.start_execution é adicionada ao Transact-SQL para iniciar a execução do pacote. A execution_id retornada pelo procedimento armazenado catalog.create_execution é usada.  
  
    ```  
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
  
## <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>Para implantar um projeto de servidor para servidor usando procedimentos armazenados  
 Você pode implantar um projeto de servidor para servidor usando os procedimentos armazenados [catalog.get_project &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database) e [catalog.deploy_project &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database).  
  
 Você precisa fazer o seguinte antes de executar os procedimentos armazenados:  
  
-   Crie um objeto de servidor vinculado. Para obter mais informações, consulte [Criar servidores vinculados &#40;Mecanismo de Banco de Dados do SQL Server&#41;](../database-engine/sql-server-database-engine-overview.md).  
  
     Na página **Opções do Servidor** da caixa de diálogo **Propriedades do Servidor Vinculado**, defina **RPC** e **RPC Out** como **True**. Além disso, defina **Habilitar Promoção de Transações Distribuídas para RPC** como **False**.  
  
-   Habilite parâmetros dinâmicos para o provedor selecionado para o servidor vinculado expandindo o nó **Provedores** sob **Servidores Vinculados** no Pesquisador de Objetos, clicando com o botão direito do mouse no provedor e clicando em **Propriedades**. Selecione **Habilitar** ao lado de **Parâmetro dinâmico**.  
  
-   Confirme se o DTC (Distributed Transaction Coordinator) foi iniciado em ambos os servidores.  
  
 Chame catalog.get_project para retornar o binário do projeto e chame catalog.deploy_project. O valor retornado por catalog.get_project é inserido em uma variável de tabela do tipo varbinary(max). O servidor vinculado não pode retornar os resultados que são varbinary(max).  
  
 No exemplo a seguir, catalog.get_project retorna um binário para o projeto SSISPackages no servidor vinculado. O catalog.deploy_project implanta o projeto no servidor local, na pasta chamada DestFolder.  
  
```  
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Implantar projetos no Servidor do Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [Executar um pacote nas Ferramentas de Dados do SQL Server](../../2014/integration-services/run-a-package-in-sql-server-data-tools.md)   
 [Executar um pacote no servidor SSIS usando o SQL Server Management Studio](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
  
