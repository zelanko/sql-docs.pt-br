---
title: "Modificar ou excluir um banco de dados do Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "bancos de dados [Analysis Services], modificando"
  - "removendo bancos de dados"
  - "excluindo bancos de dados"
  - "descartando bancos de dados"
  - "bancos de dados [Analysis Services], excluindo"
  - "modificando bancos de dados"
ms.assetid: e48e3988-c091-4379-aabc-4da62f709a7e
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 34
---
# Modificar ou excluir um banco de dados do Analysis Services
  É possível alterar o nome e a descrição de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] antes da implantação no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e depois da implantação no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Também é possível ajustar configurações adicionais de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], dependendo do ambiente.  
  
> [!NOTE]  
>  Não é possível alterar as propriedades do banco de dados usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online.  
  
## Modificando banco de dados usando o SQL Server Management Studio  
 Uma vez implantado o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para alterar o modo de representação usado pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ao se conectar com as fontes de dados contidas no banco de dados. O modo de representação permite que você especifique o contexto de segurança usado pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ao tentar conectar-se com uma fonte de dados para fins de processamento, navegação ou detalhamento.  
  
## Modificando banco de dados usando as Ferramentas de Dados do SQL Server  
 Use o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo de projeto para modificar as traduções de legenda e a descrição de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usado para definir um banco de dados. Para obter mais informações sobre como usar traduções em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Cenários de globalização para Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md).  
  
 Também é possível definir alises e funções de agregação associados a tipos de contas usados pelos atributos de conta em dimensões contidas no banco de dados. Os aliases permitem a seleção da terminologia específica do ramo usada pela empresa para os tipos de contas do plano de contas. Os tipos de conta são usados pelos membros de um atributo de conta para indicar como agregar medidas em cada membro usando as funções de agregação especificadas para cada tipo de conta existente no banco de dados. Para obter mais informações sobre os atributos de conta, consulte [Atributos e hierarquias de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## Excluindo bancos de dados  
 A exclusão de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exclui o banco de dados e todos os seus cubos, dimensões e modelos de mineração. É possível excluir um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] somente no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### Para excluir um banco de dados do Analysis Services  
  
1.  Conecte-se a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
2.  No **Pesquisador de Objetos**, expanda o nó da instância conectada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e verifique se o objeto a ser excluído está visível.  
  
3.  Clique com o botão direito do mouse no objeto a ser excluído e selecione **Excluir**.  
  
4.  Na caixa de diálogo **Excluir Objeto** , clique em **OK**.  
  
## Consulte também  
 [Documentar e gerar scripts de um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
  