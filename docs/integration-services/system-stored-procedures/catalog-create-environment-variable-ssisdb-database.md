---
title: catalog.create_environment_variable (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 91ed017b-6567-4bf2-b9f1-e2b5c70a5343
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8f7474200fa8156ab0663540611803276375ad6b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281188"
---
# <a name="catalogcreate_environment_variable-ssisdb-database"></a>catalog.create_environment_variable (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
 [@folder_name =] *folder_name*  
 O nome da pasta que contém o ambiente. O *folder_name* é **nvarchar(128)** .  
  
 [@environment_name =] *environment_name*  
 O nome do ambiente. O *environment_name* é **nvarchar(128)** .  
  
 [@variable_name =] *variable_name*  
 O nome da variável de ambiente. O *variable_name* é **nvarchar(128)** .  
  
 [@data_type =] *data_type*  
 O tipo de dados da variável. Os tipos de dados de variável de ambiente com suporte incluem **booliano**, **Byte**, **DateTime**, **Double**, **Int16**, **Int32**, **Int64**, **Single**, **String**, **UInt32** e **UInt64**. Os tipos de dados de variável de ambiente sem suporte incluem **Char**, **DBNull**, **Object** e **Sbyte**. O tipo de dados do parâmetro *data_type* é **nvarchar(128)** .  
  
 [@sensitive =] *sensitive*  
 Indica se a variável contém um valor confidencial ou não. Use um valor de `1` para indicar que o valor da variável de ambiente é confidencial ou um valor de `0` para indicar que não é. Um valor confidencial é criptografado quando é armazenado. Um valor que não é confidencial é armazenado em texto não criptografado. *Sensitive* é **bit**.  
  
 [@value =] *value*  
 O valor da variável de ambiente. O *value* é **sql_variant**.  
  
 [@description =] *description*  
 A descrição da variável do ambiente. O *value* é **nvarchar(1024)** .  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no ambiente  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O nome de pasta, nome de ambiente, ou nome de variável de ambiente não é válido  
  
-   O nome da variável já existe no ambiente  
  
-   O usuário não tem as permissões apropriadas  
  
## <a name="remarks"></a>Remarks  
 Uma variável de ambiente pode ser usada para atribuir um valor com eficiência a um parâmetro de projeto ou parâmetro de pacote para uso na execução de um pacote. As variáveis de ambiente habilitam a organização de valores de parâmetros. Os nomes de variável devem ser exclusivos dentro de um ambiente.  
  
 O procedimento armazenado valida o tipo de dados da variável para ter certeza de que tem suporte pelo catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
> [!TIP]  
>  Considere usar o tipo de dados **Int16** em [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no lugar do tipo de dados **Sbyte** sem suporte.  
  
 O valor passado a este procedimento armazenado com o parâmetro *value* será convertido de um tipo de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para um tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de acordo com a tabela a seguir:  
  
|Tipo de Dados do Integration Services|Tipo de dados do SQL Server|  
|------------------------------------|--------------------------|  
|**Booliano**|**bit**|  
|**Byte**|**binary**, **varbinary**|  
|**DateTime**|**datetime**, **datetime2**, **datetimeoffset**, **smalldatetime**|  
|**Double**|Numérico exato: **decimal**, **numeric**; Numérico aproximado: **float**, **real**|  
|**Int16**|**smallint**|  
|**Int32**|**int**|  
|**Int64**|**bigint**|  
|**Single**|Numérico exato: **decimal**, **numeric**; Numérico aproximado: **float**, **real**|  
|**String**|**varchar**, **nvarchar**, **char**|  
|**UInt32**|**int** (**int** é o mapeamento disponível mais próximo para **Uint32**.)|  
|**UInt64**|**bigint** (**int** é o mapeamento disponível mais próximo para **Uint64**.)|  
  
  
