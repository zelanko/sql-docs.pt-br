---
title: Log do aplicativo do Windows | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Windows application logs [Reporting Services]
- logs [Reporting Services], Windows application logs
- application logs [Reporting Services]
ms.assetid: 742fd00e-aa6c-4c8a-b58f-c03c489b1699
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f3d51afd8a27786be3c66bfdf935ad8b2e328d36
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580931"
---
# <a name="windows-application-log"></a>Log de aplicativo do Windows
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] grava mensagens de evento no log do aplicativo do Windows. Você pode usar as informações das mensagens gravadas no log de aplicativo para obter mais detalhes sobre os eventos gerados pelos aplicativos do servidor de relatório em execução no sistema local.  
  
## <a name="viewing-report-server-events"></a>Exibindo eventos do servidor de relatório  
 Use o recurso Visualizador de Eventos para exibir o arquivo de log e para filtrar as mensagens contidas nele. Para obter mais informações sobre mensagens de evento, consulte [Referência de erros e eventos &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md). Para obter mais informações sobre o log de aplicativo do Windows ou o Visualizador de Eventos, consulte a documentação do produto Windows.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece três fontes de evento:  
  
-   Servidor de relatório (serviço Servidor de Relatório do Windows)  
  
-   Gerenciador de Relatórios  
  
-   Processador de agendamento e entrega  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não permite desativar o registro de eventos do aplicativo para um servidor de relatório, nem controlar os eventos que são registrados. O esquema que descreve o registro de eventos de servidor de relatório é fixo. Você não pode estender o esquema para oferecer suporte a eventos personalizados.  
  
 A tabela a seguir descreve os tipos de evento que o servidor de relatório grava no log de eventos do aplicativo.  
  
|Tipo de evento|DESCRIÇÃO|  
|----------------|-----------------|  
|Informações|Um evento que descreve uma operação bem-sucedida (por exemplo, quando o serviço Servidor de Relatório é iniciado).|  
|Aviso|Um evento que indica um possível problema (por exemplo, pouco espaço em disco).|  
|Erro|Um evento que descreve um problema significativo (por exemplo, o serviço não iniciou).|  
|Auditoria Bem-sucedida|Um evento de segurança que descreve um logon bem-sucedido.|  
|Auditoria com Falha|Um evento que é registrado quando uma tentativa de logon falha.|  
  
## <a name="see-also"></a>Consulte Também  
 [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Referência de erros e eventos &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
