---
title: Executar pacotes no SSIS (SQL Server Integration Services) Scale Out | Microsoft Docs
ms.description: This article describes how to run SSIS packages in Scale Out
ms.custom: 
ms.date: 12/13/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: douglasl
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: craigg
f1_keywords: sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.workload: Inactive
ms.openlocfilehash: 091d67122b07e8787ccfce914236a4ff9f793b27
ms.sourcegitcommit: 4dab7c60fb66d61074057eb1cee73f9b24751a8f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2017
---
# <a name="run-packages-in-integration-services-ssis-scale-out"></a>Executar pacotes no SSIS (Integration Services) Scale Out
Depois de implantar pacotes no servidor do Integration Services, execute-os no Scale Out usando um dos seguintes métodos:

-   [Caixa de diálogo Executar Pacote no Scale Out](#scale_out_dialog)

-   [Procedimentos armazenados](#stored_proc)

-   [trabalhos do SQL Server Agent](#sql_agent)

## <a name="scale_out_dialog"></a> Executar pacotes com a caixa de diálogo Executar Pacote no Scale Out

1. Abra a caixa de diálogo Executar Pacote no Scale Out.

    Em [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do Integration Services. No Pesquisador de Objetos, expanda a árvore para exibir os nós em **Catálogos do Integration Services**. Clique com botão direito do mouse no nó, projeto ou pacote **SSISDB** que você deseja executar e, em seguida, clique em **Executar na Expansão**.

2. Selecione os pacotes e defina as opções.

    Na página **Seleção de Pacote**, selecione um ou mais pacotes a serem executados. Defina o ambiente, os parâmetros, os gerenciadores de conexões e as opções avançadas de cada pacote. Clique em um pacote para definir essas opções.
    
    Na guia **Avançado**, defina uma opção do Scale Out chamada **Contagem de repetição** para especificar o número de vezes que uma execução de pacote tentará executar novamente em caso de falha.

    > [!NOTE]
    > A opção **Despejar quando ocorrerem erros** só funcionará quando a conta que executa o serviço Trabalho do Scale Out for um administrador no computador local.

3. Selecione os computadores de trabalho.

    Na página **Seleção de Computador**, selecione os computadores do Trabalho do Scale Out para executar os pacotes. Por padrão, qualquer computador tem permissão para executar os pacotes. 

   > [!NOTE] 
   > Os pacotes são executados com as credenciais das contas de usuário dos serviços Trabalho do Scale Out. Examine essas credenciais na página **Seleção de Computador**. Por padrão, a conta é `NT Service\SSISScaleOutWorker140`.

   > [!WARNING]
   > Execuções de pacote disparadas por usuários diferentes no mesmo trabalho são executadas com as mesmas credenciais. Não há nenhum limite de segurança entre elas. 

4. Execute os pacotes e exiba os relatórios.

    Clique em **OK** para iniciar as execuções de pacote. Para exibir o relatório de execução de um pacote, clique com o botão direito do mouse no pacote em Pesquisador de Objetos, clique em **Relatórios**, clique em **Todas as Execuções**e encontre a execução.
    
## <a name="stored_proc"></a> Executar pacotes com procedimentos armazenados

1.  Crie execuções.

    Chame `[catalog].[create_execution]` para cada pacote. Defina o parâmetro **@runinscaleout** como `True`. Se nem todos os computadores do Trabalho do Scale Out tiverem permissão para executar o pacote, defina o parâmetro **@useanyworker** como `False`.   

2. Defina os parâmetros de execução.

    Chame `[catalog].[set_execution_parameter_value]` para cada execução.

3. Defina os Trabalhos do Scale Out.

    Chame `[catalog].[add_execution_worker]`. Se todos os computadores tiverem permissão para executar o pacote, não será necessário chamar esse procedimento armazenado. 

4. Inicie as execuções.

    Chame `[catalog].[start_execution]`. Defina o parâmetro **@retry_count** para definir o número de vezes que uma execução de pacote tentará executar novamente em caso de falha.
    
### <a name="example"></a>Exemplo
O exemplo a seguir executa dois pacotes, `package1.dtsx` e `package2.dtsx`, no Scale Out com um Trabalho do Scale Out.  

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
Para executar pacotes no Scale Out, você deve ter uma das seguintes permissões:

-   Associação na função de banco de dados **ssis_admin**  

-   Associação na função de banco de dados **ssis_cluster_executor**  
  
-   Associação na função de servidor **sysadmin**  

## <a name="set-default-execution-mode"></a>Definir modo de execução padrão
Para definir o modo de execução padrão de pacotes como **Scale Out**, faça o seguinte:

1.  No SSMS, no Pesquisador de Objetos, clique com o botão direito do mouse no nó **SSISDB** e selecione **Propriedades**.

2.  Na caixa de diálogo **Propriedades do Catálogo**, defina **Modo de execução Padrão de todo o servidor** como **Scale Out**.

Depois de definir esse modo de execução padrão, não é mais necessário especificar o parâmetro **@runinscaleout** ao chamar o procedimento armazenado `[catalog].[create_execution]`. Os pacotes são executados no Scale Out automaticamente. 

![Modo de exe](media\exe-mode.PNG)

Para alternar o modo de execução padrão novamente para que os pacotes não sejam mais executados por padrão no modo do Scale Out, defina **Modo de execução Padrão de todo o servidor** como **Servidor**.

## <a name="sql_agent"></a> Executar pacote em um trabalho do SQL Server Agent
Em um trabalho do SQL Server Agent, você pode executar um pacote do SSIS como uma etapa do trabalho. Para executar o pacote no Scale Out, defina o modo de execução padrão como **Scale Out**. Depois de definir o modo de execução padrão como **Scale Out**, os pacotes em trabalhos do SQL Server Agent serão executados no modo do Scale Out.

## <a name="next-steps"></a>Próximas etapas
-   [Solucionar problemas do Scale Out](troubleshooting-scale-out.md)
