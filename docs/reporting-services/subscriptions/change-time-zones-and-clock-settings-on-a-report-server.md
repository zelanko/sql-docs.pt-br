---
title: Alterar as configurações de fuso horário e relógio em um servidor de relatório | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- time zones [Reporting Services]
- clocks [Reporting Services]
- schedules [Reporting Services], clock settings
- schedules [Reporting Services], time zones
ms.assetid: 69a19468-baa1-40f6-b158-8afdab0f8968
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5c1e3a2b4fe468f3565dbf7ad47295ab8836315b
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65578362"
---
# <a name="change-time-zones-and-clock-settings-on-a-report-server"></a>Alterar configurações de fuso horário e relógio em um servidor de relatório
  Um servidor de relatório sempre usa a hora local do computador no qual é instalado. Você não pode configurá-lo para usar um fuso horário diferente. Se um aplicativo cliente apontar para um servidor de relatório em um fuso horário diferente, o fuso horário do servidor de relatório será usado para executar uma operação agendada. No Gerenciador de Relatórios e nas páginas de gerenciamento do SharePoint, o fuso horário é indicado em cada página de agendamento para que você saiba exatamente quando uma operação agendada ocorrerá. Por exemplo, a página para criar agendas personalizadas informará "O horário será expresso em (UTC-08:00) hora do Pacífico (EUA e Canadá)".
O servidor de relatório cria um trabalho do SQL Server Agent usado para disparar a agenda. Quando o Servidor de Relatório e o SQL Server Agent estão localizados em servidores separados, o fuso horário deve ser o mesmo em todos os servidores.
  
## <a name="changing-the-time-zone-native-mode"></a>Alterando o fuso horário (modo nativo)  
 Se o fuso horário for alterado em um computador que hospeda um servidor de relatório, reinicie o serviço Servidor de Relatório para validar a alteração.  
  
 Os valores de carimbo de data e hora de instantâneos existentes do histórico de relatórios são sincronizados com a nova configuração de fuso horário. Se um instantâneo do histórico de relatório for gerado às 9h00 e, em seguida, o fuso horário seguinte, o carimbo de data e hora no instantâneo gerado será alterado de 9h00 para 10h00.  
  
 As agendas retêm as configurações existentes, exceto as mapeadas para o novo fuso horário. Por exemplo, se uma agenda for executada às 2h00 no horário padrão do Pacífico e o fuso horário for alterado para o horário padrão do leste australiano, a agenda será executada às 2h00 do horário padrão do leste australiano.  
  
 Os valores de propriedade de carimbo de data e hora (por exemplo, o horário em que uma pasta ou item de relatório vinculado é criado) não são sincronizados com uma nova configuração de fuso horário. Se você criar um item em 25 de junho às 9h00 e, em seguida, redefinir o fuso horário ou o horário, o carimbo de data e hora permanecerá como 25 de junho às 9h00.  
  
## <a name="changing-the-time-zone-sharepoint-mode"></a>Alterando o fuso horário (modo do SharePoint)  
 A configuração de fuso horário para o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é gerenciada como parte das configurações regionais do SharePoint. Para saber mais, veja [Configurações regionais (SharePoint Server 2010 (https://technet.microsoft.com/library/cc824907.aspx)](https://technet.microsoft.com/library/cc824907.aspx).  
  
## <a name="changing-the-clock-settings"></a>Alterando as configurações de horário  
 A alteração do horário do computador não afeta os valores de carimbo de data e hora existentes (por exemplo, se você adiantar uma hora, os carimbos de data e hora dos instantâneos do histórico de relatórios não serão alterados). Pode haver um atraso de 10 segundos antes do Processador de Agendamento e Entrega usar a nova configuração. O atraso real pode variar se as configurações de intervalo de sondagem forem modificadas nos arquivos de configuração.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar e parar o serviço Servidor de Relatório](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [Agendas](../../reporting-services/subscriptions/schedules.md)  
  
  
