---
title: Log do aplicativo do Windows | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows application logs [Reporting Services]
- logs [Reporting Services], Windows application logs
- application logs [Reporting Services]
ms.assetid: 742fd00e-aa6c-4c8a-b58f-c03c489b1699
caps.latest.revision: 31
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c8fab15175eddb015bac7bd96d97bceba1fbd076
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007897"
---
# <a name="windows-application-log"></a>Log de aplicativo do Windows
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] grava mensagens de evento no log do aplicativo do Windows. Você pode usar as informações das mensagens gravadas no log de aplicativo para obter mais detalhes sobre os eventos gerados pelos aplicativos do servidor de relatório em execução no sistema local.  
  
## <a name="viewing-report-server-events"></a>Exibindo eventos do servidor de relatório  
 Use o recurso Visualizador de Eventos para exibir o arquivo de log e para filtrar as mensagens contidas nele. Para obter mais informações sobre mensagens de evento, consulte [referência de erros e eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md). Para obter mais informações sobre o log de aplicativo do Windows ou o Visualizador de Eventos, consulte a documentação do produto Windows.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece três fontes de evento:  
  
-   Servidor de relatório (serviço Servidor de Relatório do Windows)  
  
-   Gerenciador de Relatórios  
  
-   Processador de agendamento e entrega  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não permite desativar o registro de eventos do aplicativo para um servidor de relatório, nem controlar os eventos que são registrados. O esquema que descreve o registro de eventos de servidor de relatório é fixo. Você não pode estender o esquema para oferecer suporte a eventos personalizados.  
  
 A tabela a seguir descreve os tipos de evento que o servidor de relatório grava no log de eventos do aplicativo.  
  
|Tipo de evento|Description|  
|----------------|-----------------|  
|Informações|Um evento que descreve uma operação bem-sucedida (por exemplo, quando o serviço Servidor de Relatório é iniciado).|  
|Aviso|Um evento que indica um possível problema (por exemplo, pouco espaço em disco).|  
|Erro|Um evento que descreve um problema significativo (por exemplo, o serviço não iniciou).|  
|Auditoria Bem-sucedida|Um evento de segurança que descreve um logon bem-sucedido.|  
|Auditoria com Falha|Um evento que é registrado quando uma tentativa de logon falha.|  
  
## <a name="see-also"></a>Consulte também  
 [Fontes e arquivos de log do Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Referência de erros e eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  