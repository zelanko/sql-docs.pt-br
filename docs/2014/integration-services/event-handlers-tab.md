---
title: Guia manipuladores de eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.eventhandlerwindow.f1
ms.assetid: 94fc8916-8032-490c-b9d5-ded8b6217e49
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 49b6145f29fac5088d44e6e82f6dcd3eb491556a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007968"
---
# <a name="event-handlers-tab"></a>Guia Manipuladores de Eventos
  Use a guia **Manipuladores de Eventos** do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] para criar um fluxo de controle em um pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Um manipulador de eventos é executado em resposta a um evento criado pelo pacote ou por uma tarefa ou contêiner no pacote.  
  
## <a name="options"></a>Opções  
 **Executável**  
 Selecione o executável para o qual deseja criar um manipulador de eventos. O executável pode ser o pacote ou uma tarefa ou contêineres no pacote.  
  
 **Manipulador de eventos**  
 Selecione um tipo de manipulador de eventos. Crie o manipulador de eventos, arrastando os itens da **Caixa de Ferramentas**.  
  
 **Delete (excluir)**  
 Selecione um manipulador de eventos e remova-o do pacote, clicando em **Excluir**.  
  
 **Clique aqui para criar um \<nome do manipulador de eventos > para o executável \<nome executável >**  
 Clique para criar o manipulador de eventos.  
  
 Crie o fluxo de controle arrastando os objetos gráficos que representam as tarefas e os contêiners [!INCLUDE[ssIS](../includes/ssis-md.md)] da **Caixa de Ferramentas** para a superfície de design da guia **Manipuladores de Eventos** e, em seguida, conectando os objetos usando as restrições de precedência para definir a sequência na qual eles serão executados.  
  
 Além disso, para adicionar anotações, clique com o botão direito do mouse na superfície de design e, em seguida, no menu, clique em **Adicionar Anotação**.  
  
## <a name="see-also"></a>Consulte também  
 [Manipuladores de eventos do SSIS &#40;Integration Services&#41;](integration-services-ssis-event-handlers.md)   
 [Fluxo de controle](control-flow/control-flow.md)   
 [Designer SSIS](ssis-designer.md)   
 [Serviços de integração &#40;SSIS&#41; manipuladores de eventos](integration-services-ssis-event-handlers.md)  
  
  