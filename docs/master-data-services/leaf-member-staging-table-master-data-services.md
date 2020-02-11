---
title: Tabela de preparo de membros folha
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members staging table [Master Data Services]
- database [Master Data Services], members staging table
ms.assetid: a8c953da-ec20-47dc-8656-ed5f0dfed89b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 626452bb0247b355cff7e8f1e9584e2fdc0c32c9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73729057"
---
# <a name="leaf-member-staging-table-master-data-services"></a>Tabela de preparo de membros folha (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Use a tabela de preparo de membros folha (stg.name_Leaf) no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para criar, atualizar, desativar e excluir membros folha. Você também pode usar isso para atualizar valores de atributos para membros folha.  
  
##  <a name="TableColumns"></a>Colunas da tabela  
 A tabela a seguir explica para o que cada um dos campos da tabela de preparo Folha é usado.  
  
|Nome da coluna|DESCRIÇÃO|Valores|  
|-----------------|-----------------|------------|  
|**SESSÃO**|Um identificador atribuído automaticamente.|Não insira um valor nesse campo. Se o lote não tiver sido processado, esse campo estará em branco.|  
|**ImportType**<br /><br /> Obrigatório|Determina o que fazer quando dados preparados correspondem a dados existentes no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|**0**: criar novos membros. Substituir dados MDS existentes por dados preparados, mas apenas se os dados preparados não forem NULL. Valores NULL são ignorados. Para alterar o valor de atributo da cadeia de caracteres para NULL, defina-o como **~NULL~**. Para alterar o valor de atributo do número para NULL, defina-o como **-98765432101234567890**. Para alterar o valor de atributo de data e hora para NULL, defina-o como **5555-11-22T12:34:56**.<br /><br /> **1**: criar novos membros apenas. Falha em quaisquer atualizações em dados MDS existentes.<br /><br /> **2**: criar novos membros. Substituir dados MDS existentes por dados preparados. Se você importar valores NULL, eles substituirão os valores MDS existentes.<br /><br /> **3**: desativar o membro, com base no valor do código. Todos os atributos, membros da hierarquia e da coleção e transações são mantidos, mas não estão mais disponíveis na interface do usuário. Se o membro for usado como um valor de atributo baseado em domínio de outro membro, a desativação falhará. Consulte **ImportType5** para obter uma alternativa.<br /><br /> **4**: excluir permanentemente o membro, com base no valor do código. Todos os atributos, membros da hierarquia e da coleção e transações são excluídos permanentemente. Se o membro for usado como um valor de atributo baseado em domínio de outro membro, a exclusão falhará. Consulte **ImportType6** para obter uma alternativa.<br /><br /> **5**: desativar o membro, com base no valor do **código** . Todos os atributos, membros da hierarquia e da coleção e transações são mantidos, mas não estão mais disponíveis na interface do usuário. Se o membro for usado como um valor de atributo baseado em domínio de outros membros, os valores relativos serão definidos como NULL. ImportType 5 destina-se apenas a membros folha.<br /><br /> **6**: excluir permanentemente o membro, com base no valor do **código** . Todos os atributos, membros da hierarquia e da coleção e transações são excluídos permanentemente. Se o membro for usado como um valor de atributo baseado em domínio de outros membros, os valores relativos serão definidos como NULL. ImportType 6 destina-se apenas a membros folha.|  
|**ImportStatus_ID**<br /><br /> Obrigatório|O status do processo de importação.|**0**, que você especifica para indicar que o registro está pronto para preparo.<br /><br /> **1**, que é atribuído automaticamente e indica que o processo de preparo para o registro foi bem-sucedido.<br /><br /> **2**, que é atribuído automaticamente e indica que o processo de preparo do registro falhou.|  
|**Batch_ID**<br /><br /> Necessário apenas pelo serviço Web|Um identificador atribuído automaticamente que agrupa registros para preparo. Todos os membros do lote recebem esse identificador, que é exibido na interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na coluna **ID** .|Se o lote não tiver sido processado, esse campo estará em branco.|  
|**BatchTag**<br /><br /> Necessário, exceto pelo serviço Web|Um nome exclusivo para o lote, de até 50 caracteres.||  
|**ErrorCode**|Exibe um código de erro. Para todos os registros com um **ImportStatus_ID** de **2**, consulte [Erros de processo de preparo &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).||  
|**Código**<br /><br /> Obrigatório, exceto quando códigos são gerados automaticamente para **ImportType1** ou **2**; consulte [Criação automática de código &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md) para obter mais informações|Um código exclusivo para o membro.||  
|**Nome**<br /><br /> Opcional|Um nome para o membro.||  
|**NewCode**|Use apenas se você estiver alterando o código do membro.||  
|\<Nome do atributo>|Existe uma coluna para cada atributo da entidade. Use com um **ImportType** de **0** ou **2**. Para atributos de forma livre, especifique o novo texto ou valor da cadeia de caracteres para o atributo. Para atributos baseados em domínio, especifique o código do membro que será o atributo. Para atributos de link, a URL deve iniciar com **https://**.<br /><br /> Observação: não é possível preparar atributos de arquivo.||  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral: importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Exibir erros que ocorrem durante o preparo &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [Erros de processo de preparo &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
  
