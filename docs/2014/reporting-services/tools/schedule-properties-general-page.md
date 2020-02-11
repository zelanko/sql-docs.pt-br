---
title: Propriedades de agendamento (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.scheduleproperties.general.f1
ms.assetid: 20e43966-6caf-4972-a2e2-0d9131ac8f51
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 98d013126fe1db1b8101d5ae451f658546f6d1f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66099736"
---
# <a name="schedule-properties-general-page"></a>Propriedades da Agenda (página Geral)
  Use essa página para exibir ou modificar uma agenda compartilhada. As agendas compartilhadas podem ser usadas no lugar de agendas específicas de relatório ou de assinaturas. Alterações à agenda são aplicadas depois que você salva a agenda. A edição de uma agenda não tem nenhum efeito em trabalhos atualmente em andamento. Se você editar uma agenda enquanto ela estiver sendo usada, todos os relatórios e assinaturas atualmente em processamento disparados daquela agenda terão permissão para serem concluídos.  
  
 Nem todas as combinações de frequência têm suporte em uma única agenda. Por exemplo, se você desejar executar um relatório às 12h00 e às 16h00 todas as sextas-feiras, você deverá criar duas agendas diárias que especifiquem uma data de execução na sexta-feira, uma com horário de início às 12h00 e outra com horário de início às 16h00.  
  
 O processamento da agenda se baseia no horário local do servidor de relatório que hospeda e processa a agenda.  
  
 Para abrir essa página, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte a um servidor de relatório, abra a pasta **Agendas Compartilhadas** clique com o botão direito do mouse em uma agenda compartilhada e selecione **Propriedades**.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e essa página não aparece quando você está executando uma edição que não tem esse recurso. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (.https://go.microsoft.com/fwlink/?linkid=232473)  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifica o nome para a agenda compartilhada.  
  
 **Iniciar a execução desta agenda em**  
 Especifica uma data de início para essa agenda.  
  
 **Parar esta agenda em**  
 Especifica uma data de validade para essa agenda.  
  
 **Tipo**  
 Especifica se o padrão de recorrência é baseado principalmente em horas, dias, semanas, meses ou só é executado uma vez.  
  
 **Hora (Padrão de Recorrência)**  
 Especifica opções para execução de uma operação agendada em intervalos de uma hora (por exemplo, para executar um relatório a cada 6 horas). Você pode especificar o intervalo em horas e minutos.  
  
 **Dia (Padrão de Recorrência)**  
 Especifica opções para execução de uma operação agendada em intervalos de dias (por exemplo, para executar um relatório a cada 2 dias). Você pode especificar o intervalo em dias e na hora e minutos que desejar que a agenda seja executada.  
  
 **Semana (Padrão de Recorrência)**  
 Especifica opções para execução de uma operação agendada em intervalos de uma semana ou quando o padrão que você quer repetir é baseado em semanas (por exemplo, para executar um relatório a cada 2 semanas). Você pode especificar uma agenda semanal para o dia, hora e minuto que você quer a agenda seja executada.  
  
 **Mês (Padrão de Recorrência)**  
 Especifica opções para execução de uma operação agendada em intervalos de um mês ou quando o padrão que você quer repetir é baseado em meses. Você pode especificar uma agenda mensal para o dia, hora e minuto que você quer a agenda seja executada. Você pode omitir meses específicos da agenda.  
  
 **Uma vez**  
 Especifica uma agenda que só é executada uma vez, em uma data e hora específica.  
  
## <a name="see-also"></a>Consulte Também  
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Conectar-se a um servidor de relatório no Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Criar, modificar e excluir agendas](../subscriptions/create-modify-and-delete-schedules.md)   
 [Agendas](../subscriptions/schedules.md)  
  
  
