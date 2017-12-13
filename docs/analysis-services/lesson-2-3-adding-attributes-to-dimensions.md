---
title: "Adicionando atributos em dimensões | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 80551dad-97ac-40d0-90af-b810780321ce
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 4a04d6929acc77aeaf3190e65dacf933995189ee
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="lesson-2-3---adding-attributes-to-dimensions"></a>Lição 2-3-adicionar atributos às dimensões
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]Agora que você definiu dimensões, você pode populá-las com atributos que representam cada elemento de dados na dimensão. Os atributos geralmente são baseados em campos de uma exibição da fonte de dados. Ao adicionar atributos a uma dimensão, você pode incluir campos de qualquer tabela na exibição da fonte de dados.  
  
Nesta tarefa, você usará o Designer de Dimensão para adicionar atributos às dimensões Cliente e Produto. A dimensão de Cliente incluirá atributos baseados em campos de ambas as tabelas de Cliente e Geografia.  
  
## <a name="adding-attributes-to-the-customer-dimension"></a>Adicionando atributos à dimensão Cliente  
  
#### <a name="to-add-attributes"></a>Para adicionar atributos  
  
1.  Abra o Designer de Dimensão da dimensão Cliente. Para fazer isso, clique duas vezes na dimensão **Cliente** no nó **Dimensões** do Gerenciador de Soluções.  
  
2.  No painel **Atributos** , observe os atributos Customer Key e Geography Key que foram criados pelo Assistente para Cubos.  
  
3.  Na barra de ferramentas da guia **Estrutura da Dimensão** , verifique se o ícone Zoom para exibir as tabelas do painel **Exibição da Fonte de Dados** está definido para 100%.  
  
4.  Arraste as seguintes colunas da tabela **Customer** do painel **Exibição da Fonte de Dados** para o painel **Atributos** :  
  
    -   **BirthDate**  
  
    -   **MaritalStatus**  
  
    -   **Gênero**  
  
    -   **EmailAddress**  
  
    -   **YearlyIncome**  
  
    -   **TotalChildren**  
  
    -   **NumberChildrenAtHome**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **HouseOwnerFlag**  
  
    -   **NumberCarsOwned**  
  
    -   **Phone**  
  
    -   **DateFirstPurchase**  
  
    -   **CommuteDistance**  
  
5.  Arraste as seguintes colunas da tabela **Geography** do painel **Exibição da Fonte de Dados** para o painel **Atributos** :  
  
    -   **Cidade**  
  
    -   **StateProvinceName**  
  
    -   **EnglishCountryRegionName**  
  
    -   **PostalCode**  
  
6.  No menu Arquivo, clique em **Salvar Tudo**.  
  
## <a name="adding-attributes-to-the-product-dimension"></a>Adicionando atributos à dimensão Produto  
  
#### <a name="to-add-attributes"></a>Para adicionar atributos  
  
1.  Abra o Designer de Dimensão da dimensão Produto. Clique duas vezes na dimensão **Produto** no Gerenciador de Soluções.  
  
2.  No painel **Atributos** , observe o atributo Product Key que foi criado pelo Assistente para Cubos.  
  
3.  Na barra de ferramentas da guia **Estrutura da Dimensão** , verifique se o ícone Zoom para exibir as tabelas do painel **Exibição da Fonte de Dados** está definido para 100%.  
  
4.  Arraste as seguintes colunas da tabela **Product** do painel **Exibição da Fonte de Dados** para o painel **Atributos** :  
  
    -   **StandardCost**  
  
    -   **Color**  
  
    -   **SafetyStockLevel**  
  
    -   **ReorderPoint**  
  
    -   **ListPrice**  
  
    -   **Tamanho**  
  
    -   **SizeRange**  
  
    -   **Weight**  
  
    -   **DaysToManufacture**  
  
    -   **ProductLine**  
  
    -   **DealerPrice**  
  
    -   **Classe**  
  
    -   **Estilo**  
  
    -   **ModelName**  
  
    -   **StartDate**  
  
    -   **EndDate**  
  
    -   **Status**  
  
5.  No menu Arquivo, clique em **Salvar Tudo**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Revisando as propriedades de dimensão e cubo](../analysis-services/lesson-2-4-reviewing-cube-and-dimension-properties.md)  
  
## <a name="see-also"></a>Consulte também  
[Referência de propriedades de atributo de dimensão](../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
  
