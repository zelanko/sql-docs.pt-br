---
title: Notas sobre a versão dos controles do Visualizador de Relatórios
description: As notas sobre a versão dos controles WebForms e WinForms do Visualizador de Relatórios, relacionados ao Reporting Services.
ms.date: 01/16/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: 5ee9bd80519e9dc9d75bb78a98b548b2a60ef247
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "76259374"
---
# <a name="release-notes-for-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>Notas sobre a versão dos controles WebForms e WinForms do Visualizador de Relatórios do SSRS

Estas são as notas sobre a versão dos controles WebForms e WinForms do Visualizador de Relatórios, relacionados ao SSRS ([!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]).

Para obter as notas sobre a versão do SSRS, confira [Notas sobre a versão do SSRS (SQL Server Reporting Services) 2017 e posterior](../release-notes-reporting-services.md).

## <a name="15014000"></a>150.1400.0
| Descrição da alteração | Detalhes |
| :----------------- | :------ |
| Correções de bugs | Correção de um problema em que o controle do visualizador não era carregado no modo de design. |
| &nbsp; | &nbsp; |

## <a name="15013580"></a>150.1358.0
| Descrição da alteração | Detalhes |
| :----------------- | :------ |
| Correções de bugs | Reversão de uma alteração que removeu os assemblies Microsoft.ReportViewer.Design das referências do projeto. |
|           | Como parte de outras alterações, dois assemblies foram alterados da versão 15.0 para 15.3. Isso foi revertido. |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| Descrição da alteração | Detalhes |
| :----------------- | :------ |
| Correções de bug  | Visualização de impressão correta do monitor de alto DPI |
|            | A caixa de diálogo Imprimir era exibida fora do espaço visível |
|            | Um grande número de parâmetros resultava em barras de rolagem de parâmetros e as listas suspensas não funcionavam corretamente |
|            | Correção de um problema com os parâmetros nulos e de data e hora |
|            | Atualização do JQuery para a versão 3.3.1 |
|            | Correção de sobreposição com células Tablix na renderização HTML |
|            | Remoção das referências do projeto em tempo de design para eliminar assemblies incorretos do VS adicionados aos projetos |
|            | Correção de acessibilidade da barra de ferramentas para narrar somente os itens ativos |
| &nbsp; | &nbsp; |

## <a name="150900148"></a>150.900.148

| Descrição da alteração | Detalhes |
| :----------------- | :------ |
| Correção de um bug que impedia que relatórios sem parâmetros fossem carregados por meio de **Server.LoadReportDefinition**. | &nbsp; |
| O controle WebForms do Visualizador de Relatórios. | Dá suporte à inserção em páginas RTL (páginas que alteram o fluxo de texto usando a propriedade *direction: rtl;* ).<br/><br/>Dá suporte à personalização do texto da caixa de diálogo de impressão por meio da interface de localização *IReportViewerMessages5*.<br/><br/>Suporte a acessibilidade aprimorado.<br/><br/>&bull; &nbsp; &nbsp; [Pacote NuGet do controle WebForms do Visualizador de Relatórios](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| O controle WinForms do Visualizador de Relatórios. | Correção para impressão quando um aplicativo está em execução em um modo de alto DPI.<br/><br/>&bull; &nbsp; &nbsp; [Pacote NuGet do controle WinForms do Visualizador de Relatórios](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>Próximas etapas

[Introdução](integrating-reporting-services-using-reportviewer-controls-get-started.md) aos controles do Visualizador de Relatórios.

Mais perguntas? [Experimente o fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
