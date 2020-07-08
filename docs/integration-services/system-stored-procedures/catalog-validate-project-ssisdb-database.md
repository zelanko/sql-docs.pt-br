---
title: catalog.validate_project (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 5270689a-46d4-4847-b41f-3bed1899e955
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c4180093e97237b5b433714ad437447065235e54
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85673643"
---
# <a name="catalogvalidate_project-ssisdb-database"></a>catalog.validate_project (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  De forma assíncrona, valida um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
catalog.validate_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @validate_type = ] validate_type  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @environment_scope = ] environment_scope ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome de uma pasta que contém o projeto. O *folder_name* é **nvarchar(128)** .  
  
 [ @project_name = ] *project_name*  
 O nome do projeto. O *project_name* é **nvarchar(128)** .  
  
 [ @validate_type = ] *validate_type*  
 Indica o tipo de validação a ser executado. Use o caractere `F` para executar uma validação completa. Esse parâmetro é opcional, o caractere `F` será usado por padrão. O *validate_type* é **char(1)** .  
  
 [ @validation_id = ] *validation_id*  
 Retorna o ID (identificador exclusivo) da validação. O *validation_id* é **bigint**.  
  
 [ @use32bitruntime = ] *use32bitruntime*  
 Indica se o runtime de 32 bits deve ser usado para executar o pacote em um sistema operacional de 64 bits. Use o valor `1` para executar o pacote com o runtime de 32 bits ao executar em um sistema operacional de 64 bits. Use o valor `0` para executar o pacote com o runtime de 64 bits ao executar em um sistema operacional de 64 bits. Esse parâmetro é opcional. O *use32bitruntime* é **bit**.  
  
 [ @environment_scope = ] *environment_scope*  
 Indica as referências de ambiente que são consideradas pela validação. Quando o valor for `A`, todas as referências de ambiente associadas ao projeto serão incluídas na validação. Quando o valor for `S`, apenas uma única referência de ambiente será incluída. Quando o valor for `D`, nenhuma referência de ambiente será incluída e cada parâmetro deverá ter um valor padrão literal a fim de ser aprovado na validação. Esse parâmetro é opcional, o caractere `D` será usado por padrão. O *environment_scope* é **char(1)** .  
  
 [ @reference_id = ] *reference_id*  
 A ID exclusiva da referência do ambiente. Esse parâmetro é necessário apenas quando uma única referência de ambiente é incluída na validação, quando *environment_scope* é `S`. O *reference_id* é **bigint**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A saída das etapas de validação é retornada como seções diferentes do conjunto de resultados.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ no projeto e, se aplicável, permissões READ nos ambientes referenciados  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir fornece algumas condições que podem gerar um erro ou um aviso:  
  
-   A validação falha para um ou mais pacotes no projeto  
  
-   A validação falhará se um ou mais dos ambientes referenciados incluídos na validação não contiverem variáveis referenciadas  
  
-   O tipo de validação especificado não é válido  
  
-   O nome do projeto ou o ID de referência de ambiente não é válido  
  
-   O usuário não tem as permissões apropriadas  
  
## <a name="remarks"></a>Comentários  
 A validação ajuda a identificar problemas que impedirão a execução bem-sucedida dos pacotes no projeto. Use as exibições [catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) ou [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) para monitorar o status da validação.  
  
 Somente ambientes acessíveis pelo usuário podem ser usados na validação. A saída de validação é enviada ao cliente como um conjunto de resultados.  
  
 Nesta versão, a validação de projeto não dá suporte para a validação de dependência.  
  
 A validação completa confirma se todas as variáveis de ambiente referenciadas são encontradas nos ambientes referenciados incluídos na validação. Os resultados da validação completa listam referências de ambiente que não são válidas e variáveis de ambiente referenciadas que não poderiam ser encontradas em nenhum dos ambientes referenciados que foram incluídos na validação.  
  
  
