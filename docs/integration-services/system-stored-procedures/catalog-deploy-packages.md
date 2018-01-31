---
title: catalog.deploy_packages | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f44775c2852c1d89c0549f2beab7fd903d66c4d3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="catalogdeploypackages"></a>catalog.deploy_packages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Implanta um ou mais pacotes em uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou atualiza um pacote existente que foi implantado anteriormente.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta. O *folder_name* é **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 O nome do projeto na pasta. O *project_name* é **nvarchar(128)**.  
  
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
  
  
