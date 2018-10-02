---
title: Histórico de revisão de membro (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 113069c5-12e6-48ec-b443-b42e14f77308
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 907c99e6d3acb5bbc66af72ecf594300e27ea14a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772344"
---
# <a name="member-revision-history-master-data-services"></a>Histórico de revisão de membro (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Um histórico de revisão de membro será registrado cada vez que um membro for alterado, se o tipo de log de transação da entidade for membro.  
  
 Para obter informações sobre tipos de log de transações, consulte [Alterar o tipo de log de transações de entidade &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md).  
  
 Históricos de revisão de membro são registrados quando ocorrem as alterações a seguir.  
  
-   Membros são criados, excluídos, reativados ou limpos.  
  
-   Valores de atributo são alterados.  
  
-   Membros são movidos em uma hierarquia ou coleção  
  
## <a name="view-and-manage-revision-history-by-entity"></a>Exibir e gerenciar histórico de revisão por entidade  
 Na área funcional do Gerenciador, você pode exibir as revisões de todos os membros da entidade. Se você tiver permissões de atualização, poderá reverter o membro para uma versão anterior.  
  
 **Para exibir e gerenciar o histórico da revisão**  
  
1.  Em [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], selecione o modelo e a versão e clique em **Gerenciador**.  
  
2.  Selecione a entidade do menu **Entidades** .  
  
3.  Clique em **Exibir Histórico** para exibir todos os dados históricos da entidade.  
  
4.  Clique em **Filtrar** para filtrar os dados.  
  
5.  Clique no cabeçalho da coluna para classificar os dados.  
  
6.  Se você tiver permissões de atualização, clique em **Reverter Membro** para reverter à versão selecionada.  
  
## <a name="view-and-manage-revision-history-by-member"></a>Exibir e gerenciar histórico de revisão por membro  
 Na área funcional do Gerenciador, você pode exibir as revisões para um membro, se tiver permissões de leitura no membro. Se você tiver permissões atualizadas, poderá reverter o membro a uma revisão anterior ou adicionar anotações à revisão.  
  
1.  Em [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], selecione o modelo e a versão e clique em **Gerenciador**.  
  
2.  Selecione a entidade do menu **Entidades** .  
  
3.  Selecione o membro.  
  
4.  Clique em **Exibir histórico** no painel à direita.  
  
## <a name="log-retention-setting"></a>Configuração de retenção de log  
 Você pode configurar quanto tempo os dados históricos são retidos, definindo a propriedade **Retenção de Log em Dias** nas configurações do sistema para o banco de dados do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] e definindo **Retenção de Log em Dias** ao criar ou editar um modelo.  
  
## <a name="related-task"></a>Tarefa relacionada  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Reverter histórico de revisão de membro|[Reverter histórico de revisões do membro &#40;Master Data Services&#41;](../master-data-services/rollback-member-revision-history-master-data-services.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)  
  
  
