---
title: Catalog. get_parameter_values (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 5b1aeaf7-c938-4aef-bafc-e4d7a82eb578
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4ad8f0c367e38581db696d2aa32afd5b92d635d2
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="cataloggetparametervalues-ssisdb-database"></a>catalog.get_parameter_values (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Resolve e recupera os valores de parâmetro padrão de um projeto e os pacotes correspondentes no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```tsql  
get_parameter_values [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @package_name = ] package_name  
  [  , [ @reference_id = ] reference_id  ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nome_da_pasta*  
 O nome da pasta que contém o projeto. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [ @project_name =] *project_name*  
 O nome do projeto em que o parâmetro reside. O *project_name* é **nvarchar (128)**.  
  
 [ @package_name =] *nome_do_pacote*  
 O nome do pacote. Especifique o nome do pacote para recuperar todos os parâmetros de projeto e os parâmetros de um pacote específico. Use NULL para recuperar todos os parâmetros de projeto e os parâmetros de todos os pacotes. O *nome_do_pacote* é **nvarchar (260)**.  
  
 [ @reference_id =] *reference_id*  
 O identificador exclusivo de uma referência do ambiente. Esse parâmetro é opcional. O *reference_id* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna uma tabela que tem o seguinte formato:  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|O tipo de parâmetro. O valor é `20` para um parâmetro de projeto e o valor é `30` para um parâmetro de pacote.|  
|parameter_data_type|**nvarchar (128)**|O tipo de dados do parâmetro.|  
|parameter_name|**sysname**|O nome do parâmetro.|  
|parameter_value|**sql_variant**|O valor do parâmetro.|  
|sensitive|**bit**|Quando o valor é `1`, o valor do parâmetro é confidencial. Quando o valor é `0`, o valor do parâmetro não é confidencial.|  
|required|**bit**|Quando o valor é `1`, o valor do parâmetro é necessário para iniciar a execução. Quando o valor é `0`, o valor de parâmetro não é necessário para iniciar a execução.|  
|value_set|**bit**|Quando o valor é `1`, o valor do parâmetro foi atribuído. Quando o valor é `0`, o valor do parâmetro não foi atribuído.|  
  
> [!NOTE]  
>  Valores literais são exibidos em texto não criptografado. **NULO** é exibido no lugar de valores confidenciais.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ no projeto e, se aplicável, permissão READ no ambiente referenciado  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   Não é possível encontrar o pacote na pasta ou projeto especificado  
  
-   O usuário não tem as permissões apropriadas  
  
-   A referência de ambiente especificado não existe  
  
  
