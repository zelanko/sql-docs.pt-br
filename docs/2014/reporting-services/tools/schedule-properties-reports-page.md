---
title: Propriedades do Agendamento (página Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 999f0b922705e210e6761d7b534490387c8fef74
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363228"
---
# <a name="schedule-properties-reports-page"></a>Propriedades da Agenda (página Relatórios)
  Use essa página para exibir uma lista de todos os relatórios que usam agenda compartilhada. As agendas podem ser usadas para atualizar instantâneos de relatório, gerar histórico de relatório, engatilhar uma assinatura ou terminar uma cópia armazenada em cache do relatório. Para descobrir como a agenda é usada, exiba a propriedade e as informações de assinatura do relatório.  
  
 Embora essa página exiba cada relatório que usa a agenda compartilhada, ele não indica quantas vezes uma agenda compartilhada é usada naquele único relatório. Por exemplo, suponhamos que 20 assinantes diferentes do relatório Vendas da Empresa usem a mesma agenda compartilhada para engatilhar processamento de assinatura. Nesse caso, o relatório Vendas da Empresa só aparecerá uma vez nessa lista, embora o relatório tenha 20 referências à agenda compartilhada.  
  
 Para abrir essa página, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a um servidor de relatórios, abra a pasta **Agendas Compartilhadas** , clique com o botão direito do mouse em uma agenda compartilhada, selecione **Propriedades**e clique em **Relatórios**.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473).  
  
## <a name="options"></a>Opções  
 **Pasta**  
 Especifica o caminho do relatório.  
  
 **Relatório**  
 Especifica o nome do relatório que usa a agenda.  
  
## <a name="see-also"></a>Consulte também  
 [Criar, modificar e excluir agendas](../subscriptions/create-modify-and-delete-schedules.md)   
 [Agendas](../subscriptions/schedules.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Conectar-se a um servidor de relatório no Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Configurar propriedades gerais de um relatório &#40;Gerenciador de relatórios&#41;](../configure-general-properties-for-a-report-report-manager.md)  
  
  
