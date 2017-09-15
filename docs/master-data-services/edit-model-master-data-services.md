---
title: Editar modelo (Master Data Services) | Microsoft Docs
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
- models [Master Data Services], changing name
ms.assetid: 399eed32-7c61-4239-9c06-996a65219518
caps.latest.revision: 9
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: ee796a4c002df4e0a843e7a663e60d4a7f24a398
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="edit-model-master-data-services"></a>Editar Modelo (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode alterar o nome e a descrição de um modelo e indicar durante quantos dias você deseja manter os logs de transação.  
  
 Para obter mais informações, consulte [Transações &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-change-a-model"></a>Para alterar um modelo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelo** , na barra de menus, aponte para **Gerenciar** e clique em **Modelos**.  
  
3.  Na página **Gerenciar Modelos** , na grade, selecione a linha do modelo com o nome ou descrição que você deseja alterar.  
  
4.  Clique em **Editar**.  
  
5.  Na caixa **Nome** , digite o nome atualizado do modelo.  
  
6.  No campo **Descrição** , digite a descrição atualizada do modelo.  
  
7.  No campo **Dias de Retenção de Log** , selecione uma das opções para a retenção de dados de log. O valor padrão é **configuração do sistema**, que indica que o valor é herdado para configurações do sistema no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
     Para substituir a configuração do sistema sem remover os dados de log de transação, selecione **NÃO**. Para manter somente os dados de log de hoje e dados de truncamento do log para todos os últimos dias, selecione **Sim** e defina o campo **Dias** como 0. Para manter os dados de log para um número especificado de dias, selecione **Sim** e defina o campo **Dias** para o número de dias.  
  
8.  Clique em **Salvar modelo**.  
  
 A coluna **Status** na grade mostra o status da operação no modelo. Quando você clica no botão **Salvar modelo**, a imagem ![Atualizando](../master-data-services/media/mds-model-status-updating.png "Atualizando") é exibida, indicando que o modelo está sendo atualizando. Se houver erros ao criar ou editar um modelo, a imagem ![Erro](../master-data-services/media/mds-model-status-error.png "Erro") será exibida. Caso contrário, o status será OK e a imagem ![OK](../master-data-services/media/mds-model-status-ok.png "OK") será exibida.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [Excluir um modelo &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [Modelos &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
  
