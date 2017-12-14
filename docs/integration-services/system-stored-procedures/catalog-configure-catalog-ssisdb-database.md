---
title: catalog.configure_catalog (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7edd093ee4804c8c0c01a5638fd7df519f4564bc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="catalogconfigurecatalog-ssisdb-database"></a>catalog.configure_catalog (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Configura o catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] definindo uma propriedade de catálogo como um valor especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @property_name = ] *property_name*  
 O nome da propriedade do catálogo. O *property_name* é **nvarchar(255)**. Para obter mais informações sobre propriedades disponíveis, consulte [catalog.catalog_properties &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
 [ @property_value = ] *property_value*  
 O valor da propriedade do catálogo. O *property_value* é **nvarchar(255)**. Para obter mais informações sobre valores de propriedades, consulte [catalog.catalog_properties &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 Este procedimento armazenado determina se o *property_value* é válido para cada *property_name*.  
  
 Este procedimento armazenado pode ser realizado somente quando não há execução ativa, como execuções pendentes, enfileiradas, em execução e em pausa.  
  
 Enquanto o catálogo está sendo configurado, todos os outros procedimentos armazenados de catálogo apresentam falha com a mensagem de erro "O servidor está sendo configurado no momento".
  
 Quando o catálogo está configurado, uma entrada é escrita no log de operação.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   A propriedade não existe  
  
-   O valor de propriedade é inválido  
  
  
