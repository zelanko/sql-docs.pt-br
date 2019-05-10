---
title: Limpar Membros de Versão (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: adecce2d-46bb-49ff-8be9-0b31b8dd3cb6
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 9834e79746feb3e7890ab8b6d5bdd43bbfc36dbb
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65486028"
---
# <a name="purge-version-members-master-data-services"></a>Limpar Membros de Versão (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], excluir um membro apenas o desativa ou exclui temporariamente. Os dados ainda permanecem no banco de dados. Este tópico descreve como limpar (excluir permanentemente) todos os membros excluídos temporariamente em uma versão de modelo.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento.  
  
-   Você deve ter permissão para acessar a área funcional Gerenciamento de Versões.  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
## <a name="to-purge-soft-deleted-members"></a>Para limpar membros excluídos  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Gerenciamento de Versões**.  
  
2.  Na página **Gerenciar Versões** , selecione o modelo que tem a versão que você deseja limpar. A lista de versões de modelos é exibida.  
  
3.  Selecione a linha da versão que você deseja limpar.  
  
4.  Clique em **Limpar Membros**.  
  
5.  No prompt de confirmação, clique em "OK".  
  
## <a name="additional-methods-to-purge-members"></a>Métodos Adicionais para Limpar Membros  
 A limpeza de membros da versão exclui permanentemente membros excluídos temporariamente em todas as entidades que pertencem à versão selecionada. Uma alternativa mais granular é usar o preparo de base da entidade para excluir permanentemente apenas os membros específicos de uma entidade. Além disso, os administradores de entidades com permissão funcional do Explorer podem limpar uma versão de entidade na página do gerenciador de entidades.  
  
 Para obter mais informações, consulte [Tabela de preparo de membros folha &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
  
