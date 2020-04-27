---
title: Editar Modelo
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], changing name
ms.assetid: 399eed32-7c61-4239-9c06-996a65219518
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 89fa4dea57c4936a2d6a51e08f48668215ba53a2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728209"
---
# <a name="edit-model-master-data-services"></a>Editar Modelo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode alterar o nome e a descrição de um modelo e indicar durante quantos dias você deseja manter os logs de transação.  
  
 Para obter mais informações, consulte [Transações &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-change-a-model"></a>Para alterar um modelo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelo** , na barra de menus, aponte para **Gerenciar** e clique em **Modelos**.  
  
3.  Na página **Gerenciar Modelos** , na grade, selecione a linha do modelo com o nome ou descrição que você deseja alterar.  
  
4.  Clique em **Editar**.  
  
5.  Na caixa **Nome** , digite o nome atualizado do modelo.  
  
6.  No campo **Descrição** , digite a descrição atualizada do modelo.  
  
7.  No **dias de retenção de Log** selecione uma das opções para a retenção de dados de log. O valor padrão é **configuração do sistema**, que indica que o valor é herdado para configurações do sistema no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
     Para substituir a configuração do sistema sem remover os dados de log de transação, selecione **NÃO**. Para manter apenas os dados de log de hoje e truncar os dados de log para todos os dias anteriores, selecione **Sim** e defina o campo **dias** como 0. Para manter os dados de log para um número especificado de dias, selecione **Sim** e defina o campo **Dias** para o número de dias.  
  
8.  Clique em **Salvar modelo**.  
  
 A coluna **Status** na grade mostra o status da operação no modelo. Quando você clica no botão **salvar modelo** , a imagem de ![atualização](../master-data-services/media/mds-model-status-updating.png "Atualizando") é exibida, o que indica que o modelo está sendo atualizado. Se houver erros ao criar ou editar um modelo, a imagem de ![erro](../master-data-services/media/mds-model-status-error.png "Erro") será exibida. Caso contrário, o status será OK e a imagem ![OK](../master-data-services/media/mds-model-status-ok.png "OK") será exibida.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [Excluir um modelo &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [Modelos &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
  
