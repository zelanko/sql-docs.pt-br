---
title: catalog.set_environment_variable_protection (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 005b6b2f-a5d9-4ea4-8d4e-beed6ab33c0d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4f83c5569ef43ee78b2e1054faf26bf0b9867f3a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912852"
---
# <a name="catalogset_environment_variable_protection-ssisdb-database"></a>catalog.set_environment_variable_protection (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Define o bit de sensibilidade de uma variável de ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_environment_variable_protection [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable_name  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que contém o ambiente. O *folder_name* é **nvarchar(128)** .  
  
 [ @environment_name = ] *environment_name*  
 O nome do ambiente. O *environment_name* é **nvarchar(128)** .  
  
 [ @variable_name = ] *variable_name*  
 O nome da variável de ambiente. O *variable_name* é **nvarchar(128)** .  
  
 [ @sensitive = ] *sensitive*  
 Indica se a variável contém um valor confidencial ou não. Use um valor de `1` para indicar que o valor da variável de ambiente é confidencial ou um valor de `0` para indicar que não é. Um valor confidencial é criptografado quando é armazenado. Um valor que não é confidencial é armazenado em texto não criptografado. O parâmetro *sensitive* é **bit**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
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
  
-   O usuário não tem as permissões apropriadas  
  
  
