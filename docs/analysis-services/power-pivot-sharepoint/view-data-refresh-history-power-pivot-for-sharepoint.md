---
title: "Exibir histórico (PowerPivot para SharePoint) de atualização de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- data refresh history [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 4c8d8aa8-794d-4f72-ace3-78d0e688e1a5
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bad4593c84946a2957b6b433de359d4857f116ad
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="view-data-refresh-history-power-pivot-for-sharepoint"></a>Exibir o Histórico de Atualização de Dados (Power Pivot para SharePoint)
  O histórico de atualização de dados é um registro de toda a atividade de atualização de dados para os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em uma pasta de trabalho do Excel. As operações da atualização de dados são executadas em uma instância de servidor do Analysis Services em um farm do SharePoint em uma agenda fornecida por você. Por padrão, o histórico de atualização de dados é mantido durante um ano. No entanto, um administrador de farm pode especificar uma política de retenção diferente para o histórico de uso e de eventos que determine por quanto tempo os registros de atualização de dados são mantidos.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **Neste tópico:**  
  
 [Pré-requisitos](#prereq)  
  
 [Exibir o histórico da atualização de dados de uma pasta de trabalho individual](#viewhistory)  
  
 [Exibir o histórico da atualização de dados de todas as pastas de trabalho](#viewITOps)  
  
 [Usar informações do histórico](#pageelements)  
  
##  <a name="prereq"></a> Pré-requisitos  
 Você precisa ter permissões de Colaboração ou superiores para exibir o histórico de atualização de dados.  
  
 Você deve ter habilitado e agendado a atualização de dados em uma pasta de trabalho que contém os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se não tiver agendado a atualização de dados, você verá a página de definição da agenda em vez das informações do histórico.  
  
##  <a name="viewhistory"></a> Exibir o histórico da atualização de dados de uma pasta de trabalho individual  
  
1.  Em um site do SharePoint, abra a biblioteca que contém uma pasta de trabalho do Excel com os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
     Não há nenhum indicador visual que identifique quais pastas de trabalho em uma biblioteca do SharePoint contêm os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Você deve saber com antecedência qual pasta de trabalho contém os dados atualizáveis do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
2.  Selecione a pasta de trabalho e clique na seta para baixo exibida à direita.  
  
3.  Selecione **Gerenciar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Atualização de Dados**.  
  
 A página de histórico é exibida mostrando um registro completo de toda a atividade de atualização para os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] na pasta de trabalho atual do Excel.  
  
##  <a name="viewITOps"></a> Exibir o histórico da atualização de dados de todas as pastas de trabalho  
 Usando o Painel de Gerenciamento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] na Administração Central, os administradores de farm e os administradores de aplicativo do serviço podem ter uma visão abrangente do status e do histórico de atualização dos dados para todas as pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obter mais informações, consulte [Power Pivot Management Dashboard and Usage Data](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="pageelements"></a> Usar informações do histórico  
 A página de histórico da atualização de dados fornece informações detalhadas sobre cada operação de atualização. Você pode usar as informações dessa página para confirmar se a atualização ocorreu ou por que falhou.  
  
|Item|Description|  
|----------|-----------------|  
|Nome|Especifica o nome de arquivo da pasta de trabalho do Excel que contém os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|Status atual|Os valores incluem **Agendado**, **Atualizando**, **Êxito**ou **Falha**.<br /><br /> **Agendado** é exibido quando a agenda é criada pela primeira vez. Depois que a atualização de dados ocorre pela primeira vez, essa mensagem de status não é mais exibida.<br /><br /> **Atualizando** indica que a atualização de dados está em andamento. Uma solicitação está na fila de processamento ou está sendo executada ativamente no servidor.<br /><br /> **Êxito** indica que a última operação de atualização de dados foi concluída e a pasta de trabalho atualizada está verificada na biblioteca do SharePoint.<br /><br /> **Falha** indica que a última operação de atualização de dados não obteve êxito. Os dados atualizados não foram salvos. A pasta de trabalho contém os mesmos dados que tinha antes do início da atualização de dados.|  
|Última atualização bem-sucedida|Especifica a data na qual a última atualização de dados foi concluída com êxito.|  
|Próxima atualização agendada|Especifica a data na qual a próxima atualização de dados está agendada.<br /><br /> O link **Configurar agendamento** leva à página de definição da agenda. Se você tiver permissões de Colaboração na pasta de trabalho, poderá clicar no link para exibir e modificar as informações de agenda que controlam a atualização de dados autônoma para os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] na pasta de trabalho.|  
|Started (iniciado)|Dentro da seção de detalhes do histórico, **Iniciado** indica a hora de processamento real. A hora de processamento real pode ser diferente da que foi agendada. O processamento será iniciado quando houver memória suficiente disponível no servidor. Se o servidor estiver muito ocupado, o processamento talvez seja iniciado várias horas depois da hora de início especificada.|  
|Concluído|Na seção de detalhes do histórico, **Concluído** indica quando a operação de atualização de dados foi concluída. A data e a hora indicam quando a pasta de trabalho for verificada na biblioteca.<br /><br /> Se houve falha na atualização de dados, uma ou mais mensagens de erro explicam a causa da falha. Você pode expandir cada registro para exibir o status detalhado. Cada fonte de dados é listada individualmente, junto com as mensagens de êxito ou de falha que explicam por que a atualização de dados não foi concluída.|  
|Hora|Fornece o tempo cumulativo entre o início e a conclusão da atualização de dados.|  
|Status|Fornece um registro histórico da falha ou do êxito de uma operação de atualização.|  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [Agendar uma atualização de dados (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/8571208f-6aae-4058-83c6-9f916f5e2f9b)   
 [Atualização de Dados PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  

