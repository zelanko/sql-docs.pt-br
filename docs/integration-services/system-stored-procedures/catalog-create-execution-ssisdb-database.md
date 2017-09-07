---
title: Catalog. create_execution (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 95c07e2550330ff9a2ac1cc70107d11147ae53dd
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="catalogcreateexecution-ssisdb-database"></a>catalog.create_execution (Banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Cria uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Este procedimento armazenado usa o nível padrão de registro em log do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```tsql  
create_execution [ @folder_name = folder_name  
     , [ @project_name = ] project_name  
     , [ @package_name = ] package_name  
  [  , [ @reference_id = ] reference_id ]  
  [  , [ @use32bitruntime = ] use32bitruntime ] 
  [  , [ @runinscaleout = ] runinscaleout ]
  [  , [ @useanyworker = ] useanyworker ] 
     , [ @execution_id = ] execution_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nome_da_pasta*  
 O nome da pasta que contém o pacote a ser executado. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [ @project_name =] *project_name*  
 O nome do projeto que contém o pacote a ser executado. O *project_name* é **nvarchar (128)**.  
  
 [ @package_name =] *nome_do_pacote*  
 O nome do pacote a ser executado. O *nome_do_pacote* é **nvarchar (260)**.  
  
 [ @reference_id =] *reference_id*  
 Um identificador exclusivo para uma referência do ambiente. Esse parâmetro é opcional. O *reference_id* é **bigint**.  
  
 [ @use32bitruntime =] *use32bitruntime*  
 Indica se o tempo de execução de 32 bits deve ser usado para executar o pacote em um sistema operacional de 64 bits. Use o valor de 1 para executar o pacote com o tempo de execução de 32 bits ao executar em um sistema operacional de 64 bits. Use o valor 0 para executar o pacote com o tempo de execução de 64 bits ao executar em um sistema operacional de 64 bits. Esse parâmetro é opcional. O *Use32bitruntime* é **bit**.  
 
 [ @runinscaleout =] *runinscaleout*  
 Indica se a execução em expansão. Use o valor de 1 para executar o pacote de expansão. Use o valor de 0 para executar o pacote sem expansão. Esse parâmetro é opcional. Ele é definido como DEFAULT_EXECUTION_MODE em [SSISDB]. [catalog]. [catalog_properties], se não for especificado. O *runinscaleout* é **bit**. 
 
 [ @useanyworker =] *useanyworker*  
  Indique se qualquer escala Out trabalhador tem permissão para fazer a execução. Use o valor de 1 para executar o pacote com qualquer escala Out trabalhador. Use o valor de 0 para indicar que a escala não todos os Out trabalhadores são permitidos para executar o pacote. Esse parâmetro é opcional. Ele é definido como 1, se não for especificado. O *useanyworker* é **bit**. 
  
 [ @execution_id =] *execution_id*  
 Retorna o identificador exclusivo de uma instância de execução. O *execution_id* é **bigint**.  

  
## <a name="remarks"></a>Comentários  
 Uma execução é usada para especificar os valores de parâmetro que um pacote usa durante uma única instância de execução do pacote.  
  
 Se uma referência de ambiente for especificada com o *reference_id* parâmetro, o procedimento armazenado preenche os parâmetros de projeto e pacote com valores literais ou valores referenciados das variáveis de ambiente correspondente. Se referência de ambiente for especificada, valores de parâmetro padrão serão usados durante a execução do pacote. Para determinar exatamente quais valores são usados para uma determinada instância de execução, use o *execution_id* valor de parâmetro desse procedimento armazenado e a consulta de saída a [execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) exibição.  
  
 Somente pacotes marcados como pacotes de ponto de entrada podem ser especificados em uma execução. Se um pacote que não for ponto de entrada for especificado, a execução falhará.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir chama Catalog. create_execution para criar uma instância de execução para o pacote child1, que não está em expansão. Project1 do Integration Services contém o pacote. O exemplo chama catalog.set_execution_parameter_value para definir valores para os parâmetros Parameter1, Parameter2 e LOGGING_LEVEL. O exemplo chama catalog.start_execution para iniciar uma instância de execução.  
  
```  
Declare @execution_id bigint  
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Child1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'TestDeply4', @project_name=N'Integration Services Project1', @use32bitruntime=False, @reference_id=Null  
Select @execution_id  
DECLARE @var0 sql_variant = N'Child1.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter1', @parameter_value=@var0  
DECLARE @var1 sql_variant = N'Child2.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter2', @parameter_value=@var1  
DECLARE @var2 smallint = 1  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var2  
EXEC [SSISDB].[catalog].[start_execution] @execution_id  
GO  
  
```  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e EXECUTE no projeto e, se aplicável, permissões READ no ambiente referenciado  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  

 Se @runinscaleout for 1, o procedimento armazenado requer uma das seguintes permissões:
 
-   Associação de **ssis_admin** função de banco de dados

-   Associação de **ssis_cluster_executor** função de banco de dados

-   Associação de **sysadmin** função de servidor
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar erros ou avisos:  
  
-   O pacote não existe.  
  
-   O usuário não tem as permissões apropriadas.  
  
-   A referência de ambiente *reference_id*, não é válido.  
  
-   O pacote especificado não é um pacote de ponto de entrada.  
  
-   O tipo de dados da variável de ambiente referenciada é diferente do tipo de dados do projeto ou parâmetro de pacote.  
  
-   O projeto ou pacote contém parâmetros que requerem valores, mas nenhum valor foi atribuído.  
  
-   As variáveis de ambiente referenciado não foi encontradas no ambiente de pela referência de ambiente *reference_id*, especifica.  
  
## <a name="see-also"></a>Consulte também  
 [Catalog. start_execution &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [Catalog.add_execution_worker &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  

