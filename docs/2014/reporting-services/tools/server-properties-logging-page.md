---
title: Propriedades do servidor (página Registrar em log) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 29331f12c0eeb713f36999df239069e4e56c359e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082456"
---
# <a name="server-properties-logging-page"></a>Propriedades do Servidor (página Log)
  Use essa página para definir limites nos dados de execução de relatório que são coletados por um servidor de relatório. Dados de execução são armazenados internamente no banco de dados do servidor de relatório. Você pode controlar atividade de relatório para servidor de relatório que executa em modo nativo ou em modo integrado de SharePoint. Se o servidor de relatório for parte de uma implantação em expansão, o log de execução do relatório manterá um registro de todas as atividades do relatório para toda a implantação, em um único arquivo de log.  
  
 Para abrir essa página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], se conectar a um servidor de relatório, o nome do servidor de relatório com o botão direito e selecione **propriedades**. Clique em **Log** para abrir esta página.  
  
## <a name="options"></a>Opções  
 **Habilitar log de execução de relatório**  
 Clique para criar e armazenar informações sobre atividade de relatório no servidor. Se essa opção estiver habilitada, o servidor de relatório controlará quais relatórios serão usados, a frequência de processamento do relatório, o tipo de operação executado, o formato de saída e quem executou o relatório. Para obter mais informações sobre pontos de dados adicionais que são capturados no log, consulte [Log de execução do servidor de relatório e exibição do ExecutionLog3](../report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
 **Remova entradas de log mais antigas que este número de dias**  
 Especifique o número de dias depois dos quais as entradas de log serão apagadas do log de execução de relatório. O valor padrão é 60 dias.  
  
## <a name="see-also"></a>Consulte também  
 [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectar-se a um servidor de relatório no Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Fontes e arquivos de log do Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Log de execução do servidor de relatório e a exibição ExecutionLog3](../report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  
