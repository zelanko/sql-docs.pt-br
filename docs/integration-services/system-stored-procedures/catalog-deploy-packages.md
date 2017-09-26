---
title: Catalog.deploy_packages | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1839430dd7fb83ab16c4de46011819e3ce28e835
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeploypackages"></a>Catalog.deploy_packages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Implanta um ou mais pacotes para uma pasta de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catálogo ou atualiza um pacote existente que tenha sido implantado anteriormente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nome_da_pasta*  
 O nome da pasta. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [ @project_name =] *project_name*  
 O nome do projeto na pasta. O *project_name* é **nvarchar (128)**.  
  
 [ @packages_table =] *packages_table*  
 O conteúdo binário de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacote (. dtsx) arquivo (s). O *packages_table* é **[catalog]. [ Package_Table_Type]**  
  
 [ @operation_id =] *operation_id*  
 Retorna o identificador exclusivo da operação de implantação. O *operation_id* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões CREATE_OBJECTS no projeto ou modificar permissões no pacote para atualizar um pacote.  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem levar este procedimento armazenado a gerar um erro:  
  
-   Um parâmetro faz referência a um objeto que não existe, um parâmetro tenta criar um objeto que já existe ou um parâmetro é inválido de alguma outra maneira.  
  
-   O usuário não tem permissões suficientes  
  
  
