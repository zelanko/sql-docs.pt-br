---
title: Recursos do Master Data Services preteridos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: lrtoyou1223
ms.author: lle
manager: erikre
ms.openlocfilehash: d08fd9bbb91a3783cf176f150fc966d1b44a2fc4
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65485279"
---
# <a name="deprecated-master-data-services-features"></a>Recursos preteridos do Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve os recursos substituídos do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que ainda estão disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Esses recursos estão programados para serem removidos em uma versão futura do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Recursos preteridos não devem ser usados em aplicativos novos.  
  
## <a name="explicit-hierarchies-collections-and-related-components"></a>Hierarquias explícitas, coleções e componentes relacionados  
 Hierarquias explícitas, coleções e componentes relacionados são preteridos. Membros que antes foram modelados como tipos de membro consolidado (pai de hierarquia explícita) e tipos de membro de coleção serão modelados como membros folha em hierarquias derivadas. Os novos recursos a seguir permitem que hierarquias derivadas tomem o lugar de hierarquias explícitas.  
  
-   Hierarquias derivadas recursivas agora podem ser usadas para atribuir permissões de segurança de membro.  
  
     Uma hierarquia explícita é análoga a uma hierarquia derivada recursiva com um único nível não-recursivo abaixo do nível recursivo. Uma hierarquia derivada recursiva pode ser complexa, incluindo níveis abaixo e/ou acima de um nível recursivo.  
  
-   No Explorer, a página de hierarquia derivada agora mostra membros não atribuídos (não usados) para cada nível de hierarquia. Nós não utilizados são agrupados por nível de hierarquia. Os membros podem ser movidos entre os nós Raiz e Não Utilizado, arrastando e soltando ou então recortando e colando.  
  
     Na Administração do Sistema, nós não utilizados são visíveis no painel **Visualização** . Em Segurança, nós não utilizados são visíveis no painel **Permissões de Membro de Hierarquia** . Qualquer membro, seja sob um nó **Raiz** ou um nó **Não Utilizado** , podem ser atribuídos a uma permissão. Os pseudomembros **Raiz**, **Não Utilizado**e **Não Utilizado** também podem ter permissões atribuídas a eles.  
  
-   O procedimento armazenado, mdm.udpConvertCollectionAndConsolidatedMembersToLeaf, converte hierarquias explícitas em hierarquias derivadas recursivas e converte membros consolidados e de coleção em membros folha.  
  
     Tipos de membros de coleção, consolidados e hierarquias explícitas ainda têm suporte, portanto, executar o procedimento armazenado é opcional. No entanto, se você usar esses itens é recomendável que você execute o procedimento armazenado porque eles são preteridos.  
  
 Para obter informações sobre hierarquias explícitas, coleções e membros consolidados, consulte os tópicos a seguir.  
  
-   [Hierarquias explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [Coleções &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
-   [Membros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
## <a name="attribute-entity-transaction-log-type"></a>Tipo de log de transações da entidade Atributo  
O tipo de log de transações da entidade “Atributo” foi preterido. Migre para o tipo de log de transações da entidade “Membro”. Para obter informações sobre tipos de log de transação de entidade, consulte o seguinte tópico:
* [Alterar o Tipo de Log de Transações de Entidade (Master Data Services)](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)
* [Histórico de revisão de membro](../master-data-services/member-revision-history-master-data-services.md)
  
## <a name="external-resources"></a>Recursos externos  
 Postagem no blog, [Preterido: Hierarquias e coleções explícitas](https://go.microsoft.com/fwlink/p/?LinkId=615373), no msdn.com.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos descontinuados do Master Data Services](../master-data-services/discontinued-master-data-services-features.md)  
  
  
