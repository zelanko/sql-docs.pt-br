---
title: "Leaf Member Staging Table (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "members staging table [Master Data Services]"
  - "banco de dados [Master Data Services], tabela de preparo de membros"
ms.assetid: a8c953da-ec20-47dc-8656-ed5f0dfed89b
caps.latest.revision: 14
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 14
---
# Leaf Member Staging Table (Master Data Services)
  Use os membros folha (stg.name_Leaf) da tabela de preparo no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] banco de dados para criar, atualizar, desativar e excluir membros folha. Você também pode usar isso para atualizar valores de atributos para membros folha.  
  
##  <a name="TableColumns"></a> Colunas da tabela  
 A tabela a seguir explica para o que cada um dos campos da tabela de preparo Folha é usado.  
  
|Nome da coluna|Descrição|Valores|  
|-----------------|-----------------|------------|  
|**ID**|Um identificador atribuído automaticamente.|Não insira um valor nesse campo. Se o lote não tiver sido processado, esse campo estará em branco.|  
|**ImportType**<br /><br /> Required|Determina o que fazer quando dados preparados correspondem a dados existentes no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|**0**: Criar novos membros. Substituir dados MDS existentes por dados preparados, mas apenas se os dados preparados não forem NULL. Valores NULL são ignorados. Para alterar o valor de atributo da cadeia de caracteres para NULL, defina-o como **~NULL~**. Para alterar um valor de atributo de número para NULL, defina-o como **-98765432101234567890**. Para alterar um valor de atributo de data e hora para NULL, defina-o como **5555-11-22T12:34:56**.<br /><br /> **1**: Criar apenas novos membros. Falha em quaisquer atualizações em dados MDS existentes.<br /><br /> **2**: Criar novos membros. Substituir dados MDS existentes por dados preparados. Se você importar valores NULL, eles substituirão os valores MDS existentes.<br /><br /> **3**: Desativar o membro, com base no valor do Código. Todos os atributos, membros da hierarquia e da coleção e transações são mantidos, mas não estão mais disponíveis na interface do usuário. Se o membro for usado como um valor de atributo baseado em domínio de outro membro, a desativação falhará. Consulte **ImportType5** para uma alternativa.<br /><br /> **4**: excluir permanentemente o membro, com base no valor do Código. Todos os atributos, membros da hierarquia e da coleção e transações são excluídos permanentemente. Se o membro for usado como um valor de atributo baseado em domínio de outro membro, a exclusão falhará. Consulte **ImportType6** para uma alternativa.<br /><br /> **5**: desativar o membro, com base no valor do **Código** . Todos os atributos, membros da hierarquia e da coleção e transações são mantidos, mas não estão mais disponíveis na interface do usuário. Se o membro for usado como um valor de atributo baseado em domínio de outros membros, os valores relativos serão definidos como NULL. ImportType 5 destina-se apenas a membros folha.<br /><br /> **6**: excluir permanentemente o membro, com base no valor do **Código** . Todos os atributos, membros da hierarquia e da coleção e transações são excluídos permanentemente. Se o membro for usado como um valor de atributo baseado em domínio de outros membros, os valores relativos serão definidos como NULL. ImportType 6 destina-se apenas a membros folha.|  
|**ImportStatus_ID**<br /><br /> Required|O status do processo de importação.|**0**, que você especifica para indicar que o registro está pronto para preparação.<br /><br /> **1**, que é atribuído automaticamente e indica que o processo de preparação do registro teve êxito.<br /><br /> **2**, que é atribuído automaticamente e indica que ocorreu uma falha no processo de preparação do registro.|  
|**Batch_ID**<br /><br /> Necessário apenas pelo serviço Web|Um identificador atribuído automaticamente que agrupa registros para preparo. Todos os membros do lote recebem esse identificador, que é exibido na interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na coluna **ID** .|Se o lote não tiver sido processado, esse campo estará em branco.|  
|**BatchTag**<br /><br /> Necessário, exceto pelo serviço Web|Um nome exclusivo para o lote, de até 50 caracteres.||  
|**ErrorCode**|Exibe um código de erro. Para todos os registros com um **ImportStatus_ID** de **2**, consulte [processar erros de preparo e 40; Master Data Services & 41;](../master-data-services/staging-process-errors-master-data-services.md).||  
|**Código**<br /><br /> Necessário, exceto quando códigos são gerados automaticamente para **ImportType1** ou **2**; consulte [criação automática de código e 40; Master Data Services & 41;](../master-data-services/automatic-code-creation-master-data-services.md) Para obter mais informações|Um código exclusivo para o membro.||  
|**Nome**<br /><br /> Opcional|Um nome para o membro.||  
|**NewCode**|Use apenas se você estiver alterando o código do membro.||  
|\< nome do atributo>|Existe uma coluna para cada atributo da entidade. Use com um **ImportType** de **0** ou **2**. Para atributos de forma livre, especifique o novo texto ou valor da cadeia de caracteres para o atributo. Para atributos baseados em domínio, especifique o código do membro que será o atributo. Para atributos de link, a URL deve começar com **http://**.<br /><br /> Observação: não é possível preparar atributos de arquivo.||  
  
## Consulte também  
 [Visão geral: Importação de dados de tabelas e 40; Master Data Services & 41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Exibir erros que ocorrem durante a preparação & #40. Master Data Services & 41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [Erros de processo de preparação e 40; Master Data Services & 41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
  