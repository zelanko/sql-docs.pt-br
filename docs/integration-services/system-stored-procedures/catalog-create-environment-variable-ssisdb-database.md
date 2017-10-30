---
title: Catalog. create_environment_variable (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 91ed017b-6567-4bf2-b9f1-e2b5c70a5343
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 5636651cccbb43c6c1627d1f28eccd9b3f9b5b0d
ms.contentlocale: pt-br
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreateenvironmentvariable-ssisdb-database"></a>catalog.create_environment_variable (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Cria uma variável de ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.create_environment_variable [@folder_name =] folder_name  
    , [@environment_name =] environment_name  
    , [@variable_name =] variable_name  
    , [@data_type =] data_type  
    , [@sensitive =] sensitive  
    , [@value =] value  
    , [@description =] description  
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *nome_da_pasta*  
 O nome da pasta que contém o ambiente. O *nome_da_pasta* é **nvarchar (128)**.  
  
 [@environment_name =] *environment_name*  
 O nome do ambiente. O *environment_name* é **nvarchar (128)**.  
  
 [@variable_name =] *variable_name*  
 O nome da variável de ambiente. O *variable_name* é **nvarchar (128)**.  
  
 [@data_type =] *data_type*  
 O tipo de dados da variável. Suporte para dados de variável de ambiente tipos incluem **booliano**, **bytes**, **DateTime**, **duplo**, **Int16**, **Int32**, **Int64**, **único**, **cadeia de caracteres**, **UInt32**e  **UInt64**. Os tipos de dados da variável de ambiente sem suporte incluem **Char**, **DBNull**, **objeto**, e **Sbyte**. O tipo de dados de *data_type* parâmetro é **nvarchar (128)**.  
  
 [@sensitive =] *confidenciais*  
 Indica se a variável contém um valor confidencial ou não. Use um valor de `1` para indicar que o valor da variável de ambiente é confidencial ou um valor de `0` para indicar que não é. Um valor confidencial é criptografado quando é armazenado. Um valor que não é confidencial é armazenado em texto não criptografado. *Confidenciais* é **bit**.  
  
 [@value =] *valor*  
 O valor da variável de ambiente. O *valor* é **sql_variant**.  
  
 [@description =] *descrição*  
 A descrição da variável do ambiente. O *valor* é **nvarchar (1024)**.  
  
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
  
-   O nome de pasta, nome de ambiente, ou nome de variável de ambiente não é válido  
  
-   O nome da variável já existe no ambiente  
  
-   O usuário não tem as permissões apropriadas  
  
## <a name="remarks"></a>Comentários  
 Uma variável de ambiente pode ser usada para atribuir um valor com eficiência a um parâmetro de projeto ou parâmetro de pacote para uso na execução de um pacote. As variáveis de ambiente habilitam a organização de valores de parâmetros. Os nomes de variável devem ser exclusivos dentro de um ambiente.  
  
 O procedimento armazenado valida o tipo de dados da variável para ter certeza de que tem suporte pelo catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
> [!TIP]  
>  Considere o uso de **Int16** tipo de dados na [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em vez do suporte **Sbyte** tipo de dados.  
  
 O valor passado para esse procedimento armazenado com o *valor* parâmetro é convertido de um [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tipo de dados para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados de acordo com a tabela a seguir:  
  
|Tipo de dados do Integration Services|Tipo de dados do SQL Server|  
|------------------------------------|--------------------------|  
|**Booliano**|**bit**|  
|**Bytes**|**binário**, **varbinary**|  
|**DateTime**|**DateTime**, **datetime2**, **datetimeoffset**, **smalldatetime**|  
|**Double**|Numérico exato: **decimal**, **numérico**; Numérico aproximado: **float**, **real**|  
|**Int16**|**smallint**|  
|**Int32**|**int**|  
|**Int64**|**bigint**|  
|**Single**|Numérico exato: **decimal**, **numérico**; Numérico aproximado: **float**, **real**|  
|**Cadeia de caracteres**|**varchar**, **nvarchar**, **char**|  
|**UInt32**|**int** (**int** é o mapeamento disponível mais próximo para **Uint32**.)|  
|**UInt64**|**bigint** (**int** é o mapeamento disponível mais próximo para **Uint64**.)|  
  
  

