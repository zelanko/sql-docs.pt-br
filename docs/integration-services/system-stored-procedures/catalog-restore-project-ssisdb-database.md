---
title: catalog.restore_project (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 8adee525-579b-4d2f-b807-e2ecc07fb2e9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af878e23862e791443ad0057997cf93d0eab8ca1
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715988"
---
# <a name="catalogrestoreproject-ssisdb-database"></a>catalog.restore_project (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restaura um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para uma versão anterior.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.restore_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project _name  
    , [ @object_version_lsn = ] object_version_lsn  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que contém o projeto. O *folder_name* é **nvarchar(128)**.  
  
 [ @project _name = ] *project_name*  
 O nome do projeto. O *project_name* é **nvarchar(128)**.  
  
 [ @object_version_lsn = ] *object_version_lsn*  
 A versão do projeto. O *object_version_lsn* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Os detalhes do projeto são retornados como **varbinary(MAX)** como parte do conjunto de resultados se o *project_name* é localizado.  
  
 **NO RESULT SET** será retornado se o projeto não puder ser restaurado na pasta especificada.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no projeto  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   A versão do projeto não existe ou não corresponde ao nome do projeto  
  
-   O projeto não existe  
  
-   O usuário não tem as permissões apropriadas  
  
## <a name="remarks"></a>Remarks  
 Quando um projeto é restaurado, a todos os parâmetros são atribuídos valores padrão e todas as referências ao ambiente permanecem inalteradas. O número máximo de versões de projeto que são retidas no catálogo é determinado pela propriedade do catálogo **MAX_VERSIONS_PER_PROJECT**, conforme mostrado na exibição [catalog_property](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
> [!WARNING]  
>  Referências de ambiente podem não mais ser válidas depois que um projeto é restaurado.  
  
  
