---
title: "Propriedades do Agendamento (página Relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 06/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
caps.latest.revision: "23"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 938b731ea379eb31a5cf1368087fdd2eda897385
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="schedule-properties-reports-page"></a>Propriedades da Agenda (página Relatórios)
  Use a página de propriedades de agenda do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] em [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] para exibir uma lista de todos os relatórios que usam a agenda compartilhada específica. As agendas podem ser usadas para atualizar instantâneos de relatório, gerar histórico de relatório, engatilhar uma assinatura ou terminar uma cópia armazenada em cache do relatório. Para descobrir como a agenda é usada, exiba a propriedade e as informações de assinatura do relatório.  
  
 Embora essa página exiba cada relatório que usa a agenda compartilhada, ele não indica quantas vezes uma agenda compartilhada é usada naquele único relatório. Por exemplo, suponhamos que 20 assinantes diferentes do relatório Vendas da Empresa usem a mesma agenda compartilhada para engatilhar processamento de assinatura. Nesse caso, o relatório Vendas da Empresa só aparecerá uma vez nessa lista, embora o relatório tenha 20 referências à agenda compartilhada.  
  
 Para abrir a página de propriedades de agenda:
 1. Inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2. Conecte-se a um servidor de relatório.
 3. Abra a pasta **Agendamentos Compartilhados** .
 4. Clique com o botão direito do mouse em um agendamento armazenado e selecione **Propriedades**.
 5. Clique em **Relatórios**.  
  
  Você também pode gerenciar agendas compartilhadas nas **Configurações de Site** do Portal da Web do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] .
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte na edição do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="options"></a>Opções  
 **Pasta**  
 Especifica o caminho do relatório.  
  
 **Relatório**  
 Especifica o nome do relatório que usa a agenda.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar, modificar e excluir agendas](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [Agendas](../../reporting-services/subscriptions/schedules.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Configurar as propriedades gerais de um relatório (Gerenciador de Relatórios)](http://msdn.microsoft.com/en-us/10b941b2-28e6-4408-9ee4-acebc63c8496)  
  
  

