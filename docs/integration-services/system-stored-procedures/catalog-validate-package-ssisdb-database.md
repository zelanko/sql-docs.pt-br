---
title: Catalog. validate_package (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- validate_package stored procedure [Integration Services]
- catalog.validate_package stored procedure [Integration Services]
ms.assetid: 0dc03df1-b793-408f-af4c-c11188729abf
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8b4dbd030c457bfb90ac4ec7fae886de28f96854
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogvalidatepackage-ssisdb-database"></a>catalog.validate_package (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  De forma assíncrona, valida um pacote no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
validate_package [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @package_name = ] package_name  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @target_environment = ] target_environment ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nome_da_pasta*  
 O nome da pasta que contém o pacote. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [ @project_name =] *project_name*  
 O nome do projeto que contém o pacote. O *project_name* é **nvarchar (128)**.  
  
 [ @package_name =] *nome_do_pacote*  
 O nome do pacote. O *nome_do_pacote* é **nvarchar (260)**.  
  
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
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ no projeto e, se aplicável, permissões READ nos ambientes referenciados  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O nome do projeto ou pacote não é válido.  
  
-   O usuário não tem as permissões apropriadas  
  
-   Um ou mais dos ambientes referenciados incluído na validação não contêm variáveis referenciadas  
  
-   Há falha na validação do pacote  
  
-   O ambiente referenciado não existe  
  
-   As variáveis referenciadas não podem ser localizadas nos ambientes referenciados incluídos na validação  
  
-   As variáveis são referenciadas nos parâmetros de pacote, mas nenhum ambiente referenciado foi incluído na validação  
  
## <a name="remarks"></a>Comentários  
 A validação ajuda a identificar problemas que impedirão a execução bem-sucedida do pacote. Use o [Catalog. validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) ou [Catalog. Operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) exibições para monitorar o status de validação.  
  
  
