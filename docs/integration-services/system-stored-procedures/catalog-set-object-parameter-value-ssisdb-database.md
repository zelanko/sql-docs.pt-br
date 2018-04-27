---
title: catalog.set_object_parameter_value (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de4f863322b805d8a2dfc0e6f21cae8378095e93
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
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
 O tipo do parâmetro. Use o valor `20` para indicar um parâmetro de projeto ou o valor `30` para indicar um parâmetro de pacote. O *object_type* é **smallInt**.  
  
 [@folder_name =] *folder_name*  
 O nome da pasta que contém o parâmetro. O *folder_name* é **nvarchar(128)**.  
  
 [@project_name =] *project_name*  
 O nome do projeto que contém o parâmetro. O *project_name* é **nvarchar(128)**.  
  
 [@parameter_name =] *parameter_name*  
 O nome do parâmetro. O *parameter_name* é **nvarchar(128)**.  
  
 [@parameter_value =] *parameter_value*  
 O valor do parâmetro. O *parameter_value* é **sql_variant**.  
  
 [@object_name =] *object_name*  
 O nome do pacote. Esse argumento será exigido quando o parâmetro for um parâmetro de pacote. O *object_name* é **nvarchar(260)**.  
  
 [@value_type =] *value_type*  
 O tipo de valor do parâmetro. Use o caractere `V` para indicar que *parameter_value* é um valor literal que é usado por padrão quando nenhum outro valor é atribuído antes da execução. Use o caractere `R` para indicar que *parameter_value* é um valor referenciado e foi definido para o nome de uma variável de ambiente. Esse argumento é opcional, o caractere `V` é usado por padrão. O *value_type* é **char (1)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no projeto  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem fazer com que o procedimento armazenado gere um erro:  
  
-   O tipo do parâmetro não é válido  
  
-   O nome do projeto não é válido  
  
-   Para os parâmetros de pacote, o nome do pacote não é válido  
  
-   O tipo de valor não é válido  
  
-   O usuário não tem as permissões apropriadas  
  
## <a name="remarks"></a>Remarks  
  
-   Se nenhum *value_type* for especificado, um valor literal para *parameter_value* será usado por padrão. Quando um valor literal for usado, o *value_set* na exibição [object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) será definido como `1`. O valor de parâmetro NULL não é permitido.  
  
-   Se *value_type* contiver o caractere `R`, que denota um valor referenciado, *parameter_value* fará referência ao nome de uma variável de ambiente.  
  
-   O valor `20` pode ser usado para *object_type* a fim de denotar um parâmetro de projeto. Nesse caso, um valor para *object_name* não é necessário e qualquer valor especificado para *object_name* será ignorado. Esse valor será usado quando o usuário desejar definir um parâmetro de projeto.  
  
-   O valor `30` pode ser usado para *object_type* a fim de denotar um parâmetro de pacote. Nesse caso, um valor para *object_name* será usado para denotar o pacote correspondente. Se *object_name* não for especificado, o procedimento armazenado retornará um erro e será encerrado.  
  
  
