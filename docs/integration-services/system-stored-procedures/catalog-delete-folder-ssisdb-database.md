---
title: catalog.delete_folder (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b9c08992-500c-447e-bc19-1eb13c9b0293
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4e9986843ce2196cd4450bac806631a862147ef4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749603"
---
# <a name="catalogdelete_folder-ssisdb-database"></a>catalog.delete_folder (Banco de dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exclui uma pasta do catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.delete_folder [ @folder_name = ] folder_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que deve ser excluída. O *folder_name* é **nvarchar(128)** .  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 Retorna uma mensagem para confirmar a exclusão da pasta.  
  
  
