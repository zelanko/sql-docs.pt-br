---
title: catalog.set_environment_variable_property (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: c1deb31e-b8d1-44ca-b355-570959bc6478
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b57a3ca1893d44cc2ed3fd60e20a39c4e43f473
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715933"
---
# <a name="catalogsetenvironmentvariableproperty-ssisdb-database"></a>catalog.set_environment_variable_property (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Define a propriedade de uma variável de ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_environment_variable_property [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que contém o ambiente. O *folder_name* é **nvarchar(128)**.  
  
 [ @environment_name = ] *environment_name*  
 O nome do ambiente. O *environment_name* é **nvarchar(128)**.  
  
 [ @variable_name = ] *variable_name*  
 O nome da variável de ambiente. O *variable_name* é **nvarchar(128)**.  
  
 [ @property_name = ] *property_name*  
 O nome da propriedade da variável de ambiente. O *property_name* é **nvarchar(128)**.  
  
 [ @property_value = ] *property_value*  
 O valor da propriedade da variável de ambiente. O *property_value* é **nvarchar(4000)**.  
  
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
  
-   O nome da pasta não é válido  
  
-   O nome do ambiente não é válido  
  
-   O nome da variável de ambiente não é válido  
  
-   O nome da propriedade da variável de ambiente não é válido  
  
-   O usuário não tem as permissões apropriadas  
  
## <a name="remarks"></a>Remarks  
 Nesta versão, somente a propriedade `Description` pode ser definida. O valor da propriedade `Description` não pode exceder 4000 caracteres.  
  
  
