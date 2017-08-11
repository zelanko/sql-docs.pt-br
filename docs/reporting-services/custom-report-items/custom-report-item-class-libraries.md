---
title: "Bibliotecas de classe de Item de relatório personalizado | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
caps.latest.revision: 27
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f216228c01e835e88cd9d4c7d7d4190648a386db
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="custom-report-item-class-libraries"></a>Bibliotecas de classes de itens de relatório personalizados
  Itens de relatório personalizados usam classes do **reportdesigner** namespace. As classes usadas para implementar um item de relatório personalizado podem ser agrupadas em duas categorias principais: classes exclusivas destinadas a dar suporte à infraestrutura do item de relatório personalizado, e classes de wrapper gerenciado que encapsula a funcionalidade de elementos relevantes em linguagem RDL. Para obter um exemplo de código sobre como usar essas classes, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="custom-report-item-infrastructure-classes"></a>Classes de infraestrutura de itens de relatórios personalizados  
 As classes a seguir são usadas para implementar um item de relatório personalizado.  
  
> [!NOTE]  
>  As tabelas a seguir não são listagens completas; elas incluem apenas as propriedades e os métodos mais usados para cada classe.  
  
### <a name="microsoftreportdesignercustomreportitemdesigner"></a>Microsoft.ReportDesigner.CustomReportItemDesigner  
 Esta é a principal classe de item de relatório personalizado. A classe principal de sua implementação de item de relatório personalizado deve ser herdada dessa classe.  
  
#### <a name="public-properties"></a>Propriedades públicas  
  
|||  
|-|-|  
|**Nome**|O nome do item de relatório personalizado.|  
|**Tipo**|O tipo do item de relatório personalizado.|  
|**CustomData**|Um objeto <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> que encapsula as propriedades de dados do item de relatório personalizado especificadas no momento da criação.|  
|**CustomProperties**|Uma coleção de propriedades personalizadas do item de relatório personalizado.|  
|**Altura**|A altura do controle do item de relatório personalizado.|  
|**Largura**|A largura do controle do item de relatório personalizado.|  
|**Relatório**|Um contêiner das propriedades em nível de relatório, como a lista de conjuntos de dados do relatório.|  
|**AltReportItem**|O objeto de item de relatório alternativo, a ser usado onde o controle de item de relatório personalizado em tempo de execução não tem suporte.|  
|**Estilo**|As propriedades de estilo do item de relatório personalizado.|  
|**Adornos**|Uma janela de adorno usada para a edição interativa do controle.|  
|**Site**|O **ISite** do componente.|  
|**DesignerVerbCollection**|Uma matriz de verbos personalizados do menu de atalho do controle.|  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**BeginEdit**|Ativa a edição interativa do controle.|  
|**DoDefaultAction**|Chamado em resposta ao clique duplo ou pressionamento de Retornar no controle.|  
|**EndEdit**|Desativa a edição interativa do controle.|  
|**GetService**|Retorna um objeto que representa um serviço.|  
|**InitializeNewComponent**|Chamado quando um novo item de relatório personalizado é criado.|  
|**Invalidar**|Redesenha a superfície inteira do controle.|  
|**OnDragEnter**<br /><br /> **OnDragDrop**|Chamado quando um objeto é arrastado para o controle.|  
|**OnPaint**|Chamado em resposta ao **pintura** eventos.|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 Este é o atributo usado para identificar o tipo do item de relatório personalizado. O nome deve corresponder ao valor da \< **nome**> atributo o **ReportItem** elemento no arquivo de configuração do Designer de relatórios.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**CustomReportItemAttribute**|Constrói o objeto CustomReportItemAttribute.|  
  
### <a name="microsoftreportdesignerlocalizednameattribute"></a>Microsoft.ReportDesigner.LocalizedNameAttribute  
 Este é o atributo usado para especificar o nome para exibição a ser usado para o designer de item de relatório personalizado.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**LocalizedNameAttribute**|Constrói o objeto LocalizedNameAttribute.|  
  
### <a name="microsoftreportdesigneradornment"></a>Microsoft.ReportDesigner.Adornment  
 O **adorno** classe é usada pelo componente de tempo de design de item de relatório personalizado forneça áreas fora do retângulo principal da superfície de design. Essas áreas podem tratar eventos de interface do usuário, tais como cliques de mouse e operações de arrastar e soltar.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**OnShow**|Chamado quando o **adorno** está ativado.|  
|**OnHide**|Chamado quando o **adorno** está desativado.|  
|**Horas de pintura**|Chamado em resposta ao **pintura** eventos.|  
|**OnDragEnter**<br /><br /> **OnDragOver**<br /><br /> **OnDragLeave**<br /><br /> **OnDragDrop**|Chamado quando um objeto é arrastado para o **adorno**.|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 Essa classe é usada para fornecer um conjunto de serviços de exibição usados pelo item de relatório personalizado para dar suporte a **adorno** objetos para o componente de tempo de design de item de relatório personalizado.  
  
#### <a name="public-properties"></a>Propriedades públicas  
  
|||  
|-|-|  
|**AdornerWindowBounds**|Os limites da janela Adorno.|  
|**AdornerWindowRegion**|A região da janela Adorno.|  
|**AdornerWindowGraphics**|Um contexto gráfico da janela Adorno.|  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**ComponentRectInDesignerFrame**|Retorna os limites do componente convertidos em coordenadas de quadro de designer.|  
|**InvalidateAdorner**|Invalida a janela Adorno.|  
|**PointToAdorner**|Retorna um ponto em coordenadas de tela convertidas em coordenadas da janela Adorno.|  
  
### <a name="microsoftreportdesignerexpressioneditor"></a>Microsoft.ReportDesigner.ExpressionEditor  
 Esta classe pode ser usada de seu controle de item de relatório personalizado em tempo de design para invocar o Editor de Expressão.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**EditValue**|Invoca o Editor de Expressão, inicializado com o valor de objeto determinado.|  
  
### <a name="microsoftreportdesignerifieldsdataobject"></a>Microsoft.ReportDesigner.IFieldsDataObject  
 Esta classe é uma coleção de campos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], usada para dar suporte a eventos de arrastar e soltar no ambiente de design. Herda de **IReportItemDataObject**.  
  
#### <a name="public-properties"></a>Propriedades públicas  
  
|||  
|-|-|  
|**DataSetName**|O nome do conjunto de dados que contém os campos a serem soltos.|  
|**Campos**|A coleção de campos (**Microsoft.ReportDesigner.Field**) a ser removido.|  
  
## <a name="see-also"></a>Consulte também  
 [Linguagem de definição de relatório &#40; SSRS &#41;](../../reporting-services/reports/report-definition-language-ssrs.md)   
 [Criando um componente de tempo de execução do Item de relatório personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Criando um componente de tempo de Design de Item de relatório personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
  
  
