---
title: Verificando uma execução de relatório | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- auditing [Reporting Services]
- verifying report execution
- logs [Reporting Services], verifying report run
- report execution data [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services], verifying execution
- checking report execution
ms.assetid: 18a98f2f-6b40-454e-9b37-568ed1a96458
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 59ca005a30d479f8788fcdfdcf312df0dcf46c34
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43272458"
---
# <a name="verifying-a-report-run"></a>Verificando uma execução de relatório
  Para visualizar informações sobre o status de processamento do relatório, você pode usar os arquivos de log ou consultar as informações sobre status exibidas com o relatório no Gerenciador de Relatórios.  
  
## <a name="sources-of-report-execution-data"></a>Fontes de dados de execução de relatórios  
 Os logs de execução de relatório fornecem informações abrangentes sobre a execução do relatório, incluindo o nome dele, o nome do usuário que o executou, o horário da execução do relatório e a extensão de entrega usada para distribuí-lo. Para visualizar e analisar esses dados, você pode copiar o log de execução do relatório nas tabelas do banco de dados que são fáceis de consultar e relatar.  
  
 Os arquivos de log contêm muitas entradas sobre a execução de relatório e outra atividade de servidor. Uma vez que os arquivos de log contêm tantos dados, talvez você queira usar o Gerenciador de Relatórios apenas se quiser verificar quando foi a última execução do relatório. Se quiser informações adicionais, exiba os arquivos de log.  
  
> [!NOTE]  
>  O Gerenciador de Relatórios não mostra os horários de processamento dos relatórios executados sob demanda.  
  
 A tabela a seguir descreve como exibir a data e hora do processamento para vários tipos de relatórios.  
  
|Para este tipo de relatório|As informações sobre data e hora estão localizadas aqui|Para exibir as informações, faça o seguinte|  
|-----------------------------|-----------------------------------------------|-----------------------------------------------|  
|Um relatório que é executado como um instantâneo de relatório.|Na página Conteúdo. Para obter mais informações, consulte [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378).|1) Localize a pasta que contém o relatório.<br /><br /> 2) Defina a pasta na exibição Detalhes.<br /><br /> 3) Observe a data e hora na coluna **Quando Executado** .|  
|Um instantâneo no histórico de relatórios.|Na página Propriedades do Histórico. Para obter mais informações, consulte [Página de propriedades Opções de Instantâneo &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).|1) Abra o relatório.<br /><br /> 2) Clique na página **Propriedades** .<br /><br /> 3) Clique na guia **Histórico** .<br /><br /> 4) Observe a data e hora na coluna **Quando Executado** .|  
|Um relatório armazenado em cache.|Na agenda usada para criar e atualizar o relatório armazenado em cache.|1) Abra o relatório.<br /><br /> 2) Clique na página **Propriedades** .<br /><br /> 3) Clique na guia **Execução** .<br /><br /> 4) Abra a agenda.|  
  
## <a name="see-also"></a>Consulte Também  
 [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Definir propriedades de processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
