---
title: Página de exibição, relatórios (Report Manager) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4874ba29-429b-4dd4-a8cb-d4f087237dc2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c8731c1d0f79d99919c4a087521565a6ec590278
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098735"
---
# <a name="view-page-reports-report-manager"></a>Página Exibir, Relatórios (Gerenciador de Relatórios)
  Use a página Exibir de relatórios para exibir um relatório. Quando você abre um relatório pela primeira vez no Gerenciador de Relatórios, ele é formatado em HTML. Relatórios HTML incluem uma barra de ferramentas de relatórios que aparece no topo do relatório para que você possa navegar pelas páginas do relatório, pesquisar no relatório ou exportá-lo para um formato diferente. O diagrama a seguir mostra a barra de ferramentas do relatório.  
  
 ![Barra de ferramentas do relatório](media/htmlviewer-toolbar.gif "Barra de ferramentas do relatório")  
Barra de ferramentas do relatório  
  
 No [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], os relatórios podem ser configurados para executar sob demanda ou de um instantâneo de execução de relatório. Se um relatório for executado sob demanda, todo o processamento dos dados e do relatório ocorrerá cada vez que você abrir o relatório. Se você exibir um relatório configurado para executar como um instantâneo de execução de relatório, o processamento dos dados terá ocorrido quando o instantâneo foi criado.  
  
## <a name="exporting-reports"></a>Exportando relatórios  
 Nem todos os recursos de relatório estão disponíveis em todos os formatos de exportação. Se você exportar um relatório HTML para outro formato, poderá esperar algumas diferenças na exibição do relatório. Além disso, se o relatório incluir recursos interativos (como hiperlinks, marcadores ou mapas de documentos), pode ser que esses recursos não estejam disponíveis ou não funcionem da mesma maneira no novo formato.  
  
## <a name="generating-data-feeds-from-report-data"></a>Gerando feeds de dados a partir dos dados do relatório  
 É possível gerar feeds de dados de relatórios. A extensão de renderização do Atom do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] gera dois documentos em conformidade com Atom: um documento de serviço Atom que lista os feeds de dados fornecidos pelo relatório e os feeds de dados que contêm os dados do relatório. Os feeds de dados são gerados pelo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em um formato em conformidade com o Atom 1.0, o qual é legível e pode ser trocado com aplicativos que consomem feeds de dados em conformidade com o Atom. Por exemplo, o cliente [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] pode consumir feeds de dados gerados a partir de relatórios.  
  
## <a name="running-parameterized-reports"></a>Executando relatórios com parâmetros  
 Um relatório que contém campos de entrada e um botão **Exibir Relatório** é um relatório com parâmetros. Para exibir um relatório com parâmetros, você pode precisar fornecer valores que são usados para executar o relatório.  
  
> [!NOTE]  
>  Instantâneos de execução de relatório e alguns formatos de exportação não estarão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [recursos com suporte nas edições do SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
