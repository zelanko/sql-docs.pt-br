---
title: Catalog. set_object_parameter_value (banco de dados SSISDB) | Microsoft Docs
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
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 3a5dc70b1e955b3c702dc9e9dbe4776cc4ebd5ac
ms.contentlocale: pt-br
ms.lasthandoff: 10/20/2017

---
# <a name="catalogsetobjectparametervalue-ssisdb-database"></a>catalog.set_object_parameter_value (Banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Define o valor de um parâmetro no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Associa o valor a uma variável de ambiente ou atribui um valor literal que será usado por padrão quando nenhum outro valor for atribuído.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_object_parameter_value [@object_type =] object_type   
    , [@folder_name =] folder_name   
    , [@project_name =] project_name   
    , [@parameter_name =] parameter _name   
    , [@parameter_value =] parameter_value   
 [  , [@object_name =] object_name ]  
 [  , [@value_type =] value_type ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [@object_type =] *object_type*  
 O tipo de parâmetro. Use o valor `20` para indicar um parâmetro de projeto ou o valor `30` para indicar um parâmetro de pacote. O *object_type* é **smallInt**.  
  
 [@folder_name =] *nome_da_pasta*  
 O nome da pasta que contém o parâmetro. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [@project_name =] *project_name*  
 O nome do projeto que contém o parâmetro. O *project_name* é **nvarchar (128)**.  
  
 [@parameter_name =] *parameter_name*  
 O nome do parâmetro. O *parameter_name* é **nvarchar (128)**.  
  
 [@parameter_value =] *parameter_value*  
 O valor do parâmetro. O *parameter_value* é **sql_variant**.  
  
 [@object_name =] *object_name*  
 O nome do pacote. Esse argumento será exigido quando o parâmetro for um parâmetro de pacote. O *object_name* é **nvarchar (260)**.  
  
 [@value_type =] *value_type*  
 O tipo de valor do parâmetro. Use o caractere `V` para indicar que *parameter_value* é um valor literal que será usado por padrão quando nenhum outro valor for atribuído antes da execução. Use o caractere `R` para indicar que *parameter_value* é um valor referenciado e foi definido como o nome de uma variável de ambiente. Esse argumento é opcional, o caractere `V` é usado por padrão. O *value_type* é **char (1)**.  
  
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
 A lista a seguir descreve algumas condições que podem fazer com que o procedimento armazenado gere um erro:  
  
-   O tipo do parâmetro não é válido  
  
-   O nome do projeto não é válido  
  
-   Para os parâmetros de pacote, o nome do pacote não é válido  
  
-   O tipo de valor não é válido  
  
-   O usuário não tem as permissões apropriadas  
  
## <a name="remarks"></a>Comentários  
  
-   Se nenhum *value_type* for especificado, um valor literal para *parameter_value* é usado por padrão. Quando um valor literal é usado, o *value_set* no [object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) exibição está definida como `1`. O valor de parâmetro NULL não é permitido.  
  
-   Se *value_type* contém o caractere `R`, que indica um valor referenciado, *parameter_value* refere-se ao nome de uma variável de ambiente.  
  
-   O valor `20` podem ser usadas para *object_type* para denotar um parâmetro de projeto. Nesse caso, um valor para *object_name* não é necessário e qualquer valor especificado para *object_name* será ignorado. Esse valor será usado quando o usuário desejar definir um parâmetro de projeto.  
  
-   O valor `30` podem ser usadas para *object_type* para denotar um parâmetro de pacote. Nesse caso, um valor para *object_name* é usado para denotar o pacote correspondente. Se *object_name* não for especificado, o procedimento armazenado retorna um erro e será encerrado.  
  
  

