---
title: Catalog. restore_project (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8adee525-579b-4d2f-b807-e2ecc07fb2e9
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 23074fc664591411666315036e3493e1b7b26134
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrestoreproject-ssisdb-database"></a>catalog.restore_project (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restaura um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para uma versão anterior.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
restore_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project _name  
    , [ @object_version_lsn = ] object_version_lsn  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nome_da_pasta*  
 O nome da pasta que contém o projeto. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [ @project Name =] *project_name*  
 O nome do projeto. O *project_name* é **nvarchar (128)**.  
  
 [ @object_version_lsn =] *object_version_lsn*  
 A versão do projeto. O *object_version_lsn* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Detalhes do projeto são retornados como **varbinary (max)** como parte do conjunto de resultados se o *project_name* foi encontrado.  
  
 **Nenhum conjunto de resultados** será retornado se o projeto não pode ser restaurado para a pasta especificada.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no projeto  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   A versão do projeto não existe ou não corresponde ao nome do projeto  
  
-   O projeto não existe  
  
-   O usuário não tem as permissões apropriadas  
  
## <a name="remarks"></a>Comentários  
 Quando um projeto é restaurado, a todos os parâmetros são atribuídos valores padrão e todas as referências ao ambiente permanecem inalteradas. O número máximo de versões do projeto que são mantidas no catálogo é determinado pela propriedade do catálogo **MAX_VERSIONS_PER_PROJECT**, conforme o [catalog_property](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) exibição.  
  
> [!WARNING]  
>  Referências de ambiente podem não mais ser válidas depois que um projeto é restaurado.  
  
  
