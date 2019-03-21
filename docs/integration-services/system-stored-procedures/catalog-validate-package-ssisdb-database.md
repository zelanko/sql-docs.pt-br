---
title: catalog.validate_package (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- validate_package stored procedure [Integration Services]
- catalog.validate_package stored procedure [Integration Services]
ms.assetid: 0dc03df1-b793-408f-af4c-c11188729abf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: befdec64de1b12370eea84a64cb8502172a4d3b3
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57974075"
---
# <a name="catalogvalidatepackage-ssisdb-database"></a>catalog.validate_package (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  De forma assíncrona, valida um pacote no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
catalog.validate_package [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @package_name = ] package_name  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @environment_scope = ] environment_scope ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que contém o pacote. O *folder_name* é **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 O nome do projeto que contém o pacote. O *project_name* é **nvarchar(128)**.  
  
 [ @package_name = ] *package_name*  
 O nome do pacote. O *package_name* é **nvarchar(260)**.  
  
 [ @validation_id = ] *validation_id*  
 Retorna o ID (identificador exclusivo) da validação. O *validation_id* é **bigint**.  
  
 [ @use32bitruntime = ] *use32bitruntime*  
 Indica se o tempo de execução de 32 bits deve ser usado para executar o pacote em um sistema operacional de 64 bits. Use o valor `1` para executar o pacote com o tempo de execução de 32 bits ao executar em um sistema operacional de 64 bits. Use o valor `0` para executar o pacote com o tempo de execução de 64 bits ao executar em um sistema operacional de 64 bits. Esse parâmetro é opcional. O *use32bitruntime* é **bit**.  
  
 [ @environment_scope = ] *environment_scope*  
 Indica as referências de ambiente que são consideradas pela validação. Quando o valor for `A`, todas as referências de ambiente associadas ao projeto serão incluídas na validação. Quando o valor for `S`, apenas uma única referência de ambiente será incluída. Quando o valor for `D`, nenhuma referência de ambiente será incluída e cada parâmetro deverá ter um valor padrão literal a fim de ser aprovado na validação. Esse parâmetro é opcional. O caractere `D` é usado por padrão. O *environment_scope* é **char(1)**.  
  
 [ @reference_id = ] *reference_id*  
 A ID exclusiva da referência do ambiente. Esse parâmetro é necessário apenas quando uma única referência de ambiente é incluída na validação, quando *environment_scope* é `S`. O *reference_id* é **bigint**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ no projeto e, se aplicável, permissões READ nos ambientes referenciados  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O nome do projeto ou pacote não é válido.  
  
-   O usuário não tem as permissões apropriadas  
  
-   Um ou mais dos ambientes referenciados incluído na validação não contêm variáveis referenciadas  
  
-   Há falha na validação do pacote  
  
-   O ambiente referenciado não existe  
  
-   As variáveis referenciadas não podem ser localizadas nos ambientes referenciados incluídos na validação  
  
-   As variáveis são referenciadas nos parâmetros de pacote, mas nenhum ambiente referenciado foi incluído na validação  
  
## <a name="remarks"></a>Remarks  
 A validação ajuda a identificar problemas que podem impedir a execução bem-sucedida do pacote. Use as exibições [catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) ou [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) para monitorar o status da validação.  
  
  
