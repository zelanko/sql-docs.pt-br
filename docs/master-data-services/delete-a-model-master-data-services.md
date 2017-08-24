---
title: Excluir um modelo (Master Data Services) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting models [Master Data Services]
- models [Master Data Services], deleting models
ms.assetid: f0ad3cc4-aed7-47c8-94bc-2971fe9fe871
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be50aa7e9de502b0db2cb427bf894081196b579e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="delete-a-model-master-data-services"></a>Excluir um modelo (Master Data Services)
  Exclua um modelo para removê-lo juntamente com todos os seus dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
> [!NOTE]  
>  Quando esse procedimento estiver concluído, todos os objetos e dados de todas as versões do modelo serão excluídos permanentemente.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-a-model"></a>Para excluir um modelo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelo** , na barra de menus, aponte para **Gerenciar** e clique em **Modelos**.  
  
3.  Na página **Gerenciar Modelos** , na grade, selecione a linha do modelo que você deseja excluir.  
  
4.  Clique em **Excluir**.  
  
5.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
6.  Na caixa de diálogo de confirmação adicional, clique em **OK**.  
  
 A coluna **Status** na grade mostra o status da operação no modelo. Quando você clica o **Salvar modelo** botão, o ![atualização](../master-data-services/media/mds-model-status-updating.png "atualização") imagem for exibida, indicando que o modelo está atualizando. Se houver erros ao criar ou editar um modelo, o ![erro](../master-data-services/media/mds-model-status-error.png "erro") imagem é exibida. Caso contrário, o status será OK e a imagem ![OK](../master-data-services/media/mds-model-status-ok.png "OK") será exibida.  
  
## <a name="see-also"></a>Consulte também  
 [Modelos de &#40; Master Data Services &#41;](../master-data-services/models-master-data-services.md)   
 [Criar um modelo de &#40; Master Data Services &#41;](../master-data-services/create-a-model-master-data-services.md)  
  
  
