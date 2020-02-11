---
title: Preparando procedimento armazenado (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8647a1a4529f7c7d4a8258eac5b726da203c7df9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482720"
---
# <a name="staging-stored-procedure-master-data-services"></a>Preparando procedimento armazenado (Master Data Services)
  Ao iniciar o processo de preparo no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], você usa um entre três procedimentos armazenados.  
  
-   stg.udp_name_Leaf  
  
-   stg.udp_name_Consolidated  
  
-   stg.udp_name_Relationship  
  
 Onde nome é o nome da tabela de preparo que foi especificada quando a entidade foi criada.  
  
## <a name="staging-process-stored-procedure-parameters"></a>Parâmetros do procedimento armazenado do processo de preparo  
 A tabela a seguir lista os parâmetros desses procedimentos armazenados.  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|**VersionName**<br /><br /> Obrigatório|O nome da versão. Pode ou não diferenciar maiúsculas de minúsculas, dependendo de sua configuração de ordenação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|**LogFlag**<br /><br /> Obrigatório|Determina se as transações são registradas em log durante o processo de preparo. Os valores possíveis são:<br /><br /> **0**: não registrar transações em log.<br />**1**: transações de log.<br /><br /> <br /><br /> Para obter mais informações sobre transações, consulte [Transações &#40;Master Data Services&#41;](transactions-master-data-services.md).|  
|**BatchTag**<br /><br /> Necessário, exceto pelo serviço Web|O valor **BatchTag** conforme especificado na tabela de preparo.|  
|**Batch_ID**<br /><br /> Necessário apenas pelo serviço Web|O valor **Batch_ID** , conforme especificado na tabela de preparo.|  
  
### <a name="staging-process-stored-procedure-example"></a>Exemplo de procedimento armazenado do processo de preparo  
 O exemplo a seguir mostra como iniciar o processo de preparo por meio do procedimento armazenado de preparo.  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimento armazenado de validação &#40;Master Data Services&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)   
 [Carregar ou atualizar Membros no Master Data Services usando o processo de preparo](add-update-and-delete-data-master-data-services.md)   
 [Exibir erros que ocorrem durante o processo de preparo &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)  
  
  
