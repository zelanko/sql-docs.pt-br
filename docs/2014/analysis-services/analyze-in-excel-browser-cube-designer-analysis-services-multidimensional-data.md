---
title: Analisar no Excel (guia navegador, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.datapane.f1
- sql12.asvs.ssms.analyzeinexcel.f1
ms.assetid: 890ed457-137e-44ac-9b2c-83344a1b8fc9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cdd0c98a00b5643c73b1536b7449c855a444aea8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62643514"
---
# <a name="analyze-in-excel-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Analisar no Excel (guia Navegador, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  **Analisar no Excel** oferece ao desenvolvedor de cubo uma forma rápida de examinar a aparência de um projeto para o usuário final. O recurso **Analisar no Excel** abre o Microsoft Excel, cria uma conexão da fonte de dados para o banco de dados de workspace e adiciona automaticamente uma Tabela Dinâmica à planilha. Esse recurso substitui o Office Web Control que forneceu um Tabela Dinâmica inserida na guia Navegador nas versões anteriores.  
  
 **Para exibir dados de cubo:**  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no Gerenciador de Soluções, clique duas vezes em um cubo para abri-lo no Designer de Cubo.  
  
2.  Clique na guia **Navegador** .  
  
3.  Clique em **Reconectar** para validar a conexão.  
  
4.  Clique no ícone do Excel na barra de menus.  
  
5.  Quando solicitado a habilitar conexões de dados, clique em **Habilitar**. O Excel é aberto usando a conexão de dados atual, adicionando uma Tabela Dinâmica à planilha para que você possa começar a procurar seus dados.  
  
 Agora você pode criar uma Tabela Dinâmica de modo interativo arrastando medidas da tabela de fatos para a área Valores e atributos de dimensão para as áreas Linha e Coluna. Se você tiver hierarquias, adicione-as às áreas Linhas ou Coluna. Você pode acumular ou fazer uma busca detalhada na hierarquia para procurar dados de fato em níveis diferentes.  
  
 Os objetos e os dados são exibidos no contexto do usuário efetivo ou de função e perspectiva. Ao usar o Excel, as credenciais do usuário atual, e não as credenciais especificadas na página **Informações da Representação** , são usadas na conexão com a fonte de dados quando uma consulta é executada.  
  
> [!NOTE]  
>  Para usar o recurso Analisar no Excel, o Excel deve estar instalado no mesmo computador do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Se o Excel não estiver instalado no mesmo computador, você poderá usar o Excel em outro computador e conectar-se ao cubo como uma fonte de dados. Você pode então adicionar manualmente uma Tabela Dinâmica à planilha. Os objetos de modelo (tabelas, colunas, medidas e KPIs) são incluídos como campos na lista de campos da Tabela Dinâmica.  
  
 Para obter mais informações sobre o recurso **Analisar no Excel** , consulte estes recursos:  
  
 [Analisar no Excel &#40;SSAS de Tabela&#41;](tabular-models/analyze-in-excel-ssas-tabular.md)  
  
 [Analisar um modelo de tabela no Excel &#40;SSAS de Tabela&#41;](tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)  
  
 [Procurar dados e metadados no Cubo](multidimensional-models/browse-data-and-metadata-in-cube.md)  
  
## <a name="see-also"></a>Consulte também  
 [Navegador &#40;Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia do navegador, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Metadados &#40;guia do navegador, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Consulta e filtro &#40;guia do navegador, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  
