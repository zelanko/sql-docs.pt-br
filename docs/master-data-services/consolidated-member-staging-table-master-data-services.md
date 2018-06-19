---
title: Tabela de preparo de membros consolidados (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], attributes staging table
- attributes staging table [Master Data Services]
ms.assetid: 070681ed-be99-49ae-93bd-6402f2134ace
caps.latest.revision: 14
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 8fca9f6a5d0389ec61aca30357b71e52041d59e7
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35333890"
---
# <a name="consolidated-member-staging-table-master-data-services"></a>Tabela de preparo de membros consolidados (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Use a tabela de preparo de membros consolidados (stg.name_Consolidated) no banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para criar, atualizar, desativar e excluir membros consolidados. Você também pode usar isso para atualizar valores de atributos para membros consolidados.  
  
##  <a name="TableColumns"></a> Colunas da tabela  
 A tabela a seguir explica para o que cada um dos campos da tabela de preparo Consolidado é usado.  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**ID**|Um identificador atribuído automaticamente. Não insira um valor nesse campo. Se o lote não tiver sido processado, esse campo estará em branco.|  
|**ImportType**<br /><br /> Obrigatório|Determina o que fazer quando dados preparados correspondem a dados existentes no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> **0**: Criar novos membros. Substituir dados MDS existentes por dados preparados, mas apenas se os dados preparados não forem NULL. Valores NULL são ignorados. Para alterar um valor de atributo para NULL, use **~NULL~**.<br /><br /> **1**: Criar apenas novos membros. Falha em quaisquer atualizações em dados MDS existentes.<br /><br /> **2**: Criar novos membros. Substituir dados MDS existentes por dados preparados. Se você importar valores NULL, eles substituirão os valores MDS existentes.<br /><br /> **3**: Desativar o membro, com base no valor do Código. Todos os atributos, membros da hierarquia e da coleção e transações são mantidos, mas não estão mais disponíveis na interface do usuário. Se o membro for usado como um valor de atributo baseado em domínio de outro membro, a desativação falhará.<br /><br /> **4**: excluir permanentemente o membro, com base no valor do Código. Todos os atributos, membros da hierarquia e da coleção e transações são excluídos permanentemente. Se o membro for usado como um valor de atributo baseado em domínio de outro membro, a exclusão falhará.|  
|**ImportStatus_ID**<br /><br /> Obrigatório|O status do processo de importação. Os valores possíveis são:<br /><br /> **0**, que você especifica para indicar que o registro está pronto para preparação.<br /><br /> **1**, que é atribuído automaticamente e indica que o processo de preparação do registro teve êxito.<br /><br /> **2**, que é atribuído automaticamente e indica que ocorreu uma falha no processo de preparação do registro.|  
|**Batch_ID**<br /><br /> Necessário apenas pelo serviço Web|Um identificador atribuído automaticamente que agrupa registros para preparo. Todos os membros do lote recebem esse identificador, que é exibido na interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na coluna **ID** .<br /><br /> Se o lote não tiver sido processado, esse campo estará em branco.|  
|**BatchTag**<br /><br /> Necessário, exceto pelo serviço Web|Um nome exclusivo para o lote, de até 50 caracteres.|  
|**HierarchyName**<br /><br /> Obrigatório|O nome da hierarquia explícita. Cada membro consolidado pode pertencer a apenas uma hierarquia.|  
|**ErrorCode**|Exibe um código de erro. Para todos os registros com um **ImportStatus_ID** de **2**, consulte [Erros de processo de preparo &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).|  
|**Code**<br /><br /> Obrigatório, exceto quando códigos são gerados automaticamente para **ImportType1** ou **2**; consulte [Criação automática de código &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md) para obter mais informações|Um código exclusivo para o membro.|  
|**Nome**<br /><br /> Opcional|Um nome para o membro.|  
|**NewCode**|Use apenas se você estiver alterando o código do membro.|  
|\<Nome do atributo>|Existe uma coluna para cada atributo da entidade. Use com um **ImportType** de **0** ou **2**. Para atributos de forma livre, especifique o novo texto ou valor da cadeia de caracteres para o atributo. Para atributos baseados em domínio, especifique o código do membro que será o atributo. Para atributos de link, a URL deve iniciar com **http://**.<br /><br /> <br /><br /> Observação: não é possível preparar atributos de arquivo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Exibir erros que ocorrem durante o preparo &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [Erros de processo de preparo &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
  
