---
title: Catalog. configure_catalog (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 15bec231bf1de825cea952e07827074d56751386
ms.contentlocale: pt-br
ms.lasthandoff: 10/20/2017

---
# <a name="catalogconfigurecatalog-ssisdb-database"></a>catalog.configure_catalog (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Configura o catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] definindo uma propriedade de catálogo como um valor especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @property_name =] *property_name*  
 O nome da propriedade do catálogo. O *property_name* é **nvarchar (255)**. Para obter mais informações sobre propriedades disponíveis, consulte [Catalog. catalog_properties &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
 [ @property_value =] *property_value*  
 O valor da propriedade do catálogo. O *property_value* é **nvarchar (255)**. Para obter mais informações sobre valores de propriedade, consulte [Catalog. catalog_properties &#40; Banco de dados SSISDB &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 Esse procedimento armazenado determina se o *property_value* é válido para cada *property_name*.  
  
 Este procedimento armazenado pode ser realizado somente quando não há execução ativa, como execuções pendentes, enfileiradas, em execução e em pausa.  
  
 Enquanto o catálogo está sendo configurado, todos os outros catálogo armazenadas procedimentos falha com a mensagem de erro "Servidor atualmente está sendo configurado."
  
 Quando o catálogo está configurado, uma entrada é escrita no log de operação.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   A propriedade não existe  
  
-   O valor de propriedade é inválido  
  
  

