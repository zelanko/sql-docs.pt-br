---
title: Catalog. delete_environment (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: d44b765f-9523-4e6a-bb17-37846d5e5334
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4b225e35b22c7dbeb7c53cb8d93aac6e5e1059f2
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeleteenvironment-ssisdb-database"></a>catalog.delete_environment (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exclui um ambiente de uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```tsql  
delete_environment [ @folder_name = ] folder_name , [ @environment_name = ] environment_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nome_da_pasta*  
 O nome da pasta que contém o ambiente. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [ @environment_name =] *environment_name*  
 O nome do ambiente que deve ser excluído. O *environment_name* é **nvarchar (128)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no ambiente  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O ambiente especificado não existe.  
  
-   O usuário não tem as permissões apropriadas  
  
  
