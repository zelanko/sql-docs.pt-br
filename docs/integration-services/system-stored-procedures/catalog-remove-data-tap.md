---
title: Catalog.remove_data_tap | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2f2c9b5d9333c201120e5f3a3e392c59012a8ac7
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogremovedatatap"></a>catalog.remove_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Remove um toque de dados de uma saída de componente que está em uma execução. O identificador exclusivo do toque de dados é associado a uma instância da execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.remove_data_tap [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @data_tap_id =] *data_tap_id*  
 O identificador exclusivo do toque de dados criado por meio do procedimento armazenado catalog.add_data_tap. O *data_tap_id* é **bigint**.  
  
## <a name="remarks"></a>Comentários  
 Quando um pacote contém mais de uma tarefa de fluxo de dados com o mesmo nome, o toque de dados é adicionado à primeira tarefa de fluxo de dados com o determinado nome.  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (êxito)  
  
 Quando há falha no procedimento armazenado, ele gera um erro.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 Para remover dados toca, a instância da execução deve estar no estado criado (um valor de 1 no **status** coluna o [Catalog. Operations &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md)exibição).  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões MODIFY na instância de execução  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve as condições que podem provocar falha no procedimento armazenado.  
  
-   O usuário não tem permissões MODIFY.  
  
## <a name="see-also"></a>Consulte também  
 [add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  

