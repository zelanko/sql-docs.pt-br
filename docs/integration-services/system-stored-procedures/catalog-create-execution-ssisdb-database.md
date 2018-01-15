---
title: catalog.create_execution (Banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 883d6283f191827caf4de79e3f148f4680ccfe8a
ms.sourcegitcommit: 34d3497039141d043429eed15d82973b18ad90f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="catalogcreateexecution-ssisdb-database"></a>catalog.create_execution (Banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Cria uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Este procedimento armazenado usa o nível padrão de registro em log do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.create_execution [@folder_name = folder_name  
     , [@project_name =] project_name  
     , [@package_name =] package_name  
  [  , [@reference_id =] reference_id ]  
  [  , [@use32bitruntime =] use32bitruntime ] 
  [  , [@runinscaleout =] runinscaleout ]
  [  , [@useanyworker =] useanyworker ] 
     , [@execution_id =] execution_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *folder_name*  
 O nome da pasta que contém o pacote a ser executado. O *folder_name* é **nvarchar(128)**.  
  
 [@project_name =] *project_name*  
 O nome do projeto que contém o pacote a ser executado. O *project_name* é **nvarchar(128)**.  
  
 [@package_name =] *package_name*  
 O nome do pacote a ser executado. O *package_name* é **nvarchar(260)**.  
  
 [@reference_id =] *reference_id*  
 Um identificador exclusivo para uma referência do ambiente. Esse parâmetro é opcional. O *reference_id* é **bigint**.  
  
 [@use32bitruntime =] *use32bitruntime*  
 Indica se o tempo de execução de 32 bits deve ser usado para executar o pacote em um sistema operacional de 64 bits. Use o valor 1 para executar o pacote com o tempo de execução de 32 bits ao executar em um sistema operacional de 64 bits. Use o valor 0 para executar o pacote com o tempo de execução de 64 bits ao executar em um sistema operacional de 64 bits. Esse parâmetro é opcional. O *Use32bitruntime* é **bit**.  
 
 [@runinscaleout =] *runinscaleout*  
 Indique se a execução está no Scale Out. Use o valor 1 para executar o pacote no Scale Out. Use o valor 0 para executar o pacote sem o Scale Out. Esse parâmetro é opcional. Se o valor não for especificado, ele será definido como DEFAULT_EXECUTION_MODE em [SSISDB].[catalog].[catalog_properties]. O *runinscaleout* é **bit**. 
 
[@useanyworker =] *useanyworker*  
Indique se qualquer Trabalho do Scale Out tem permissão para fazer a execução.

-   Use o valor 1 para executar o pacote com qualquer Trabalho do Scale Out. Ao definir `@useanyworker` como verdadeiro, qualquer trabalho cuja contagem máxima de tarefas (conforme especificado no arquivo de configuração do trabalho) ainda não tenha sido atingida estará disponível para executar o pacote.

-   Use o valor 0 para indicar que nem todos os Trabalhos do Scale Out têm permissão para executar o pacote. Ao definir `@useanyworker` como falso, você precisará especificar os trabalhos que têm permissão para executar o pacote usando o Gerenciador do Scale Out ou chamando o procedimento armazenado `[catalog].[add_execution_worker]`.

Esse parâmetro é opcional. Se o valor não for especificado, ele será definido como 1. O *useanyworker* é **bit**. 
  
 [@execution_id =] *execution_id*  
 Retorna o identificador exclusivo de uma instância de execução. O *execution_id* é **bigint**.  

  
## <a name="remarks"></a>Remarks  
 Uma execução é usada para especificar os valores de parâmetro que um pacote usa durante uma única instância de execução do pacote.  
  
 Se uma referência de ambiente for especificada com o parâmetro *reference_id*, o procedimento armazenado populará os parâmetros de projeto e pacote com valores literais ou valores referenciados das variáveis de ambiente correspondentes. Se referência de ambiente for especificada, valores de parâmetro padrão serão usados durante a execução do pacote. Para determinar exatamente quais valores são usados para uma determinada instância de execução, use o valor de parâmetro de saída *execution_id* desse procedimento armazenado e consulte a exibição [execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md).  
  
 Somente pacotes marcados como pacotes de ponto de entrada podem ser especificados em uma execução. Se um pacote que não for ponto de entrada for especificado, a execução falhará.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir chama catalog.create_execution para criar uma instância de execução para o pacote Child1.dtsx, que não está no Scale Out. Project1 do Integration Services contém o pacote. O exemplo chama catalog.set_execution_parameter_value para definir valores para os parâmetros Parameter1, Parameter2 e LOGGING_LEVEL. O exemplo chama catalog.start_execution para iniciar uma instância de execução.  
  
```sql  
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
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e EXECUTE no projeto e, se aplicável, permissões READ no ambiente referenciado  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  

 Se @runinscaleout é 1, este procedimento armazenado exige uma das seguintes permissões:
 
-   Associação à função de banco de dados **ssis_admin**

-   Associação à função de banco de dados **ssis_cluster_executor**

-   Associação à função de servidor **sysadmin**
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar erros ou avisos:  
  
-   O pacote não existe.  
  
-   O usuário não tem as permissões apropriadas.  
  
-   A referência do ambiente, *reference_id*, não é válida.  
  
-   O pacote especificado não é um pacote de ponto de entrada.  
  
-   O tipo de dados da variável de ambiente referenciada é diferente do tipo de dados do projeto ou parâmetro de pacote.  
  
-   O projeto ou pacote contém parâmetros que requerem valores, mas nenhum valor foi atribuído.  
  
-   As variáveis de ambiente referenciadas não podem ser localizadas no ambiente especificado pela referência de ambiente *reference_id*.  
  
## <a name="see-also"></a>Consulte Também  
 [catalog.start_execution &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [catalog.add_execution_worker &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  
