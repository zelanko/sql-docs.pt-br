---
title: "Trabalhar com diagramas em Designer de exibição de fonte de dados (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.dsvdesigner.findtable.f1
- sql13.asvs.dsvdesigner.diagramorganizerpane.f1
- sql13.asvs.dsvdesigner.diagrampane.f1
helpviewer_keywords:
- data source views [Analysis Services], diagrams
- diagrams [Analysis Services]
ms.assetid: 491fdd22-2326-4f27-a0dd-0a02faae3fd8
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b3e877f63972f6a891f788a65196d2ec621cc203
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="work-with-diagrams-in-data-source-view-designer-analysis-services"></a>Trabalhar com diagramas em um Designer de exibição da fonte de dados (Analysis Services)
  Um diagrama DSV (exibição de fonte de dados) é uma representação visual dos objetos em um DSV. Você pode trabalhar com o diagrama interativamente para adicionar, ocultar, excluir ou modificar objetos específicos. Você também pode criar vários diagramas no mesmo DSV para concentrar a atenção em um subconjunto dos objetos.  
  
 Para alterar a área do diagrama exibida no painel de diagrama, clique na seta de quatro pontas no canto inferior direito do painel e arraste a caixa de seleção sobre o diagrama em miniatura até selecionar a área que deve ser exibida no painel de diagrama.  
  
 Este tópico inclui as seguintes seções:  
  
 [Adicionar um diagrama](#bkmk_add)  
  
 [Editar ou excluir um diagrama](#bkmk_edit)  
  
 [Localizar tabelas em um diagrama](#bkmk_findtables)  
  
 [Organizar os objetos em um diagrama](#bkmk_arrangeobjects)  
  
 [Preservar a organização do objeto](#bkmk_preserve)  
  
##  <a name="bkmk_add"></a> Adicionar um diagrama  
 Diagramas de DSV são criados automaticamente quando você cria o DSV. Depois que o DSV existe, você pode criar diagramas adicionais, removê-los ou ocultar objetos específicos para criar uma representação mais gerenciável do DSV.  
  
 Para criar um novo diagrama, clique com o botão direito do mouse em qualquer lugar do painel **Organizador de Diagramas** , clique em **Novo Diagrama**.  
  
 Quando você define inicialmente uma exibição da fonte de dados (DSV) em um projeto do Analysis Services, todas as tabelas e exibições adicionadas à exibição de fonte de dados são adicionadas para o \<todas as tabelas > diagrama. Esse diagrama aparece no painel Organizador de Diagramas do Designer de Exibição da Fonte de Dados, suas tabelas (bem como colunas e relações) são listadas no painel Tabelas e as tabelas desse diagrama (bem como colunas e relações) são exibidas graficamente no painel do esquema. No entanto, como adicionar tabelas, exibições e consultas nomeadas para o \<todas as tabelas > diagrama, o número absoluto de objetos nesse diagrama dificulta a visualização das relações, particularmente como várias tabelas de fatos são adicionadas ao diagrama e de dimensão tabelas se relacionam com várias tabelas de fatos.  
  
 Para reduzir a poluição visual quando você quer apenas exibir um subconjunto das tabelas da exibição da fonte de dados, é possível definir subdiagramas (chamados simplesmente de diagramas) formados por subconjuntos das tabelas, exibições e consultas nomeadas da exibição da fonte de dados. Você pode usar diagramas para agrupar itens da exibição da fonte de dados de acordo com as necessidades dos negócios ou da solução.  
  
 É possível agrupar tabelas e consultas nomeadas relacionadas em diagramas separados de acordo com os negócios e facilitar o entendimento da exibição da fonte de dados que contém muitas tabelas, exibições e consultas nomeadas. A mesma tabela ou consulta nomeada pode ser incluída em vários diagramas, exceto para o \<todas as tabelas > diagrama. No \<todas as tabelas > diagrama, todos os objetos que estão contidos na exibição da fonte de dados são mostrados exatamente uma vez.  
  
##  <a name="bkmk_edit"></a> Editar ou excluir um diagrama  
 Ao trabalhar com um diagrama, preste atenção aos comandos usados por adicionar e remover objetos. Por exemplo, excluir um objeto de um diagrama o excluirá da DSV. Se você apenas desejar excluí-lo do diagrama, use **Ocultar Tabela** em vez disso.  
  
 ![Captura de tela de espaço de trabalho de diagrama, menu de atalho](../../analysis-services/multidimensional-models/media/ssas-olapdsv-diagram.gif "captura de tela de espaço de trabalho de diagrama, menu de atalho")  
  
 Embora você possa ocultar objetos individualmente, trazê-los de volta usando o comando Mostrar Tabelas Relacionadas retorna todos os objetos relacionados ao diagrama. Para controlar quais objetos são retornados para o espaço de trabalho, arraste-os do painel de Tabelas em vez disso.  
  
##  <a name="bkmk_findtables"></a> Localizar tabelas em um diagrama  
 Se o esquema for grande, poderá ser difícil rolar uma determinada tabela no painel **Diagrama** . No entanto, as ferramentas a seguir facilitam a localização de uma tabela em um diagrama.  
  
-   Role a lista de tabelas no painel **Tabelas** .  
  
     Para incluir uma tabela no diagrama exibido no momento, arraste a tabela do painel **Tabelas** para o painel de diagrama.  
  
     Para centralizar a exibição em uma tabela que já está incluída no diagrama, selecione a tabela no painel **Tabelas** .  
  
-   Localizador de tabelas do painel **Diagrama** – o localizador de tabela é um ícone de 4 setas na intersecção das barras de rolagem vertical e horizontal no canto direito inferior do painel **Diagrama** . Ele abre uma representação em miniatura do diagrama atual no painel Diagrama. Você pode usar essa miniatura para alterar a exibição do painel Diagrama para qualquer local no diagrama.  
  
-   Use a caixa de diálogo **Localizar Tabela** – Clique com o botão direito do mouse em uma área livre do painel Diagrama e clique em **Localizar Tabela**. Ou clique no comando **Localizar Tabela** na barra de ferramentas ou no menu **Exibição da Fonte de Dados** .  
  
     Você pode digitar cadeias de caracteres e caracteres curinga na caixa Filtro para exibir subconjuntos das tabelas no diagrama.  
  
##  <a name="bkmk_arrangeobjects"></a> Organizar os objetos em um diagrama  
 Embora o Designer de Exibição da Fonte de Dados possa definir vários diagramas para facilitar o entendimento da DSV, pode ser difícil a leitura de diagramas com dezenas de tabelas, bem como a reorganização manual dos layouts de tabelas pode ser um processo entediante. O Designer de Exibição da Fonte de Dados pode reorganizar automaticamente as tabelas do diagrama atual em um layout retangular ou diagonal com base nas relações entre as tabelas do mesmo.  
  
-   No layout retangular, as linhas de relações são desenhadas entre as tabelas em vez de entre colunas. As linhas de relação são desenhadas horizontal e verticalmente entre as tabelas.  
  
-   No layout diagonal, as linhas de relação são desenhadas o mais diretamente possível entre colunas relacionadas das tabelas. Uma relação com várias colunas é anexada à primeira coluna relacionada da tabela. Se as colunas de uma tabela não ficarem visíveis, as linhas serão desenhadas por cima da tabela.  
  
##  <a name="bkmk_preserve"></a> Preservar a organização do objeto  
 Depois de organizar manualmente as tabelas da maneira desejada, adicionar mais tabelas ao diagrama pode fazer um diagrama remover todas as alterações recentes feitas no layout do objeto.  
  
 Esse comportamento é mais provável de ocorrer quando você adiciona uma tabela, fazendo o organizador de diagramas mover outras tabelas para acomodar a nova. Ele redesenha o diagrama para assegurar que todas as tabelas e linhas de conexão sejam representadas corretamente. Neste momento, os ajustes manuais na colocação de objetos específicos podem ser perdidos.  
  
 Para evitar esse problema, adicione todas as tabelas primeiro, antes de fazer algum ajuste final. Os objetos devem agora manter sua posição no diagrama quando você abri-lo novamente mais tarde.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Designer de exibição de fonte de dados &#40; Analysis Services - dados multidimensionais &#41;](http://msdn.microsoft.com/library/6f40a074-761f-440b-a999-09b755bd86ce)  
  
  

