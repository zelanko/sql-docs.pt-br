---
title: Tabela de preparo de membros folha (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members staging table [Master Data Services]
- database [Master Data Services], members staging table
ms.assetid: a8c953da-ec20-47dc-8656-ed5f0dfed89b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b4e66dbfa26ea1e6090d128756a9542d349c9929
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971286"
---
# <a name="leaf-member-staging-table-master-data-services"></a>Tabela de preparo de membros folha (Master Data Services)
  Use a tabela de preparo de membros folha (stg.name_Leaf) no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para criar, atualizar, desativar e excluir membros folha. Você também pode usar isso para atualizar valores de atributos para membros folha.  
  
##  <a name="table-columns"></a><a name="TableColumns"></a>Colunas da tabela  
 A tabela a seguir explica para o que cada um dos campos da tabela de preparo Folha é usado.  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**ID**|Um identificador atribuído automaticamente. Não insira um valor nesse campo. Se o lote não tiver sido processado, esse campo estará em branco.|  
|**ImportType**<br /><br /> Obrigatório|Os valores de **ID** a seguir determinam o que fazer quando os dados testados correspondem aos dados que já existem no banco de dado [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] :<br /><br /> **0**: Criar novos membros. Substituir dados MDS existentes por dados preparados, mas apenas se os dados preparados não forem NULL. Valores NULL são ignorados. Para alterar o valor de atributo da cadeia de caracteres para NULL, defina-o como **~NULL~**. Para alterar o valor de atributo do número para NULL, defina-o como **-98765432101234567890**. Para alterar o valor de atributo de data e hora para NULL, defina-o como **5555-11-22T12:34:56**.<br /><br /> **1**: Criar apenas novos membros. Falha em quaisquer atualizações em dados MDS existentes.<br /><br /> **2**: Criar novos membros. Substituir dados MDS existentes por dados preparados. Se você importar valores NULL, eles substituirão os valores MDS existentes.<br /><br /> **3**: Desativar o membro, com base no valor do Código. Todos os atributos, membros da hierarquia e da coleção e transações são mantidos, mas não estão mais disponíveis na interface do usuário. Se o membro for usado como um valor de atributo baseado em domínio de outro membro, a desativação falhará. Consulte **ImportType5** para obter uma alternativa.<br /><br /> **4**: excluir permanentemente o membro, com base no valor do Código. Todos os atributos, membros da hierarquia e da coleção e transações são excluídos permanentemente. Se o membro for usado como um valor de atributo baseado em domínio de outro membro, a exclusão falhará. Consulte **ImportType6** para obter uma alternativa.<br /><br /> **5**: desativar o membro, com base no valor do **Código** . Todos os atributos, membros da hierarquia e da coleção e transações são mantidos, mas não estão mais disponíveis na interface do usuário. Se o membro for usado como um valor de atributo baseado em domínio de outros membros, os valores relativos serão definidos como NULL. ImportType 5 destina-se apenas a membros folha.<br /><br /> **6**: excluir permanentemente o membro, com base no valor do **Código** . Todos os atributos, membros da hierarquia e da coleção e transações são excluídos permanentemente. Se o membro for usado como um valor de atributo baseado em domínio de outros membros, os valores relativos serão definidos como NULL. ImportType 6 destina-se apenas a membros folha.|  
|**ImportStatus_ID**<br /><br /> Obrigatório|O status do processo de importação. Os valores possíveis são:<br /><br /> **0**, que você especifica para indicar que o registro está pronto para preparação.<br /><br /> **1**, que é atribuído automaticamente e indica que o processo de preparação do registro teve êxito.<br /><br /> **2**, que é atribuído automaticamente e indica que ocorreu uma falha no processo de preparação do registro.|  
|**Batch_ID**<br /><br /> Necessário apenas pelo serviço Web|Um identificador atribuído automaticamente que agrupa registros para preparo. Todos os membros do lote recebem esse identificador, que é exibido na interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na coluna **ID** .<br /><br /> Se o lote não tiver sido processado, esse campo estará em branco.|  
|**BatchTag**<br /><br /> Necessário, exceto pelo serviço Web|Um nome exclusivo para o lote, de até 50 caracteres.|  
|**ErrorCode**|Exibe um código de erro. Para todos os registros com um **ImportStatus_ID** de **2**, consulte [Erros de processo de preparo &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md).|  
|**Código**<br /><br /> Obrigatório, exceto quando códigos são gerados automaticamente para **ImportType1** ou **2**; consulte [Criação automática de código &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md) para obter mais informações|Um código exclusivo para o membro.|  
|**Nome**<br /><br /> Opcional|Um nome para o membro.|  
|**NewCode**|Use apenas se você estiver alterando o código do membro.|  
|\<Attribute name>|Existe uma coluna para cada atributo da entidade. Use com um **ImportType** de **0** ou **2**. Para atributos de forma livre, especifique o novo texto ou valor da cadeia de caracteres para o atributo. Para atributos baseados em domínio, especifique o código do membro que será o atributo. Para atributos de link, a URL deve iniciar com **http://**.<br /><br /> Observação: não é possível preparar atributos de arquivo.|  
  
##  <a name="did-this-article-help-you-were-listening"></a><a name="feedback"></a>Este artigo o ajuda? Estamos ouvindo  
 Quais são as informações que você está procurando? Você as localizou? Estamos ouvindo seus comentários para melhorar o conteúdo. Envie seus comentários para[sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Leaf%20Member%20Staging%20Table%20page)  
  
## <a name="see-also"></a>Consulte Também  
 [Carregar ou atualizar Membros no Master Data Services usando o processo de preparo](add-update-and-delete-data-master-data-services.md)   
 [Master Data Services de importação de dados &#40;&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [Exibir erros que ocorrem durante o processo de preparo &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [Erros de processo de preparo &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)  
  
  
