---
title: Notas sobre a versão para os controles do Visualizador de Relatórios do SSRS
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maghan
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: 1528358c8aff5d6e99869f0f4f8c1676ee2d5e75
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730910"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>Notas de versão para os controles de Visualizador de relatórios para WebForms e WinForms do SSRS

Essas são as notas de versão para os controles de Visualizador de relatórios de WebForms e WinForms, relacionados ao [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS).

Para obter as notas de versão para o SSRS, consulte [notas de versão para o SQL Server Reporting Services (SSRS) 2017 e posterior](../release-notes-reporting-services.md).

## <a name="15013580"></a>150.1358.0
| Alterar descrição | Detalhes |
| :----------------- | :------ |
| Correções de bugs | Reverter uma alteração que removido Microsoft.ReportViewer.Design assemblies de referências do projeto. |
|           | Como parte de outras alterações, os dois assemblies foram alterados de versão 15.0 a 15.3. Isso foi revertido. |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| Alterar descrição | Detalhes |
| :----------------- | :------ |
| Correções de bugs  | Visualização de impressão apropriada para o monitor de DPI alto |
|            | Caixa de diálogo Imprimir mostraria fora do espaço visível |
|            | Grande número de parâmetros resultou em barras de rolagem de parâmetro e listas suspensas não está funcionando corretamente |
|            | Corrigido o problema com os parâmetros de tempo de Null e data |
|            | JQuery atualizado para a versão 3.3.1 |
|            | Corrigido sobrepor células tablix em renderização HTML |
|            | Removido o projeto referencia para eliminar os assemblies incorretos do VS que está sendo adicionados aos projetos de tempo de design |
|            | Correção de acessibilidade para a barra de ferramentas narrar somente para itens do Active Directory |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| Alterar descrição | Detalhes |
| :----------------- | :------ |
| Correção de um bug que impedia que relatórios sem parâmetros fossem carregados por meio de **Server.LoadReportDefinition**. | &nbsp; |
| O controle WebForms do Visualizador de Relatórios. | Dá suporte à inserção em páginas RTL (páginas que alteram o fluxo de texto usando a propriedade *direction: rtl;* ).<br/><br/>Dá suporte à personalização do texto da caixa de diálogo de impressão por meio da interface de localização *IReportViewerMessages5*.<br/><br/>Suporte a acessibilidade aprimorado.<br/><br/>&bull; &nbsp; &nbsp; [Pacote do NuGet para o controle do Visualizador de relatórios de WebForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| O controle WinForms do Visualizador de Relatórios. | Correção para impressão quando um aplicativo está em execução em um modo de alto DPI.<br/><br/>&bull; &nbsp; &nbsp; [Pacote do NuGet para o controle do Visualizador de relatórios do WinForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>Próximas etapas

[Introdução](integrating-reporting-services-using-reportviewer-controls-get-started.md) aos controles do Visualizador de Relatórios.

Ainda tem dúvidas? [Experimente o fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
