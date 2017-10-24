---
title: Catalog. start_execution (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 8edb51596198f27f00c1b78ddc8b3075ad035143
ms.contentlocale: pt-br
ms.lasthandoff: 10/20/2017

---
# <a name="catalogstartexecution-ssisdb-database"></a>catalog.start_execution (Banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Inicia uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.start_execution [@execution_id =] execution_id [, [@retry_count =] retry_count]  
```  
  
## <a name="arguments"></a>Argumentos  
 [@execution_id =] *execution_id*  
 O identificador exclusivo da instância de execução. O *execution_id* é **bigint**.
 
 [@retry_count =] *contagem_novas_tentativas*  
 A contagem de repetição se a execução falhará. Ele entra em vigor somente se a execução estiver em expansão. Esse parâmetro é opcional. Se não for especificado, seu valor é definido como 0. O *contagem_de_novas_tentativas* é **int**.
  
## <a name="remarks"></a>Comentários  
 Uma execução é usada para especificar os valores de parâmetro que é usado por um pacote durante uma única instância de execução do pacote. Depois que uma instância de execução tiver sido criada e antes que ela tenha sido iniciada, o projeto correspondente deve ser reimplantado. Nesse caso, a instância de execução faz referência a um projeto que está desatualizado. Essa referência inválida faz com que o procedimento armazenado falha.  
  
> [!NOTE]  
>  As execuções podem ser iniciadas apenas uma vez. Para iniciar uma instância de execução, ele deve estar no estado criado (um valor de `1` no **status** coluna o [Catalog. Operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) exibição).  
  
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
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY na instância de execução, permissões READ e EXECUTE no projeto, e se aplicável, permissões READ no ambiente referenciado  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O usuário não tem as permissões apropriadas  
  
-   O identificador da execução não é válido  
  
-   A execução já foi iniciada ou já foi concluída; as execuções podem ser iniciadas apenas uma vez  
  
-   A referência do ambiente associada ao projeto não é válida  
  
-   Os valores do parâmetro exigido não foram definidos  
  
-   A versão do projeto associada à instância de execução está desatualizada; somente a versão mais recente de um projeto pode ser executada  
  
  

