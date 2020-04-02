---
title: Bibliotecas de classes de itens de relatório personalizados | Microsoft Docs
description: Saiba mais sobre as bibliotecas de classes de itens de relatório personalizados e use exemplos de código para entender como usar essas classes.
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f30b581c67eb161bd0d221b9a4aa341d90ab7148
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80216941"
---
# <a name="custom-report-item-class-libraries"></a>Bibliotecas de classes de itens de relatório personalizados
  Os itens de relatório personalizados usam classes do namespace **Microsoft.ReportDesigner**. As classes usadas para implementar um item de relatório personalizado podem ser agrupadas em duas categorias principais: classes exclusivas destinadas a dar suporte à infraestrutura do item de relatório personalizado, e classes de wrapper gerenciado que encapsula a funcionalidade de elementos relevantes em linguagem RDL. Para obter um exemplo de código sobre como usar essas classes, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
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
|**Height**|A altura do controle do item de relatório personalizado.|  
|**Width**|A largura do controle do item de relatório personalizado.|  
|**Report**|Um contêiner das propriedades em nível de relatório, como a lista de conjuntos de dados do relatório.|  
|**AltReportItem**|O objeto de item de relatório alternativo, a ser usado onde o controle de item de relatório personalizado em tempo de execução não tem suporte.|  
|**Estilo**|As propriedades de estilo do item de relatório personalizado.|  
|**Adornment**|Uma janela de adorno usada para a edição interativa do controle.|  
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
|**Invalidate**|Redesenha a superfície inteira do controle.|  
|**OnDragEnter**<br /><br /> **OnDragDrop**|Chamado quando um objeto é arrastado para o controle.|  
|**OnPaint**|Chamado em resposta ao evento **Paint**.|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 Este é o atributo usado para identificar o tipo do item de relatório personalizado. O nome deve corresponder ao valor do atributo \<**Name**> do elemento **ReportItem** no arquivo de configuração do Designer de Relatórios.  
  
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
 A classe **Adornment** é usada pelo componente de item de relatório personalizado em tempo de design para fornecer áreas fora do retângulo principal da área de design. Essas áreas podem tratar eventos de interface do usuário, tais como cliques de mouse e operações de arrastar e soltar.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**OnShow**|Chamado quando o **Adornment** é ativado.|  
|**OnHide**|Chamado quando o **Adornment** é desativado.|  
|**Paint**|Chamado em resposta ao evento **Paint**.|  
|**OnDragEnter**<br /><br /> **OnDragOver**<br /><br /> **OnDragLeave**<br /><br /> **OnDragDrop**|Chamado quando um objeto é arrastado para o **Adornment**.|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 Essa classe é usada para fornecer uma coleção de serviços de exibição usados pelo item de relatório personalizado para dar suporte a objetos **Adornment** para o componente de item de relatório personalizado em tempo de design.  
  
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
|**Fields**|A coleção de campos (**Microsoft.ReportDesigner.Field**) a ser removida.|  
  
## <a name="see-also"></a>Consulte Também  
 [Linguagem RDL &#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md)   
 [Criando um componente de item de relatório personalizado em tempo de execução](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Criar um componente de tempo de design de item de relatório personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
  
  
