---
title: Bibliotecas de classes de itens de relatório personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e65ae16a2297c0f54f16e31e770623c8edd80639
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376798"
---
# <a name="custom-report-item-class-libraries"></a>Bibliotecas de classes de itens de relatório personalizados
  Os itens de relatórios personalizados usam classes do namespace `Microsoft.ReportDesigner`. As classes usadas para implementar um item de relatório personalizado podem ser agrupadas em duas categorias principais: classes exclusivas destinadas a dar suporte à infraestrutura do item de relatório personalizado, e classes de wrapper gerenciado que encapsula a funcionalidade de elementos relevantes em linguagem RDL. Para obter um exemplo de código sobre como usar essas classes, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="custom-report-item-infrastructure-classes"></a>Classes de infraestrutura de itens de relatórios personalizados  
 As classes a seguir são usadas para implementar um item de relatório personalizado.  
  
> [!NOTE]  
>  As tabelas a seguir não são listagens completas; elas incluem apenas as propriedades e os métodos mais usados para cada classe.  
  
### <a name="microsoftreportdesignercustomreportitemdesigner"></a>Microsoft.ReportDesigner.CustomReportItemDesigner  
 Esta é a principal classe de item de relatório personalizado. A classe principal de sua implementação de item de relatório personalizado deve ser herdada dessa classe.  
  
#### <a name="public-properties"></a>Propriedades públicas  
  
|||  
|-|-|  
|`Name`|O nome do item de relatório personalizado.|  
|`Type`|O tipo do item de relatório personalizado.|  
|`CustomData`|Um objeto <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> que encapsula as propriedades de dados do item de relatório personalizado especificadas no momento da criação.|  
|`CustomProperties`|Uma coleção de propriedades personalizadas do item de relatório personalizado.|  
|`Height`|A altura do controle do item de relatório personalizado.|  
|`Width`|A largura do controle do item de relatório personalizado.|  
|`Report`|Um contêiner das propriedades em nível de relatório, como a lista de conjuntos de dados do relatório.|  
|`AltReportItem`|O objeto de item de relatório alternativo, a ser usado onde o controle de item de relatório personalizado em tempo de execução não tem suporte.|  
|`Style`|As propriedades de estilo do item de relatório personalizado.|  
|`Adornment`|Uma janela de adorno usada para a edição interativa do controle.|  
|`Site`|O `ISite` do componente.|  
|`DesignerVerbCollection`|Uma matriz de verbos personalizados do menu de atalho do controle.|  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`BeginEdit`|Ativa a edição interativa do controle.|  
|`DoDefaultAction`|Chamado em resposta ao clique duplo ou pressionamento de Retornar no controle.|  
|`EndEdit`|Desativa a edição interativa do controle.|  
|`GetService`|Retorna um objeto que representa um serviço.|  
|`InitializeNewComponent`|Chamado quando um novo item de relatório personalizado é criado.|  
|`Invalidate`|Redesenha a superfície inteira do controle.|  
|`OnDragEnter`<br /><br /> `OnDragDrop`|Chamado quando um objeto é arrastado para o controle.|  
|`OnPaint`|Chamado em resposta ao evento `Paint`.|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 Este é o atributo usado para identificar o tipo do item de relatório personalizado. O nome deve corresponder ao valor do atributo <`Name`> do elemento `ReportItem` no arquivo de configuração do Designer de Relatórios.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`CustomReportItemAttribute`|Constrói o objeto CustomReportItemAttribute.|  
  
### <a name="microsoftreportdesignerlocalizednameattribute"></a>Microsoft.ReportDesigner.LocalizedNameAttribute  
 Este é o atributo usado para especificar o nome para exibição a ser usado para o designer de item de relatório personalizado.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`LocalizedNameAttribute`|Constrói o objeto LocalizedNameAttribute.|  
  
### <a name="microsoftreportdesigneradornment"></a>Microsoft.ReportDesigner.Adornment  
 A classe `Adornment` é usada pelo componente de item de relatório personalizado em tempo de design para fornecer áreas fora do retângulo principal da superfície de design. Essas áreas podem tratar eventos de interface do usuário, tais como cliques de mouse e operações de arrastar e soltar.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`OnShow`|Chamado quando `Adornment` está ativado.|  
|`OnHide`|Chamado quando `Adornment` está desativado.|  
|`Paint`|Chamado em resposta ao evento `Paint`.|  
|`OnDragEnter`<br /><br /> `OnDragOver`<br /><br /> `OnDragLeave`<br /><br /> `OnDragDrop`|Chamado quando um objeto é arrastado para o `Adornment`.|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 Esta classe é usada para fornecer uma coleção de serviços de exibição usados pelo item de relatório personalizado para dar suporte a objetos `Adornment` para o componente de item de relatório personalizado em tempo de design.  
  
#### <a name="public-properties"></a>Propriedades públicas  
  
|||  
|-|-|  
|`AdornerWindowBounds`|Os limites da janela Adorno.|  
|`AdornerWindowRegion`|A região da janela Adorno.|  
|`AdornerWindowGraphics`|Um contexto gráfico da janela Adorno.|  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`ComponentRectInDesignerFrame`|Retorna os limites do componente convertidos em coordenadas de quadro de designer.|  
|`InvalidateAdorner`|Invalida a janela Adorno.|  
|`PointToAdorner`|Retorna um ponto em coordenadas de tela convertidas em coordenadas da janela Adorno.|  
  
### <a name="microsoftreportdesignerexpressioneditor"></a>Microsoft.ReportDesigner.ExpressionEditor  
 Esta classe pode ser usada de seu controle de item de relatório personalizado em tempo de design para invocar o Editor de Expressão.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`EditValue`|Invoca o Editor de Expressão, inicializado com o valor de objeto determinado.|  
  
### <a name="microsoftreportdesignerifieldsdataobject"></a>Microsoft.ReportDesigner.IFieldsDataObject  
 Esta classe é uma coleção de campos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], usada para dar suporte a eventos de arrastar e soltar no ambiente de design. Herdada de `IReportItemDataObject`.  
  
#### <a name="public-properties"></a>Propriedades públicas  
  
|||  
|-|-|  
|`DataSetName`|O nome do conjunto de dados que contém os campos a serem soltos.|  
|`Fields`|A coleção de campos (`Microsoft.ReportDesigner.Field`) a serem soltos.|  
  
## <a name="see-also"></a>Consulte também  
 [Linguagem RDL &#40;SSRS&#41;](../reports/report-definition-language-ssrs.md)   
 [Criando um componente de item de relatório personalizado em tempo de execução](creating-a-custom-report-item-run-time-component.md)   
 [Criar um componente de tempo de design de item de relatório personalizado](creating-a-custom-report-item-design-time-component.md)  
  
  
