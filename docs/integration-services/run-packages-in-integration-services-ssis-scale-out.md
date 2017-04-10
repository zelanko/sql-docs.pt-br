---
title: "Executar pacotes na Expans&#227;o do Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f4cd7-9c47-416d-bb1e-40acc3e05342
caps.latest.revision: 5
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 5
---
# Executar pacotes na Expans&#227;o do Integration Services (SSIS)
Depois que os pacotes são implantados no servidor Integration Services, você pode executá-los em Expansão.

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>Executar pacotes com a caixa de diálogo **Executar Pacote em Expansão** 

1. ### <a name="open-the-execute-package-in-scale-out-dialog-box"></a>Abra a caixa de diálogo Executar pacote em Expansão ###
    Em [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do Integration Services. No Pesquisador de Objetos, expanda a árvore para exibir os nós em **Catálogos do Integration Services**. Clique com botão direito do mouse no nó, projeto ou pacote **SSISDB** que você deseja executar e, em seguida, clique em **Executar na Expansão**.
2. ### <a name="select-packages-and-set-the-options"></a>Selecionar pacotes e definir as opções ###
    Na página de **Seleção de pacote** você seleciona vários pacotes para executar e define o ambiente, os parâmetros, os gerenciadores de conexão e as opções avançadas para cada pacote. Clique em um pacote para definir essas opções.
    
    Na guia **Avançado**, você define uma opção de Expansão chamada **Contagem de repetição**. Isso define o número de vezes que uma execução de pacote tentará executar novamente se a execução falhar.
3. ### <a name="select-machines"></a>Selecionar computadores ###
    Na página **Seleção de Computador**, você seleciona os computadores Trabalho de Expansão para executar os pacotes. Por padrão, qualquer computador tem permissão para executar os pacotes. 

   > [!NOTE]
> Os pacotes são executados com a credencial das contas de usuário dos serviços Trabalho de Expansão, que são mostrados na página de **Seleção de Computador**. Por padrão, a conta é NT Service\SSISScaleOutWorker140. Você talvez queira alterar para suas próprias contas de laboratório.

4. ### <a name="run-the-packages-and-view-reports"></a>Executar os pacotes e exibir os relatórios 
    Clique em **OK** para iniciar as execuções de pacote. Para exibir o relatório de execução de um pacote, clique com o botão direito do mouse no pacote em Pesquisador de Objetos, clique em **Relatórios**, clique em **Todas as Execuções** e encontre a execução.
    
    
## <a name="run-packages-with-stored-procedures"></a>Executar pacotes com procedimentos armazenados

1. ### <a name="create-executions"></a>Criar execuções ###
    Chamar [catalog].[create_execution] para cada pacote. Definir o parâmetro **@runincluster** como Verdadeiro. Se nem todos os computadores de Trabalho de Expansão tiverem permissão para executar o pacote, defina o parâmetro ** @useanyworker** como False.   
2. ### <a name="set-execution-parameters"></a>Definir os parâmetros de execução ###
    Chamar [catalog].[set_execution_parameter_value] para cada execução.
3. ### <a name="set-scale-out-workers"></a>Definir os Trabalhos de Expansão ###
    Chamar [catalog].[add_execution_worker]. Se qualquer computador tiver permissão para executar o pacote, você não precisará chamar esse procedimento armazenado. 
4. ### <a name="start-executions"></a>Iniciar execuções ###
    Chamar [catalog].[start_execution]. Definir o parâmetro **@retry_count** para definir o número de vezes que uma execução de pacote tentará executar novamente se a execução falhar.
    
    ### <a name="example"></a>Exemplo  ###  
    O exemplo a seguir executa dois pacotes, package1.dtsx e package2.dtsx, na Expansão com um Trabalho de Expansão.  
    ```
    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO

    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO
    ```


## <a name="permissions"></a>Permissões
A execução de pacotes na Expansão exige uma das seguintes permissões:

-   Associação na função de banco de dados **ssis_admin**  

-   Associação na função de banco de dados **ssis_cluster_executor**  
  
-   Associação na função de servidor **sysadmin**  
    