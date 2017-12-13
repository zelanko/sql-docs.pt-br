---
title: catalog.deploy_project (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 2e3439b4-7226-4b61-a993-7a1d161eac7e
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b056ec4e0d4f762190154988fe3fa225e447c315
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="catalogdeployproject-ssisdb-database"></a>catalog.deploy_project (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Implanta um projeto a uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou atualiza um projeto existente que foi implantado anteriormente.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.deploy_project [@folder_name =] folder_name   
      , [@project_name =] project_name   
      , [@project_stream =] projectstream   
    [ , [@operation_id ] = operation_id OUTPUT ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *folder_name*  
 O nome da pasta em que o projeto é implantado. O *folder_name* é **nvarchar(128)**.  
  
 [@project_name =] *project_name*  
 O nome do projeto novo ou atualizado na pasta. O *project_name* é **nvarchar(128)**.  
  
 [@projectstream =] *projectstream*  
 O conteúdo binário de um arquivo de implantação de projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (extensão .ispac).  
  
 Você pode usar uma instrução SELECT com a função OPENROWSET e o provedor de conjuntos de linhas BULK para recuperar o conteúdo binário do arquivo. Para obter um exemplo, consulte [Implantar projetos e pacotes SSIS (Integration Services)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md). Para obter mais informações sobre OPENROWSET, veja [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
 O *projectstream* é **varbinary(MAX)**  
  
 [@operation_id =] *operation_id*  
 Retorna o identificador exclusivo da operação de implantação. O *operation_id* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões CREATE_OBJECTS na pasta para implantar um novo projeto ou permissões MODIFY no projeto atualizar um projeto  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem levar este procedimento armazenado a gerar um erro:  
  
-   Um parâmetro faz referência a um objeto que não existe, um parâmetro tenta criar um objeto que já existe ou um parâmetro é inválido de alguma outra maneira  
  
-   O valor do parâmetro *@project_name* não corresponde ao nome do projeto no arquivo de implantação  
  
-   O usuário não tem permissões suficientes  
  
## <a name="remarks"></a>Comentários  
 Durante uma implantação ou atualização de projeto, o procedimento armazenado não verifica o nível de proteção de pacotes individuais no projeto.  
  
  
