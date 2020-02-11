---
title: Exibir histórico de atualização de dados (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- data refresh history [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 4c8d8aa8-794d-4f72-ace3-78d0e688e1a5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3efe11a733408124490ece2e85c9bd40db34f3fb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070914"
---
# <a name="view-data-refresh-history-powerpivot-for-sharepoint"></a>Exibir histórico de atualização de dados (PowerPivot para SharePoint)
  O histórico de atualização de dados é um registro de todas as atividades de atualização de dados PowerPivot em uma pasta de trabalho do Excel. As operações da atualização de dados são executadas em uma instância de servidor do Analysis Services em um farm do SharePoint em uma agenda fornecida por você. Por padrão, o histórico de atualização de dados é mantido durante um ano. No entanto, um administrador de farm pode especificar uma política de retenção diferente para o histórico de uso e de eventos que determine por quanto tempo os registros de atualização de dados são mantidos.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **Neste tópico:**  
  
 [Pré-requisitos](#prereq)  
  
 [Exibir o histórico de atualização de dados de uma pasta de trabalho individual](#viewhistory)  
  
 [Exibir o histórico de atualização de dados para todas as pastas de trabalho](#viewITOps)  
  
 [Usar informações de histórico](#pageelements)  
  
##  <a name="prereq"></a> Pré-requisitos  
 Você precisa ter permissões de Colaboração ou superiores para exibir o histórico de atualização de dados.  
  
 Você deve ter habilitado e agendado a atualização de dados em uma pasta de trabalho que contém dados PowerPivot. Se não tiver agendado a atualização de dados, você verá a página de definição da agenda em vez das informações do histórico.  
  
##  <a name="viewhistory"></a>Exibir o histórico de atualização de dados de uma pasta de trabalho individual  
  
1.  Em um site do SharePoint, abra a biblioteca contendo uma pasta de trabalho do Excel que contém dados PowerPivot.  
  
     Não há indicador visual que identifique quais pastas de trabalho em uma biblioteca do SharePoint contêm dados PowerPivot. Você deve saber com antecedência qual pasta de trabalho contém dados atualizáveis do PowerPivot.  
  
2.  Selecione a pasta de trabalho e clique na seta para baixo exibida à direita.  
  
3.  Selecione **Gerenciar Atualização de Dados PowerPivot**.  
  
 A página de histórico é exibida mostrando um registro completo de todas as atividades de atualização de dados PowerPivot na pasta de trabalho atual do Excel.  
  
##  <a name="viewITOps"></a>Exibir o histórico de atualização de dados para todas as pastas de trabalho  
 Usando o Painel de Gerenciamento PowerPivot na Administração Central, os administradores de farm e de aplicativos de serviço podem obter uma exibição abrangente do histórico e do status da atualização de todas as pastas de trabalho PowerPivot. Para obter mais informações, consulte [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="pageelements"></a>Usar informações de histórico  
 A página de histórico da atualização de dados fornece informações detalhadas sobre cada operação de atualização. Você pode usar as informações dessa página para confirmar se a atualização ocorreu ou por que falhou.  
  
|Item|DESCRIÇÃO|  
|----------|-----------------|  
|Nome|Especifica o nome do arquivo da pasta de trabalho do Excel que contém dados PowerPivot.|  
|Status atual|Os valores incluem **Agendado**, **Atualizando**, **Êxito**ou **Falha**.<br /><br /> **Agendado** aparece quando você cria o agendamento pela primeira vez. Depois que a atualização de dados ocorre pela primeira vez, essa mensagem de status não é mais exibida.<br /><br /> A **atualização** indica que a atualização de dados está em andamento. Uma solicitação está na fila de processamento ou está sendo executada ativamente no servidor.<br /><br /> Com **êxito** indica que a última operação de atualização de dados foi concluída e a pasta de trabalho atualizada é verificada novamente na biblioteca do SharePoint.<br /><br /> **Falha** indica que a última operação de atualização de dados não teve êxito. Os dados atualizados não foram salvos. A pasta de trabalho contém os mesmos dados que tinha antes do início da atualização de dados.|  
|Última atualização bem-sucedida|Especifica a data na qual a última atualização de dados foi concluída com êxito.|  
|Próxima atualização agendada|Especifica a data na qual a próxima atualização de dados está agendada.<br /><br /> O link **Configurar agendamento** leva à página de definição da agenda. Se você tiver permissões de colaboração na pasta de trabalho, poderá clicar no link para exibir e modificar as informações de agenda que controlam a atualização de dados PowerPivot na pasta de trabalho.|  
|Iniciado|Dentro da seção de detalhes do histórico, **Iniciado** indica a hora de processamento real. A hora de processamento real pode ser diferente da que foi agendada. O processamento será iniciado quando houver memória suficiente disponível no servidor. Se o servidor estiver muito ocupado, o processamento talvez seja iniciado várias horas depois da hora de início especificada.|  
|Concluído|Na seção de detalhes do histórico, **Concluído** indica quando a operação de atualização de dados foi concluída. A data e a hora indicam quando a pasta de trabalho for verificada na biblioteca.<br /><br /> Se houve falha na atualização de dados, uma ou mais mensagens de erro explicam a causa da falha. Você pode expandir cada registro para exibir o status detalhado. Cada fonte de dados é listada individualmente, junto com as mensagens de êxito ou de falha que explicam por que a atualização de dados não foi concluída.|  
|Hora|Fornece o tempo cumulativo entre o início e a conclusão da atualização de dados.|  
|Status|Fornece um registro histórico da falha ou do êxito de uma operação de atualização.|  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [Agendar uma atualização de dados &#40;PowerPivot para SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [Atualização de dados PowerPivot](power-pivot-data-refresh.md)  
  
  
