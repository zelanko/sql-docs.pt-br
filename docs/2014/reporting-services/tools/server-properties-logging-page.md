---
title: Propriedades do servidor (página Registrar em log) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a04c27fd790a1ad5c4ba453b43af5983a6440e3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099525"
---
# <a name="server-properties-logging-page"></a>Propriedades do Servidor (página Log)
  Use essa página para definir limites nos dados de execução de relatório que são coletados por um servidor de relatório. Dados de execução são armazenados internamente no banco de dados do servidor de relatório. Você pode controlar atividade de relatório para servidor de relatório que executa em modo nativo ou em modo integrado de SharePoint. Se o servidor de relatório for parte de uma implantação em expansão, o log de execução do relatório manterá um registro de todas as atividades do relatório para toda a implantação, em um único arquivo de log.  
  
 Para abrir essa página, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a um servidor de relatório, clique com o botão direito do mouse no nome do servidor de relatório e selecione **Propriedades**. Clique em **Log** para abrir esta página.  
  
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
  
  
