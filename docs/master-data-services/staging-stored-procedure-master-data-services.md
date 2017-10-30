---
title: Preparando procedimento armazenado (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
caps.latest.revision: 15
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 19ce25e1182e362761b1919f36d72623dd7289e7
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="staging-stored-procedure-master-data-services"></a>Preparando procedimento armazenado (Master Data Services)
  Ao iniciar o processo de preparo no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], você usa um entre três procedimentos armazenados.  
  
-   stg.udp_\<name>_Leaf  
  
-   stg.udp_\<name>_Consolidated  
  
-   stg.udp_\<name>_Relationship  
  
 Onde nome é o nome da tabela de preparo que foi especificada quando a entidade foi criada.  
  
## <a name="staging-process-stored-procedure-parameters"></a>Parâmetros do procedimento armazenado do processo de preparo  
 A tabela a seguir lista os parâmetros desses procedimentos armazenados.  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|**VersionName**<br /><br /> Required|O nome da versão. Pode ou não diferenciar maiúsculas de minúsculas, dependendo de sua configuração de agrupamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**LogFlag**<br /><br /> Required|Determina se as transações são registradas em log durante o processo de preparo. Os valores possíveis são:<br /><br /> **0**: não registrar transações em log.<br /><br /> **1**: registrar transações em log.<br /><br /> <br /><br /> Para obter mais informações sobre transações, consulte [Transações &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).|  
|**BatchTag**<br /><br /> Necessário, exceto pelo serviço Web|O valor **BatchTag** conforme especificado na tabela de preparo.|  
|**Batch_ID**<br /><br /> Necessário apenas pelo serviço Web|O valor **Batch_ID** , conforme especificado na tabela de preparo.|  
|**Nome do Usuário**|Parâmetro opcional|  
|**ID de usuário**|Parâmetro opcional|  
  
### <a name="staging-process-stored-procedure-example"></a>Exemplo de procedimento armazenado do processo de preparo  
 O exemplo a seguir mostra como iniciar o processo de preparo por meio do procedimento armazenado de preparo.  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
      @UserName=N’domain\user’  
  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimento armazenado de validação &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [Exibir erros que ocorrem durante o preparo &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)  
  
  

