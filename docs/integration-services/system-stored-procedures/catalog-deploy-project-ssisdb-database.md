---
title: catalog.deploy_project (banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 2e3439b4-7226-4b61-a993-7a1d161eac7e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b2578745d445c1f2ac91b037ac7ce8e694687a16
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913042"
---
# <a name="catalogdeploy_project-ssisdb-database"></a>catalog.deploy_project (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Implanta um projeto a uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou atualiza um projeto existente que foi implantado anteriormente.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.deploy_project [@folder_name =] folder_name   
      , [ @project_name = ] project_name   
      , [ @project_stream = ] projectstream   
    [ , [ @operation_id = ] operation_id OUTPUT ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *folder_name*  
 O nome da pasta em que o projeto é implantado. O *folder_name* é **nvarchar(128)** .  
  
 [@project_name =] *project_name*  
 O nome do projeto novo ou atualizado na pasta. O *project_name* é **nvarchar(128)** .  
  
 [@projectstream =] *projectstream*  
 O conteúdo binário de um arquivo de implantação de projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (extensão .ispac).  
  
 Você pode usar uma instrução SELECT com a função OPENROWSET e o provedor de conjuntos de linhas BULK para recuperar o conteúdo binário do arquivo. Para obter um exemplo, consulte [Implantar projetos e pacotes SSIS (Integration Services)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md). Para obter mais informações sobre OPENROWSET, veja [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
 O *projectstream* é **varbinary(MAX)**  
  
 [@operation_id =] *operation_id*  
 Retorna o identificador exclusivo da operação de implantação. O *operation_id* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões CREATE_OBJECTS na pasta para implantar um novo projeto ou permissões MODIFY no projeto atualizar um projeto  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem levar este procedimento armazenado a gerar um erro:  
  
-   Um parâmetro faz referência a um objeto que não existe, um parâmetro tenta criar um objeto que já existe ou um parâmetro é inválido de alguma outra maneira  
  
-   O valor do parâmetro *\@project_name* não corresponde ao nome do projeto no arquivo de implantação  
  
-   O usuário não tem permissões suficientes  
  
## <a name="remarks"></a>Comentários  
 Durante uma implantação ou atualização de projeto, o procedimento armazenado não verifica o nível de proteção de pacotes individuais no projeto.  
  
  
