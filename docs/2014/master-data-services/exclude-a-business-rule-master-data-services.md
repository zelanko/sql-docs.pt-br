---
title: Excluir uma regra de negócios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8f18e047b11bee4093ce7a6e494c1ae1bf3d0ada
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483380"
---
# <a name="exclude-a-business-rule-master-data-services"></a>Apagar uma regra de negócio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], exclua uma regra de negócio quando não desejar removê-la permanentemente, nem validar dados em relação a ela.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-exclude-a-business-rule"></a>Para excluir uma regra de negócios  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Manutenção de Regra de Negócio** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Entidade** , selecione uma entidade.  
  
5.  Na lista **tipo de membro** , selecione um tipo de membro.  
  
6.  Na lista **Atributo** , selecione um atributo ou deixe o valor padrão **Todos**.  
  
7.  Na grade, na linha da regra de negócio, marque a caixa de seleção na coluna **excluir** . O valor na coluna **status** é **exclusão pendente**.  
  
8.  Clique em **Publicar regras de negócio**.  
  
9. Na caixa de diálogo de confirmação, clique em **OK**. O valor na coluna **status** é **excluído**.  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir uma regra de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-business-rule-master-data-services.md)   
 [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
