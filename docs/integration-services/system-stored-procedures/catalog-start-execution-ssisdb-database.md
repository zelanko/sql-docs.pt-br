---
title: catalog.start_execution (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 733e71edda284d8051cc1f641ae94a3518e6b0d1
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715741"
---
# <a name="catalogstartexecution-ssisdb-database"></a>catalog.start_execution (Banco de dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Inicia uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.start_execution [@execution_id =] execution_id [, [@retry_count =] retry_count]  
```  
  
## <a name="arguments"></a>Argumentos  
 [@execution_id =] *execution_id*  
 O identificador exclusivo da instância de execução. O *execution_id* é **bigint**.
 
 [@retry_count =] *retry_count*  
 A contagem de repetições se a execução falhar. Ele entra em vigor somente se a execução estiver no Scale Out. Esse parâmetro é opcional. Se o valor não for especificado, ele será definido como 0. O *retry_count* é **int**.
  
## <a name="remarks"></a>Remarks  
 Uma execução é usada para especificar os valores de parâmetro que são usados por um pacote durante uma única instância de execução do pacote. Depois que uma instância de execução tiver sido criada e antes que ela tenha sido iniciada, o projeto correspondente deve ser reimplantado. Nesse caso, a instância de execução faz referência a um projeto que está desatualizado. Essa referência inválida faz com que o procedimento armazenado falhe.  
  
> [!NOTE]  
>  As execuções podem ser iniciadas apenas uma vez. Para iniciar uma instância de execução, ela deve estar no estado criado (um valor de `1` na coluna **status** da exibição [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md)).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir chama catalog.create_execution para criar uma instância de execução para o pacote Child1.dtsx. Project1 do Integration Services contém o pacote. O exemplo chama catalog.set_execution_parameter_value para definir valores para os parâmetros Parameter1, Parameter2 e LOGGING_LEVEL. O exemplo chama catalog.start_execution para iniciar uma instância de execução.  
  
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
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY na instância de execução, permissões READ e EXECUTE no projeto, e se aplicável, permissões READ no ambiente referenciado  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O usuário não tem as permissões apropriadas  
  
-   O identificador da execução não é válido  
  
-   A execução já foi iniciada ou já foi concluída; as execuções podem ser iniciadas apenas uma vez  
  
-   A referência do ambiente associada ao projeto não é válida  
  
-   Os valores do parâmetro exigido não foram definidos  
  
-   A versão do projeto associada à instância de execução está desatualizada; somente a versão mais recente de um projeto pode ser executada  
  
  
