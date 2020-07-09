---
title: catalog.create_folder (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 95f74f595481d9cf373c51be18cccf404b824e49
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749657"
---
# <a name="catalogcreate_folder-ssisdb-database"></a>catalog.create_folder (Banco de dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Cria uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.create_folder [ @folder_name = ] folder_name, [ @folder_id = ] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *folder_name*  
 O nome da nova pasta. O *folder_name* é **nvarchar(128)** .  
  
 [@folder_name =] *folder_id*  
 O ID (identificador exclusivo) da pasta. O *folder_id* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 O identificador da pasta é retornado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
O procedimento armazenado retornará um erro se já existir uma pasta com o mesmo nome.  
  
  
