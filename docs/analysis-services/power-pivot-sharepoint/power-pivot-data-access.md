---
title: Power Pivot Data Access | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0485e78db0c1e338c5f6680cefc0fa87583505b5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="power-pivot-data-access"></a>Acesso a dados do Power Pivot
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Este tópico descreve os modos nos quais os dados são recuperados de uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] publicada em uma biblioteca do SharePoint.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são armazenados dentro de uma pasta de trabalho do Excel. A cadeia de conexão é uma URL para uma pasta de trabalho em um site do SharePoint.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são geralmente usados pela pasta de trabalho que os contém, como os dados por trás de Tabelas Dinâmicas e Gráficos Dinâmicos. Como alternativa, os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] também podem ser usados como uma fonte de dados externa, em que uma pasta de trabalho, painel ou relatório conecta-se a um arquivo do Excel separado (.xlsx) no SharePoint e recupera os dados para uso subsequente. As ferramentas de cliente que geralmente usam dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são o Excel, o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], outros relatórios do Reporting Services e o PerformancePoint.  
  
 Na área de trabalho, o suplemento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usa o AMO e ADOMD.NET para criar, processar e consultar os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no espaço de trabalho de cliente.  
  
 Em um farm do SharePoint, os Serviços do Excel usam o provedor local de OLE DB do MSOLAP para conectar-se a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . O provedor envia a solicitação de conexão para um servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no farm. Esse servidor carrega os dados, executa a consulta e retorna o conjunto de resultados.  
  
##  <a name="queryproc"></a> Consulta de dados do Power Pivot no SharePoint  
 Quando você exibe uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em uma biblioteca do SharePoint, os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que estão dentro da pasta de trabalho são detectados, extraídos e processados separadamente em instâncias de servidor do Analysis Services dentro do farm, e os Serviços do Excel renderizam a camada de apresentação. É possível exibir a pasta de trabalho totalmente processada em uma janela do navegador ou em um aplicativo da área de trabalho do Excel 2010 que tenha o suplemento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 O diagrama a seguir mostra como uma solicitação de processamento de consulta se move pelo farm. Como os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] fazem parte de uma pasta de trabalho do Excel 2010, uma solicitação de processamento de consulta ocorre quando um usuário abre uma pasta de trabalho do Excel em uma biblioteca do SharePoint e interage com uma Tabela Dinâmica ou um Gráfico Dinâmico que contém dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 ![GMNI_DataProcReq](../../analysis-services/power-pivot-sharepoint/media/gmni-dataprocreq.gif "GMNI_DataProcReq")  
  
 Os componentes dos Serviços do Excel e do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint processam partes diferentes do mesmo arquivo de pasta de trabalho (.xlsx). Os Serviços do Excel detectam os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e solicitam o processamento de um servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. O servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aloca a solicitação em uma instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] , que extrai e carrega os dados da pasta de trabalho na biblioteca de conteúdo. Os dados armazenados na memória são mesclados de volta na pasta de trabalho renderizada e devolvidos ao Excel Web Access para apresentação em uma janela de navegador.  
  
 Nem todos os dados de uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são tratados pelo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Os Serviços do Excel processam tabelas e dados de células de uma planilha. Apenas Tabelas Dinâmicas, Gráficos Dinâmicos e segmentações de dados que vão de encontro aos dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são tratados pelo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
## <a name="see-also"></a>Consulte também  
 [Conecte-se ao Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)   
 [Acesso de dados de modelo de tabela](../../analysis-services/tabular-models/tabular-model-data-access.md)  
  
  
