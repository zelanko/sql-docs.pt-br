---
title: sys.dm_xe_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_objects
- sys.dm_xe_objects
- sys.dm_xe_objects_TSQL
- dm_xe_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_objects dynamic management view
- extended events [SQL Server], views
ms.assetid: 5d944b99-b097-491b-8cbd-b0e42b459ec0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 023ee54178c5f303797c6db83cc646353304b051
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090269"
---
# <a name="sysdmxeobjects-transact-sql"></a>sys.dm_xe_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada objeto exposto por um pacote de evento. Os objetos podem ser um dos seguintes:  
  
-   Eventos. Os eventos indicam pontos de interesse em um caminho de execução. Todos os eventos contêm informações sobre um ponto de interesse.  
  
-   Ações. As ações são executadas sincronicamente quando os eventos têm início. Uma ação pode acrescentar dados em tempo de execução a um evento.  
  
-   Destinos. Os destinos consomem eventos de forma síncrona no thread que aciona o evento ou de forma assíncrona em um thread fornecido pelo sistema.  
  
-   Predicados. Fontes de predicado recuperam valores de fontes de evento para uso em operações de comparação. As comparações de predicado comparam tipos de dados específicos e retornam um valor booliano.  
  
-   Tipos. Os tipos encapsulam o comprimento e as características da coleção de bytes que é exigida para interpretar os dados.  

 |Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|O nome do objeto. nome é exclusivo dentro de um pacote para um tipo de objeto específico. Não permite valor nulo.|  
|object_type|**nvarchar(60)**|O tipo do objeto. object_type é um dos seguintes:<br /><br /> event<br /><br /> action<br /><br /> target<br /><br /> pred_source<br /><br /> pred_compare<br /><br /> type<br /><br /> Não permite valor nulo.|  
|package_guid|**uniqueidentifier**|A GUID para o pacote que expõe esta ação. Há uma relação muitos para uma com sys.dm_xe_packages.package_id. Não permite valor nulo.|  
|description|**nvarchar(256)**|Uma descrição da ação. Descrição é definida pelo autor do pacote. Não permite valor nulo.|  
|funcionalidades|**int**|Um bitmap que descreve as funcionalidades do objeto. Permite valor nulo.|  
|capabilities_desc|**nvarchar(256)**|Lista todas as funcionalidades do objeto. Permite valor nulo.<br /><br /> **Recursos que se aplicam a todos os tipos de objeto**<br /><br /> -<br />                                **Privado**. O único objeto disponível para uso interno e que não pode ser acessado via CREATE/ALTER EVENT SESSION DDL. Audite eventos e destinos nesta categoria além de um número pequeno de objetos usados internamente.<br /><br /> ===============<br /><br /> **Recursos de eventos**<br /><br /> -<br />                                **No_block**. O evento está em um caminho de código crítico que não pode ser bloqueado por nenhuma razão. Eventos com essa capacidade não podem ser adicionados a nenhuma sessão de evento que especifique NO_EVENT_LOSS.<br /><br /> ===============<br /><br /> **Recursos que se aplicam a todos os tipos de objeto**<br /><br /> -<br />                                **Process_whole_buffers**. O destino consome buffers de eventos de uma vez, em vez de evento após evento.<br /><br /> -<br />                        **Singleton**. Somente uma instância do destino pode existir em um processo. Embora várias sessões de evento possam referenciar o mesmo destino singleton, há realmente só uma instância e essa instância visualizará cada evento exclusivo somente uma vez. Isso será importante se o destino for adicionado a várias sessões que coletam o mesmo evento.<br /><br /> -<br />                                **Synchronous**. O destino é executado no thread que está gerando o evento, antes de o controle ser retornado à linha de código de chamada.|  
|type_name|**nvarchar(60)**|O nome para objetos pred_source e pred_compare. Permite valor nulo.|  
|type_package_guid|**uniqueidentifier**|O GUID do pacote que expõe o tipo no qual este objeto opera. Permite valor nulo.|  
|type_size|**int**|O tamanho, em bytes, do tipo de dados. Isto só é para tipos de objeto válidos. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|sys.dm_xe_objects.package_guid|sys.dm_xe_packages.guid|Muitos para um|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

