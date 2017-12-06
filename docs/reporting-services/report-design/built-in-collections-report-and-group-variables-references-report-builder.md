---
title: "Referências de coleções de variáveis de grupo e de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10404"
- "10083"
- sql13.rtp.rptdesigner.groupproperties.variables.f1
- sql13.rtp.rptdesigner.categorygroupproperties.variables.f1
- sql13.rtp.rptdesigner.reportproperties.variables.f1
- "10292"
- sql13.rtp.rptdesigner.seriesgroupproperties.variables.f1
- "10412"
ms.assetid: 4be5b463-3ce2-483d-a3c6-dae752cb543e
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 423768a2a0381377a3d780e632399a41ecf11e5a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="built-in-collections---report-and-group-variables-references-report-builder"></a>Coleções internas – referências de variáveis de grupo e de relatório (Construtor de Relatórios)
  Quando há um cálculo complexo usado mais de uma vez em expressões em um relatório, convém criar uma variável. É possível criar uma variável do relatório ou uma variável do grupo. Os nomes de variável devem ser exclusivos em um relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-variables"></a>Variáveis do relatório  
 Use uma variável do relatório para manter um valor para cálculos dependentes de tempo, como taxas de moeda ou carimbos de data/hora ou para um cálculo complexo que seja referenciado várias vezes. Por padrão, uma variável do relatório é calculada uma vez e pode ser usada em expressões em um relatório. As variáveis de relatório são somente leitura por padrão. Você pode alterar o padrão para habilitar uma variável de relatório como leitura-gravação. O valor em uma variável de relatório é preservado durante toda a sessão, até o relatório ser processado novamente.  
  
 Para adicionar uma variável do relatório, abra a caixa de diálogo **ReportProperties** , clique em **Variáveis**e forneça um nome e um valor. Os nomes são cadeias de caracteres que diferenciam maiúsculas de minúsculas, começando com uma letra e sem espaços. Um nome pode conter letras, números ou sublinhados (_).  
  
 Para fazer referência à variável em uma expressão, use a sintaxe de coleção global, por exemplo, `=Variables!CustomTimeStamp.Value`. Na superfície de design, o valor é exibido em uma caixa de texto como `<<Expr>>`.  
  
 Você pode usar variáveis de relatório dos seguintes modos:  
  
-   **Uso somente leitura** Defina um valor uma vez para criar uma constante para a sessão de relatório, por exemplo, para criar um carimbo de data/hora.  
  
     Como as expressões nas caixas de texto são avaliadas sob demanda como páginas de um usuário em um relatório, os valores dinâmicos (por exemplo, uma expressão que inclui a função `Now()` , que retorna a hora do dia) poderão retornar valores diferentes se você percorrer as páginas para a frente e para trás com o botão **Voltar** . Ao configurar o valor de uma variável do relatório como a expressão `=Now()`e adicionar a variável à expressão, você garante que o mesmo valor seja usado no processamento do relatório.  
  
-   **Uso de leitura-gravação** Defina um valor uma vez e serialize-o dentro da sessão de relatório. A opção de leitura-gravação para variáveis fornece uma alternativa melhor do que o uso de uma variável estática no bloco de Código na definição do relatório.  
  
     Quando você desmarca a opção **Somente Leitura** de uma variável, a propriedade Writable da variável é definida como **true**. Para atualizar o valor de uma expressão, use o método SetValue, por exemplo, `=Variables!MyVariable.SetValue("123")`.  
  
    > [!NOTE]  
    >  Não é possível controlar quando o processador do relatório inicializa uma variável ou avalia uma expressão que atualiza uma variável. A ordem de execução da inicialização da variável não é definida.  
  
 Para obter mais informações, consulte [Visualizar relatórios no Construtor de Relatórios](../../reporting-services/report-builder/previewing-reports-in-report-builder.md).  
  
## <a name="group-variables"></a>Variáveis do grupo  
 Use uma variável do grupo para calcular uma expressão complexa uma vez no escopo de um grupo. Uma variável do grupo é válida apenas no escopo do grupo e de seus grupos filho.  
  
 Por exemplo, suponha que uma região de dados exiba dados de inventário para itens que estão em categorias de impostos diferentes e você queira aplicar taxas de impostos distintas a cada categoria. Você agrupa os dados em Categoria e define uma variável *Tax* no grupo pai. Em seguida, você define uma variável de grupo para *ItemTax* para cada categoria de imposto e atribui cada um dos diferentes subgrupos de Categoria à variável do grupo correto. Por exemplo:  
  
-   Para o grupo pai baseado em `[Category]`, defina a variável *Tax* com um valor `[Tax]`. Suponha que os valores da categoria sejam Alimentos e Vestuário.  
  
-   Para o grupo filho baseado em `[Subcategory]`, defina a variável *ItemsTax* como `=Variables!Tax.Value * Sum(Fields!Price.Value)`. Suponha que os valores da subcategoria para a categoria Alimentos sejam Bebidas e Pães. Suponha que os valores da subcategoria para Vestuário sejam Camisas e Chapéus.  
  
-   Para uma caixa de texto em uma linha no grupo filho, adicione a expressão `=Variables!ItemsTax.Value`.  
  
     A caixa de texto exibe o imposto total para Bebidas e Pães usando o imposto sobre Alimentos e para Camisas e Chapéus usando o imposto sobre Vestuário.  
  
 Para adicionar uma variável do grupo, abra a caixa de diálogo **Propriedades do Grupo Tablix** , clique em **Variáveis**e forneça um nome e um valor. A variável do grupo é calculada uma vez por valor do grupo exclusivo.  
  
 Para fazer referência à variável em uma expressão, use a sintaxe de coleção global, por exemplo, `=Variables!GroupDescription.Value`. Na superfície de design, o valor é exibido em uma caixa de texto como `<<Expr>>`.  
  
## <a name="see-also"></a>Consulte também  
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
