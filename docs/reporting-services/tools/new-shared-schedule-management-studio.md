---
title: Novo agendamento compartilhado (Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.newschedule.f1
ms.assetid: b2c69586-d98e-4933-827d-f5e6c15c5203
caps.latest.revision: "32"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f0c57efec1f1e0c06f516cef9d53bae19272d568
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="new-shared-schedule-management-studio"></a>Nova Agenda Compartilhada (Management Studio)
  Use essa página para criar uma agenda compartilhada para executar relatórios publicados e assinaturas. As agendas compartilhadas podem ser usadas no lugar de agendas específicas de relatório ou de assinaturas. Informações de agenda centralizadas e a capacidade de pausar e retomar operações de agendamento são dois recursos básicos que distinguem as agendas compartilhadas de agendas específicas de item.  
  
 Nem todas as combinações de frequência têm suporte em uma única agenda. Por exemplo, se você desejar executar um relatório às 12h00 e às 16h00 todas as sextas-feiras, você deverá criar duas agendas diárias que especifiquem uma data de execução na sexta-feira, uma com horário de início às 12h00 e outra com horário de início às 16h00.  
  
 O processamento da agenda se baseia no horário local do servidor de relatório que hospeda e processa a agenda.  
  
 Para abrir essa página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte a um servidor de relatório, clique com o botão direito do mouse em **Agenda Compartilhada**e selecione **Nova Agenda**. Para salvar a agenda, o serviço SQL Server Agent deve estar em execução.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte pelas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte pelas edições do SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite um nome para a agenda compartilhada. Esse nome aparece em listas suspensas quando os usuários selecionam uma agenda compartilhada para relatórios e assinaturas. Certifique-se de fornecer um nome descritivo que caiba facilmente dentro de uma lista e que diferencie com facilidade uma agenda compartilhada de outra. Um nome deve conter pelo menos um caractere alfanumérico. Também pode conter espaços e alguns símbolos. Não use os seguintes caracteres ao especificar um nome:  
  
 ; ? : @ & = + , $ / * < >  
  
 " /  
  
 **Iniciar a execução desta agenda em**  
 Especifique uma data de início para essa agenda.  
  
 **Parar esta agenda em**  
 Especifique uma data de validade para essa agenda.  
  
 **Tipo**  
 Especifica se o padrão de recorrência é baseado principalmente em horas, dias, semanas ou meses.  
  
 **Hora (Padrão de Recorrência)**  
 Selecione opções para execução de uma operação agendada em intervalos de uma hora (por exemplo, para executar um relatório a cada 6 horas). Você pode especificar o intervalo em horas e minutos.  
  
 **Dia (Padrão de Recorrência)**  
 Selecione opções para execução de uma operação agendada em intervalos de dias (por exemplo, para executar um relatório a cada 2 dias). Você pode especificar o intervalo em dias e na hora e minutos que desejar que a agenda seja executada.  
  
 **Semana (Padrão de Recorrência)**  
 Selecione opções para execução de uma operação agendada em intervalos de uma semana ou quando o padrão que você quer repetir é baseado em semanas (por exemplo, para executar um relatório a cada 2 semanas). Você pode especificar uma agenda semanal para o dia, hora e minuto que você quer a agenda seja executada.  
  
 **Mês (Padrão de Recorrência)**  
 Selecione opções para execução de uma operação agendada em intervalos de um mês ou quando o padrão que você quer repetir é baseado em meses. Você pode especificar uma agenda mensal para o dia, hora e minuto que você quer a agenda seja executada. Você pode omitir meses específicos da agenda.  
  
 **Uma vez**  
 Selecione esta opção para criar uma agenda que só executa uma vez, em uma data e hora específica.  
  
## <a name="see-also"></a>Consulte também  
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Criar, modificar e excluir agendas](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [Agendas](../../reporting-services/subscriptions/schedules.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
