---
title: Notas sobre a versão para os controles do Visualizador de Relatórios do SSRS
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: d6c7130e45e535ad1849bed5713313bf6f89020f
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923807"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>Notas de versão para os controles do Visualizador de relatórios para WebForms e WinForms do SSRS

Estas são as notas de versão para os controles do Visualizador de relatórios de WebForms e WinForms, relacionados a [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS).

Para ver as notas de versão do SSRS, consulte [notas de versão para SQL Server Reporting Services (SSRS) 2017 e posterior](../release-notes-reporting-services.md).

## <a name="15013580"></a>150.1358.0
| Alterar descrição | Detalhes |
| :----------------- | :------ |
| Correções de bugs | Reverteu uma alteração que removeu os assemblies Microsoft. ReportViewer. Design das referências do projeto. |
|           | Como parte de outras alterações, dois assemblies foram alterados da versão 15,0 para 15,3. Isso foi revertido. |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| Alterar descrição | Detalhes |
| :----------------- | :------ |
| Correções de bugs  | Visualização de impressão adequada para o monitor de alto DPI |
|            | A caixa de diálogo Imprimir apareceria fora do espaço visível |
|            | Um grande número de parâmetros resultou em barras de rolagem de parâmetro e as listas suspensas não estão funcionando corretamente |
|            | Corrigido o problema com parâmetros nulos e de data e hora |
|            | JQuery atualizado para a versão 3.3.1 |
|            | Correção de sobreposição com células Tablix na renderização HTML |
|            | Removidas as referências de projeto de tempo de design para eliminar assemblies do VS que estão sendo adicionados aos projetos |
|            | Correção de acessibilidade para barra de ferramentas para narrar somente para itens ativos |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| Alterar descrição | Detalhes |
| :----------------- | :------ |
| Correção de um bug que impedia que relatórios sem parâmetros fossem carregados por meio de **Server.LoadReportDefinition**. | &nbsp; |
| O controle WebForms do Visualizador de Relatórios. | Dá suporte à inserção em páginas RTL (páginas que alteram o fluxo de texto usando a propriedade *direction: rtl;* ).<br/><br/>Dá suporte à personalização do texto da caixa de diálogo de impressão por meio da interface de localização *IReportViewerMessages5*.<br/><br/>Suporte a acessibilidade aprimorado.<br/><br/>&bull; &nbsp; &nbsp; [pacote NuGet para o controle do Visualizador de relatórios de WebForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| O controle WinForms do Visualizador de Relatórios. | Correção para impressão quando um aplicativo está em execução em um modo de alto DPI.<br/><br/>&bull; &nbsp; &nbsp; [pacote NuGet para o controle do Visualizador de relatórios de WinForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>Próximas etapas

[Introdução](integrating-reporting-services-using-reportviewer-controls-get-started.md) aos controles do Visualizador de Relatórios.

Ainda tem dúvidas? [Experimente o fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
