---
title: catalog.configure_catalog (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b093d11e0a54b9e2c744358de82f7d5b09e7c33
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58274648"
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
 None  
  
## <a name="remarks"></a>Remarks  
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
  
  
