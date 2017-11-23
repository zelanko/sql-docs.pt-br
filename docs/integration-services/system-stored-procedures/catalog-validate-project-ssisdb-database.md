---
title: Catalog. validate_project (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 5270689a-46d4-4847-b41f-3bed1899e955
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 83439015694f4235af4a67e994e916651ec63cc1
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogvalidateproject-ssisdb-database"></a>catalog.validate_project (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  De forma assíncrona, valida um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
catalog.validate_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @validate_type = ] validate_type  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @target_environment = ] target_environment ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nome_da_pasta*  
 O nome de uma pasta que contém o projeto. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [ @project_name =] *project_name*  
 O nome do projeto. O *project_name* é **nvarchar (128)**.  
  
 [ @validate_type =] *validate_type*  
 Indica o tipo de validação a ser executado. Use o caractere `F` para executar uma validação completa. O *validate_type* é **char (1)**.  
  
 [ @validation_id =] *validation_id*  
 Retorna o ID (identificador exclusivo) da validação. O *validation_id* é **bigint**.  
  
 [ @use32bitruntime =] *use32bitruntime*  
 Indica se o tempo de execução de 32 bits deve ser usado para executar o pacote em um sistema operacional de 64 bits. Use o valor de `1` para executar o pacote com o tempo de execução de 32 bits ao executar em um sistema operacional de 64 bits. Use o valor `0` para executar o pacote com o tempo de execução de 64 bits ao executar em um sistema operacional de 64 bits. Esse parâmetro é opcional. O *use32bitruntime* é **bit**.  
  
 [ @environment_scope =] *environment_scope*  
 Indica as referências de ambiente que são consideradas pela validação. Quando o valor for `A`, todas as referências de ambiente associadas ao projeto serão incluídas na validação. Quando o valor for `S`, apenas uma única referência de ambiente será incluída. Quando o valor for `D`, nenhuma referência de ambiente será incluída e cada parâmetro deverá ter um valor padrão literal a fim de ser aprovado na validação. Esse parâmetro é opcional, o caractere `D` será usado por padrão. O *environment_scope* é **char (1)**.  
  
 [ @reference_id =] *reference_id*  
 A ID exclusiva da referência do ambiente. Esse parâmetro é necessário somente quando uma única referência de ambiente é incluída na validação, quando *environment_scope* é `S`. O *reference_id* é **bigint**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A saída das etapas de validação é retornada como seções diferentes do conjunto de resultados.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ no projeto e, se aplicável, permissões READ nos ambientes referenciados  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir fornece algumas condições que podem gerar um erro ou um aviso:  
  
-   A validação falha para um ou mais pacotes no projeto  
  
-   A validação falhará se um ou mais dos ambientes referenciados incluídos na validação não contiverem variáveis referenciadas  
  
-   O tipo de validação especificado não é válido  
  
-   O nome do projeto ou o ID de referência de ambiente não é válido  
  
-   O usuário não tem as permissões apropriadas  
  
## <a name="remarks"></a>Comentários  
 A validação ajuda a identificar problemas que impedirão a execução bem-sucedida dos pacotes no projeto. Use o [Catalog. validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) ou [Catalog. Operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) exibições para monitorar o status de validação.  
  
 Somente ambientes acessíveis pelo usuário podem ser usados na validação. A saída de validação é enviada ao cliente como um conjunto de resultados.  
  
 Nesta versão, a validação de projeto não dá suporte para a validação de dependência.  
  
 A validação completa confirma se todas as variáveis de ambiente referenciadas são encontradas nos ambientes referenciados incluídos na validação. Os resultados da validação completa listam referências de ambiente que não são válidas e variáveis de ambiente referenciadas que não poderiam ser encontradas em nenhum dos ambientes referenciados que foram incluídos na validação.  
  
  

