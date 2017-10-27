---
title: "Relatório de web part do visualizador em um site do SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a37ed5efe7c365c601deb95d9fe761d227e7021e
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>Relatório de web part do visualizador em um site do SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

A web part do Visualizador de relatórios é uma parte da web personalizado. Você pode usar a web part para exibir, navegar, imprimir e exportar relatórios em um servidor de relatório em um site do SharePoint. A web part do Visualizador de relatórios está associada a arquivos de definição (. RDL) de relatório que são processados por um servidor de relatório do Microsoft SQL Server Reporting Services. 

A web part do Visualizador de relatórios mais recente também pode relatórios paginado do serviço implantados em um servidor de relatório do Power BI. A web part não funciona com relatórios do Power BI.

## <a name="why-the-report-viewer-web-part-is-re-introduced"></a>Por que a web part do Visualizador de relatórios é lançada novamente

A web part do Visualizador de relatórios estava disponível como parte do suplemento Reporting Services para produtos do SharePoint. A web part foi específica para servidores de relatório no modo integrado do SharePoint. Modo integrado do SharePoint foi preterido após o SQL Server 2016.

Começando com o SQL Server 2017, há apenas um modo de instalação do Reporting Services: **modo nativo**. Você pode incorporar todos os tipos de relatórios usando um visualizador de páginas da web part usando a *rs: Inserir = true* parâmetro de URL. Inserir relatórios em páginas do SharePoint é uma história de integração solicitada por clientes e a web part do Visualizador de relatórios atualizada habilita este cenário para relatórios paginados.

Enquanto a web part do Visualizador de páginas é suficiente para inserir um relatório paginado em uma página do SharePoint, a web part do Visualizador de relatórios atualizada oferece recursos adicionais.

* Mostrar/ocultar botões da barra de ferramentas específica
* Substituir valores de parâmetro de relatório
* Conectar web parts de filtro para os parâmetros de relatório

## <a name="download-the-report-viewer-web-part-solution-package"></a>Baixe o pacote de solução do Visualizador de relatórios da web part

A web part do Visualizador de relatórios está disponível no Microsoft Download Center.

[Baixe o pacote de solução web part Visualizador de relatórios](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="considerations-and-limitations"></a>Considerações e limitações

Os itens listados são específicos para a web part do Visualizador de relatórios atualizada.

* A web part só pode ser usada em *clássico* páginas do SharePoint.
* Somente os relatórios paginados (RDL) têm suporte para inserção na web part do Visualizador de relatórios. Se você estiver procurando para inserir relatórios do Power BI ou relatórios móveis, você pode usar o *rs: Inserir = true* parâmetro de URL.

## <a name="next-steps"></a>Próximas etapas

Para começar a usar a web part do Visualizador de relatórios atualizada, consulte [implantar a web part do Visualizador de relatórios em um site do SharePoint](deploy-report-viewer-web-part.md).

