---
title: catalog.set_customized_logging_level_description | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 6ceaa39f-2439-457b-b99f-f12d88a1be32
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4e03fd076ccf7185749c63b1dc85c48d9f8d1611
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="catalogsetcustomizedloggingleveldescription"></a>catalog.set_customized_logging_level_description
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Altera descrição de um nível de log personalizado existente. Para obter mais informações sobre níveis de registro em log personalizados, consulte [Registro em Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_customized_logging_level_description [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @level_name = ] *level_name*  
 O nome de um nível de log personalizado existente.  
  
 O *level_name* é **nvarchar(128)**.  
  
 [ @level_description = ] *level_description*  
 A nova descrição para o nível de log personalizado especificado.  
  
 O *level_description* é **nvarchar(1024)**.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (êxito)  
  
 Quando há falha no procedimento armazenado, ele gera um erro.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação na função de banco de dados **ssis_admin**  
  
-   Associação na função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve as condições que podem provocar falha no procedimento armazenado.  
  
-   O usuário não tem as permissões necessárias.  
  
  
