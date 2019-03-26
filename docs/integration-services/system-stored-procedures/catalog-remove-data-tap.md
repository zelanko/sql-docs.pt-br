---
title: catalog.remove_data_tap | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 497c82ffc7a9bf0b6715a4d005145c73a19f7b78
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270867"
---
# <a name="catalogremovedatatap"></a>catalog.remove_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Remove um toque de dados de uma saída de componente que está em uma execução. O identificador exclusivo do toque de dados é associado a uma instância da execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.remove_data_tap [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @data_tap_id = ] *data_tap_id*  
 O identificador exclusivo do toque de dados criado por meio do procedimento armazenado catalog.add_data_tap. O *data_tap_id* é **bigint**.  
  
## <a name="remarks"></a>Remarks  
 Quando um pacote contém mais de uma tarefa de fluxo de dados com o mesmo nome, o toque de dados é adicionado à primeira tarefa de fluxo de dados com o determinado nome.  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (êxito)  
  
 Quando há falha no procedimento armazenado, ele gera um erro.  
  
## <a name="result-set"></a>Conjunto de resultados  
 None  
  
## <a name="remarks"></a>Remarks  
 Para remover coletas de dados, a instância da execução deve estar no estado criado (um valor de 1 na coluna **status** da exibição [catalog.operations &#40;banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)).  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões MODIFY na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve as condições que podem provocar falha no procedimento armazenado.  
  
-   O usuário não tem permissões MODIFY.  
  
## <a name="see-also"></a>Consulte Também  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
