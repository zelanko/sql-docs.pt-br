---
title: Catalog. clear_object_parameter_value (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: dcbbb714-a051-4805-9e2b-2c2fb647c890
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5d0d89081a31341a8d813d9985940c0e3ce0160a
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogclearobjectparametervalue-ssisdb-database"></a>catalog.clear_object_parameter_value (Banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Limpa o valor de um parâmetro para um projeto ou pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] existente armazenado no servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```tsql  
clear_object_parameter [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @object_type = ] object_type   
    , [ @object_name = ] object_name   
    , [ @parameter_ name = ] parameter_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nome_da_pasta*  
 O nome da pasta que contém o projeto. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [ @project_name =] *project_name*  
 O nome do projeto. O *project_name* é **nvarchar (128)**.  
  
 [ @object_type =] *object_type*  
 O tipo do objeto. Os valores válidos incluem `20` para um projeto e `30` para um pacote. O *object_type* é **smallInt**.  
  
 [@ Name do objeto =] *Name do objeto*  
 O nome do pacote. O *Name do objeto* é **nvarchar (260)**.  
  
 [ @parameter_ nome =] *parameter_name*  
 O nome do parâmetro. O *parameter_ nome* é **nvarchar (128)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no projeto  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem fazer com que o procedimento armazenado de clear_object_parameter gerar um erro:  
  
-   Um tipo de objeto inválido é especificado ou o nome do objeto não pode ser localizado no projeto.  
  
-   O projeto não existe, o projeto não está acessível ou o nome do projeto é inválido.  
  
-   Um nome de parâmetro inválido é especificado.  
  
-   O usuário não tem as permissões apropriadas.  
  
  
