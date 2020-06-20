---
title: Tabela de preparo de relações (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 529d0521c320ff2e893a2269fe020d191a6ce284
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960686"
---
# <a name="relationship-staging-table-master-data-services"></a>Tabela de preparo de relações (Master Data Services)
  Use a tabela de preparo de relação (stg.name_Relationship) no banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para alterar o local dos membros em uma hierarquia explícita, com base na relação que os membros têm entre si.  
  
##  <a name="table-columns"></a><a name="TableColumns"></a>Colunas da tabela  
 A tabela a seguir explica para o que cada um dos campos da tabela de preparo Relação é usado.  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**ID**|Um identificador atribuído automaticamente. Não insira um valor nesse campo. Se o lote não tiver sido processado, esse campo estará em branco.|  
|**RelationshipType**<br /><br /> Obrigatório|O tipo de relação que está sendo definido. Os valores possíveis são:<br /><br /> **1**: pai<br /><br /> **2**: irmão (no mesmo nível)|  
|**ImportStatus_ID**<br /><br /> Obrigatório|O status do processo de importação. Os valores possíveis são:<br /><br /> **0**, que você especifica para indicar que o registro está pronto para preparação.<br /><br /> **1**, que é atribuído automaticamente e indica que o processo de preparação do registro teve êxito.<br /><br /> **2**, que é atribuído automaticamente e indica que ocorreu uma falha no processo de preparação do registro.|  
|**Batch_ID**<br /><br /> Necessário apenas pelo serviço Web|Um identificador atribuído automaticamente que agrupa registros para preparo. Todos os membros do lote recebem esse identificador, que é exibido na interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na coluna **ID** .<br /><br /> Se o lote não tiver sido processado, esse campo estará em branco.|  
|**BatchTag**<br /><br /> Necessário, exceto pelo serviço Web|Um nome exclusivo para o lote, de até 50 caracteres.|  
|**HierarchyName**<br /><br /> Obrigatório|O nome da hierarquia explícita. Cada membro consolidado pode pertencer a apenas uma hierarquia.|  
|**ParentCode**<br /><br /> Obrigatório|Para relações pai-filho, o código do membro consolidado que será o pai da folha filho ou do membro consolidado.<br /><br /> Para relações de irmão, o código de um dos irmãos.|  
|**ChildCode**<br /><br /> Obrigatório|Para relações pai-filho, o código do membro consolidado ou folha que será o filho.<br /><br /> Para relações de irmão, o código de um dos irmãos.|  
|**Ordem de classificação**<br /><br /> Opcional|Um inteiro que indica a ordem do membro em relação aos outros membros sob o pai. Cada membro filho deve ter um identificador exclusivo.|  
|**ErrorCode**|Exibe um código de erro. Para todos os registros com um **ImportStatus_ID** de **2**, consulte [Erros de processo de preparo &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Mover membros de hierarquia explícitos usando o processo de preparo &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Master Data Services de importação de dados &#40;&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [Exibir erros que ocorrem durante o processo de preparo &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [Erros de processo de preparo &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)  
  
  
