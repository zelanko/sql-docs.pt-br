---
title: catalog.event_message_context | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 273a54f8-b107-4f36-9461-2b475644760d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: cb5add10328aaa4e7c3d1d49b7ac4ebdd8f2e658
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038373"
---
# <a name="catalogeventmessagecontext"></a>catalog.event_message_context 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe informações sobre as condições que são associadas às mensagens de evento de execução, para execuções no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|Context_id|BIGINT|ID exclusiva do contexto de erro.|  
|Event_message_id|BIGINT|ID exclusiva da mensagem à qual o contexto está relacionado.|  
|Context_depth|INT|À medida que a profundidade aumenta, o contexto do erro é mais detalhado. Quando um erro ocorre, a profundidade de contexto começa em 1. O valor de 0 indica o estado do pacote antes do início da execução.|  
|Package_path|Nvarchar(max)|O caminho do pacote para a origem de contexto.|  
|Context_type|SMALLINT|O tipo do objeto que é a origem do contexto. Consulte a seção **Comentários** para obter uma lista de tipos de contexto.|  
|Context_source_name|Nvarchar(4000)|O nome do objeto que é a origem do contexto.|  
|Context_source_id|Nvarchar(38)|A ID exclusiva do objeto que é a origem do contexto.|  
|Property_name|Nvarchar(4000)|O nome da propriedade associada à origem do contexto.|  
|Property_value|Sql_variant|O valor da propriedade associada à origem do contexto.|  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir lista os tipos de contexto.  
  
||||  
|-|-|-|  
|Valor do tipo de contexto|Nome do Tipo|Descrição|  
|10|Tarefa|Estado de uma tarefa quando um erro ocorreu.|  
|20|Pipeline|Erro de um componente de pipeline: origem, destino ou componente de transformação.|  
|30|Sequência|Estado de uma sequência.|  
|40|Loop For|Estado de um Loop For.|  
|50|Loop Foreach|Estado de um Loop Foreach.|  
|60|Pacote|Estado de um pacote quando um erro ocorreu.|  
|70|Variável|Valor da variável|  
|80|Gerenciador de conexões|Propriedades de um gerenciador de conexões.|  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na operação  
  
-   Associação à função de banco de dados **ssis_admin**.  
  
-   Associação à função de servidor **sysadmin**.  
  
  
