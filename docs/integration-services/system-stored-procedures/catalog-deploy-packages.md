---
description: catalog.deploy_packages
title: catalog.deploy_packages | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 383fe8ab64e0488ded13726d83e80a8bf7244455
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422160"
---
# <a name="catalogdeploy_packages"></a>catalog.deploy_packages 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Implanta um ou mais pacotes em uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou atualiza um pacote existente que foi implantado anteriormente.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.deploy_packages [ @folder_name = ] folder_name
    , [ @project_name = ] project_name
    , [ @packages_table = ] packages_table
    [, [ @operation_id OUTPUT = ] operation_id OUTPUT]
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta. O *folder_name* é **nvarchar(128)** .  
  
 [ @project_name = ] *project_name*  
 O nome do projeto na pasta. O *project_name* é **nvarchar(128)** .  
  
 [ @packages_table = ] *packages_table*  
 O conteúdo binário de arquivos de pacote de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (.dtsx). O *packages_table* é **[catalog].[Package_Table_Type]**  
  
 [ @operation_id = ] *operation_id*  
 Retorna o identificador exclusivo da operação de implantação. O *operation_id* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões CREATE_OBJECTS no projeto ou MODIFY no pacote para atualizar um pacote.  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem levar este procedimento armazenado a gerar um erro:  
  
-   Um parâmetro faz referência a um objeto que não existe, um parâmetro tenta criar um objeto que já existe ou um parâmetro é inválido de alguma outra maneira.  
  
-   O usuário não tem permissões suficientes  
  
  
