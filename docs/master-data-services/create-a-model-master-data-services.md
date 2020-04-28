---
title: Criar um modelo
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], creating models
- creating models [Master Data Services]
ms.assetid: 9bb3b3b3-bde8-44aa-ad62-eaae21188141
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 730e18fca866891d62b68d321ec13e4be5da59bf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728486"
---
# <a name="create-a-model-master-data-services"></a>Criar um modelo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um modelo para conter objetos de modelo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-model"></a>Para criar um modelo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelo** , na barra de menus, aponte para **Gerenciar** e clique em **Modelos**.  
  
3.  Na página **Gerenciar Modelos** , clique em **Adicionar**. Um painel é exibido no lado direito.  
  
4.  Na caixa **Nome** , digite o nome do modelo.  
  
5.  (Opcionalmente) No campo **Descrição** , digite a descrição do modelo.  
  
6.  No **dias de retenção de Log** selecione uma das opções para a retenção de dados de log. O valor padrão é **configuração do sistema**, que indica que o valor é herdado para configurações do sistema no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
     Para substituir a configuração do sistema sem remover os dados de log de transação, selecione **NÃO**. Para manter apenas os dados de log de hoje e truncar os dados de log para todos os dias anteriores, selecione **Sim** e defina o campo **dias** como 0. Para manter os dados de log para um número especificado de dias, selecione **Sim** e defina o campo **Dias** para o número de dias.  
  
7.  Como opção, selecione **Criar entidade com o mesmo nome que o modelo** para criar uma entidade com o mesmo nome do modelo.  
  
8.  Clique em **Salvar modelo**.  
  
 Para cada modelo criado, uma linha com oito colunas é adicionada à grade. As oito colunas são:  
  
-   **Status**: o status do modelo. Quando você clica no botão **salvar modelo** , a imagem de ![atualização](../master-data-services/media/mds-model-status-updating.png "Atualizando") é exibida, o que indica que o modelo está sendo atualizado. Se houver erros ao criar ou editar um modelo, a imagem de ![erro](../master-data-services/media/mds-model-status-error.png "Erro") será exibida. Caso contrário, o status será OK e a imagem ![OK](../master-data-services/media/mds-model-status-ok.png "OK") será exibida.  
  
-   **Nome**: o nome do modelo.  
  
-   **Descrição**: A descrição do modelo.  
  
-   **Dias de Retenção de Log**: O número de dias pelos quais o log é retido para o modelo.  
  
-   **Criado Por**: o nome do usuário que criou o modelo.  
  
-   **Data e Hora da Criação**: a data e hora em que o modelo foi criado.  
  
-   **Atualizado Por**: o nome de usuário do usuário que atualizou o modelo pela última vez.  
  
-   **Data e Hora da Atualização**: a data e hora em que o modelo foi atualizado.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Modelos &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)   
 [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)   
 [Excluir um modelo &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [Editar &#40;de Master Data Services de modelo&#41;](../master-data-services/edit-model-master-data-services.md)   
 [Transações &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
  
