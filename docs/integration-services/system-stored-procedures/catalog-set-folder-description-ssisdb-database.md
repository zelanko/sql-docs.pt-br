---
title: catalog.set_folder_description (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
ms.assetid: 802416f6-5177-4db5-bca5-976dec5faf53
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3945f1a7eb3d416b801d7803fa256df47bdcc42
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogsetfolderdescription-ssisdb-database"></a>catalog.set_folder_description (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Define a descrição de uma pasta do catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_folder_description [ @folder_name = ] folder_name  
    , [ @folder_description = ] folder_description  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta. O *folder_name* é **nvarchar(128)**.  
  
 [ @folder_description = ] *folder_description*  
 A descrição da pasta. O *folder_description* é **nvarchar(MAX)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 O procedimento armazenado retorna uma mensagem para confirmar a configuração da nova descrição de pasta.  
  
  
