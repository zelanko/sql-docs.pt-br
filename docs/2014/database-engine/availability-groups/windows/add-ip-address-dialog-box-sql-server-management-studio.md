---
title: Caixa de diálogo Adicionar Endereço IP (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygrouplistener.addipaddress.f1
ms.assetid: 98c9ad3b-ff3c-4c1d-b344-59a72fca137c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68bd85258bd3fd259386f020394ffb5bc70a9781
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791910"
---
# <a name="add-ip-address-dialog-box-sql-server-management-studio"></a>Caixa de diálogo Adicionar Endereço IP (SQL Server Management Studio)
  Este tópico da Ajuda F1 descreve as opções especificadas da caixa de diálogo **Adicionar Endereço IP** . Essa caixa de diálogo acessada na caixa de diálogo **Novo Ouvinte de Grupo de Disponibilidade** e na guia **Ouvinte** da página **Especificar Réplicas** do [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] ou [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Antes de você começar a adicionar sub-redes a um ouvinte do grupo de disponibilidade, verifique se você sabe o endereço IP de cada sub-rede e, para um endereço IPv4, a máscara de sub-rede.  
  
##  <a name="PageOptions"></a> Adicionar opções de endereço IP  
 **Sub-rede**  
 Use a lista suspensa para selecionar um endereço para a sub-rede que você está adicionando ao ouvinte do grupo de disponibilidade. Por padrão, uma sub-rede possui um endereço IPv4 e um endereço IPv6. Na primeira vez que você usa a caixa de diálogo **Adicionar Endereço IP** , a lista suspensa **Sub-rede** exibe os endereços de sub-rede de cada sub-rede que hospeda uma réplica para o grupo de disponibilidade. Para adicionar uma determinada sub-rede ao ouvinte, selecione um de seus endereços de sub-rede.  
  
 Depois de concluir a caixa de diálogo **Adicionar Endereço IP** e clicar em **OK** para adicionar um endereço de sub-rede selecionado ao ouvinte, a lista suspensa **Sub-rede** filtra esse endereço de sub-rede. Todos os endereços de sub-rede selecionados permanecem na lista suspensa. Adicione um e apenas um endereço de sub-rede por sub-rede ao ouvinte, caso contrário, haverá falha na criação do ouvinte.  
  
 **Endereços**  
 Use esse campo para inserir um endereço IP estático para o endereço de sub-rede selecionado. Entre em contato com o administrador de rede para obter esse endereço IP. Insira um endereço válido para o endereço de sub-rede selecionado, caso contrário, haverá falha na criação.  
  
 **Endereço IPv4**  
 Se você tiver selecionado o endereço de sub-rede IPv4 de uma sub-rede, insira um endereço IPv4 estático válido aqui.  
  
 **Máscara de Sub-rede**  
 Para um endereço IPv4, este campo somente leitura exibe a máscara de sub-rede da sub-rede selecionada.  
  
 **Endereço IPv6**  
 Se você tiver selecionado o endereço de sub-rede IPv6 de uma sub-rede, insira um endereço IPv6 estático válido aqui.  
  
 **OK**  
 Clique para criar e adicionar a sub-rede cujo endereço selecionado, junto com o endereço IP estático que você especificou. Uma linha contendo esses valores será adicionada à grade de sub-redes da caixa de diálogo **Novo Ouvinte de Grupo de Disponibilidade** ou **Especificar Réplicas** .  
  
> [!IMPORTANT]  
>  A caixa de diálogo **Adicionar Endereço IP** não verifica o endereço IP. Além disso, a caixa de diálogo não impede que você adicione o segundo endereço de sub-rede para uma sub-rede que você já adicionou ao ouvinte de grupo de disponibilidade.  
  
 **Cancelar**  
 Clique para cancelar suas seleções e retornar à caixa de diálogo **Novo Ouvinte do Grupo de disponibilidade** ou à guia **Ouvinte** sem adicionar um endereço IP estático a nenhuma sub-rede.  
  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Conectividade de cliente AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md)  
  
  
