---
title: "Expansão de executar pacotes no SQL Server Integration Services (SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
f1_keywords:
- sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2c158ae6a711ecb5f5065561c0c8c303e9a09980
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---

# <a name="run-packages-in-integration-services-ssis-scale-out"></a>Executar pacotes no Integration Services (SSIS) expansão
Depois que os pacotes são implantados no servidor Integration Services, você pode executá-los em Expansão.

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>Executar pacotes com a caixa de diálogo Executar pacote em expansão 

1. Abra a caixa de diálogo Executar pacote em Expansão

    Em [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do Integration Services. No Pesquisador de Objetos, expanda a árvore para exibir os nós em **Catálogos do Integration Services**. Clique com botão direito do mouse no nó, projeto ou pacote **SSISDB** que você deseja executar e, em seguida, clique em **Executar na Expansão**.

2. Selecionar pacotes e definir as opções

    Na página de **Seleção de pacote** você seleciona vários pacotes para executar e define o ambiente, os parâmetros, os gerenciadores de conexão e as opções avançadas para cada pacote. Clique em um pacote para definir essas opções.
    
    Na guia **Avançado** , você define uma opção de Expansão chamada **Contagem de repetição**. Isso define o número de vezes que uma execução de pacote tentará executar novamente se a execução falhar.

    > [!Note]
    > O **despejar quando ocorrerem erros** opção só entrará em vigor quando a conta que executa o serviço de escala fora do trabalho é um administrador do computador local.

3. Selecionar computadores

    Na página **Seleção de Computador** , você seleciona os computadores Trabalho de Expansão para executar os pacotes. Por padrão, qualquer computador tem permissão para executar os pacotes. 

   > [!Note] 
   > Os pacotes são executados com a credencial das contas de usuário dos serviços Trabalho de Expansão, que são mostrados na página de **Seleção de Computador** . Por padrão, a conta é NT Service\SSISScaleOutWorker140. Você talvez queira alterar para suas próprias contas de laboratório.

   >[!WARNING]
   >Execuções de pacote disparadas por usuários diferentes no mesmo trabalhador são executadas com a mesma conta. Não há nenhum limite de segurança entre eles. 

4. Executar os pacotes e exibir os relatórios 

    Clique em **OK** para iniciar as execuções de pacote. Para exibir o relatório de execução de um pacote, clique com o botão direito do mouse no pacote em Pesquisador de Objetos, clique em **Relatórios**, clique em **Todas as Execuções**e encontre a execução.
    
## <a name="run-packages-with-stored-procedures"></a>Executar pacotes com procedimentos armazenados

1. Criar execuções

    Chamar [catalog].[create_execution] para cada pacote. Definir o parâmetro **@runinscaleout** como Verdadeiro. Se nem todos os computadores de Trabalho de Expansão tiverem permissão para executar o pacote, defina o parâmetro **@useanyworker** como False.   

2. Definir os parâmetros de execução

    Chamar [catalog].[set_execution_parameter_value] para cada execução.

3. Definir os Trabalhos de Expansão

    Chamar [catalog].[add_execution_worker]. Se qualquer computador tiver permissão para executar o pacote, você não precisará chamar esse procedimento armazenado. 

4. Iniciar execuções

    Chamar [catalog].[start_execution]. Definir o parâmetro **@retry_count** para definir o número de vezes que uma execução de pacote tentará executar novamente se a execução falhar.
    
#### <a name="example"></a>Exemplo
O exemplo a seguir executa dois pacotes, package1.dtsx e package2.dtsx, na Expansão com um Trabalho de Expansão.  

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO

Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO
```

### <a name="permissions"></a>Permissões
A execução de pacotes na Expansão exige uma das seguintes permissões:

-   Associação na função de banco de dados **ssis_admin**  

-   Associação na função de banco de dados **ssis_cluster_executor**  
  
-   Associação na função de servidor **sysadmin**  

## <a name="set-default-execution-mode"></a>Modo de execução do conjunto de padrão
Para definir o modo de execução padrão para "Expansão", com o botão direito do **SSISDB** nó no Pesquisador de objetos do SSMS e selecione **propriedades**.
No **propriedades de catálogo** caixa de diálogo, defina **modo de execução de todo o servidor padrão** para **expansão**.

Após essa configuração, não é necessário especificar o  **@runinscaleout**  parâmetro [catalog]. [ create_execution]. Execuções são executadas automaticamente em expansão. 

![Modo de exe](media\exe-mode.PNG)

Para alternar o modo de execução padrão para o modo de não - expansão, basta definir **modo de execução de todo o servidor padrão** para **Server**.

## <a name="run-package-in-sql-agent-job"></a>Executar o pacote no trabalho do SQL agent
No trabalho do Sql agent, você pode optar por executar um pacote SSIS como uma etapa do trabalho. Para executar o pacote de expansão, você pode aproveitar o modo de execução padrão acima. Depois de configurar o modo de execução de padrão de "Expansão", pacotes em trabalhos do Sql agent serão executados em expansão.

