---
title: Catalog. deploy_project (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 2e3439b4-7226-4b61-a993-7a1d161eac7e
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 5682cd23cb65e097bccb8cc69d5f2ec88ece7709
ms.contentlocale: pt-br
ms.lasthandoff: 10/20/2017

---
# <a name="catalogdeployproject-ssisdb-database"></a>catalog.deploy_project (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Implanta um projeto a uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou atualiza um projeto existente que foi implantado anteriormente.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.deploy_project [@folder_name =] folder_name   
      , [@project_name =] project_name   
      , [@project_stream =] projectstream   
    [ , [@operation_id ] = operation_id OUTPUT ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *nome_da_pasta*  
 O nome da pasta onde o projeto é implantado. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [@project_name =] *project_name*  
 O nome do projeto novo ou atualizado na pasta. O *project_name* é **nvarchar (128)**.  
  
 [@projectstream =] *projectstream*  
 O conteúdo binário de um arquivo de implantação de projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (extensão .ispac).  
  
 Você pode usar uma instrução SELECT com a função OPENROWSET e o provedor de conjuntos de linhas BULK para recuperar o conteúdo binário do arquivo. Para obter um exemplo, consulte [implantar Integration Services (SSIS) projetos e pacotes](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md). Para obter mais informações sobre OPENROWSET, consulte [OPENROWSET &#40; Transact-SQL &#41; ](../../t-sql/functions/openrowset-transact-sql.md).  
  
 O *projectstream* é **varbinary (max)**  
  
 [@operation_id =] *operation_id*  
 Retorna o identificador exclusivo da operação de implantação. O *operation_id* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões CREATE_OBJECTS na pasta para implantar um novo projeto ou permissões MODIFY no projeto atualizar um projeto  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem levar este procedimento armazenado a gerar um erro:  
  
-   Um parâmetro faz referência a um objeto que não existe, um parâmetro tenta criar um objeto que já existe ou um parâmetro é inválido de alguma outra maneira  
  
-   O valor do parâmetro  *@project_name*  não coincide com o nome do projeto no arquivo de implantação  
  
-   O usuário não tem permissões suficientes  
  
## <a name="remarks"></a>Comentários  
 Durante uma implantação ou atualização de projeto, o procedimento armazenado não verifica o nível de proteção de pacotes individuais no projeto.  
  
  

