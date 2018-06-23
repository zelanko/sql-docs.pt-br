---
title: Excluir uma regra de negócios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d64a01cf9df6865790b39510ad5c6222d8d6fd87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119545"
---
# <a name="exclude-a-business-rule-master-data-services"></a>Apagar uma regra de negócio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], exclua uma regra de negócio quando não desejar removê-la permanentemente, nem validar dados em relação a ela.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-exclude-a-business-rule"></a>Para excluir uma regra de negócios  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Manutenção de Regra de Negócio** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Entidade** , selecione uma entidade.  
  
5.  Do **tipo de membro** , selecione um tipo de membro.  
  
6.  Na lista **Atributo** , selecione um atributo ou deixe o valor padrão **Todos**.  
  
7.  Na grade, na linha da regra de negócio, marque a caixa de seleção no **excluir** coluna. O valor de **Status** coluna é **exclusão pendente**.  
  
8.  Clique em **Publicar regras de negócio**.  
  
9. Na caixa de diálogo de confirmação, clique em **OK**. O valor de **Status** coluna é **excluídas**.  
  
## <a name="see-also"></a>Consulte também  
 [Excluir uma regra de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-business-rule-master-data-services.md)   
 [Criar e publicar uma regra de negócios &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  