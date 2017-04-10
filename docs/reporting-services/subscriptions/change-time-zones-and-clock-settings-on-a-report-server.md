---
title: "Alterar configura&#231;&#245;es de fuso hor&#225;rio e rel&#243;gio em um servidor de relat&#243;rio | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "fusos horários [Reporting Services]"
  - "relógios [Reporting Services]"
  - "agendas [Reporting Services], configurações do relógio"
  - "agendas [Reporting Services], fusos horários"
ms.assetid: 69a19468-baa1-40f6-b158-8afdab0f8968
caps.latest.revision: 22
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 22
---
# Alterar configura&#231;&#245;es de fuso hor&#225;rio e rel&#243;gio em um servidor de relat&#243;rio
  Um servidor de relatório sempre usa a hora local do computador no qual é instalado. Você não pode configurá-lo para usar um fuso horário diferente. Se um aplicativo cliente apontar para um servidor de relatório em um fuso horário diferente, o fuso horário do servidor de relatório será usado para executar uma operação agendada. No Gerenciador de Relatórios e nas páginas de gerenciamento do SharePoint, o fuso horário é indicado em cada página de agendamento para que você saiba exatamente quando uma operação agendada ocorrerá. Por exemplo, a página para criar agendas personalizadas informará "O horário será expresso em (UTC-08:00) hora do Pacífico (EUA e Canadá)".  
  
## Alterando o fuso horário (modo nativo)  
 Se o fuso horário for alterado em um computador que hospeda um servidor de relatório, reinicie o serviço Servidor de Relatório para validar a alteração.  
  
 Os valores de carimbo de data e hora de instantâneos existentes do histórico de relatórios são sincronizados com a nova configuração de fuso horário. Se um instantâneo do histórico de relatório for gerado às 9h00 e, em seguida, o fuso horário seguinte, o carimbo de data e hora no instantâneo gerado será alterado de 9h00 para 10h00.  
  
 As agendas retêm as configurações existentes, exceto as mapeadas para o novo fuso horário. Por exemplo, se uma agenda for executada às 2h00 no horário padrão do Pacífico e o fuso horário for alterado para o horário padrão do leste australiano, a agenda será executada às 2h00 do horário padrão do leste australiano.  
  
 Os valores de propriedade de carimbo de data e hora (por exemplo, o horário em que uma pasta ou item de relatório vinculado é criado) não são sincronizados com uma nova configuração de fuso horário. Se você criar um item em 25 de junho às 9h00 e, em seguida, redefinir o fuso horário ou o horário, o carimbo de data e hora permanecerá como 25 de junho às 9h00.  
  
## Alterando o fuso horário (modo do SharePoint)  
 A configuração de fuso horário para o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é gerenciada como parte das configurações regionais do SharePoint. Para obter mais informações, consulte [Configurações regionais (SharePoint Server 2010 (http://technet.microsoft.com/library/cc824907.aspx)](http://technet.microsoft.com/library/cc824907.aspx).  
  
## Alterando as configurações de horário  
 A alteração do horário do computador não afeta os valores de carimbo de data e hora existentes (por exemplo, se você adiantar uma hora, os carimbos de data e hora dos instantâneos do histórico de relatórios não serão alterados). Pode haver um atraso de 10 segundos antes do Processador de Agendamento e Entrega usar a nova configuração. O atraso real pode variar se as configurações de intervalo de sondagem forem modificadas nos arquivos de configuração.  
  
## Consulte também  
 [Iniciar e parar o serviço Servidor de Relatório](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [Agendas](../../reporting-services/subscriptions/schedules.md)  
  
  