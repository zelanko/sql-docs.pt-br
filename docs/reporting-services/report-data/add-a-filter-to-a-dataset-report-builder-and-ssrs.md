---
title: "Adicionar um filtro a um conjunto de dados (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eed37e74-6a43-4d7c-9959-2d5fa6a6aba9
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68838748a77567747cd7f44f7924738d87b68450
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="add-a-filter-to-a-dataset-report-builder-and-ssrs"></a>Adicionar um filtro a um conjunto de dados (Construtor de Relatórios e SSRS)
  Adicione um filtro a um conjunto de dados para limitar os dados em um relatório depois que os dados forem recuperados de uma fonte de dados externa. Quando você adiciona um filtro a um conjunto de dados, todas as partes de relatório ou regiões de dados usam somente dados que correspondem às condições de filtro.  
  
 Para um conjunto de dados compartilhado, um filtro que se aplica a todos os itens dependentes deve fazer parte da definição de banco de dados compartilhada no servidor de relatório. Um relatório ou parte de relatório que contém uma instância de um conjunto de dados compartilhado pode criar um filtro adicional que se aplica somente à instância.  
  
 Para adicionar um filtro, é necessário especificar uma ou mais condições que são equações de filtro. Uma equação de filtro é composta por uma expressão que identifica os dados que você deseja filtrar, um operador, e o valor para comparação. Os tipos de dados dos dados filtrados e o valor devem coincidir. Não há suporte para filtragem de valores de agregação para um conjunto de dados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-filter-to-a-shared-dataset"></a>Para adicionar um filtro a um banco de dados compartilhado  
  
1.  Abra um conjunto de dados compartilhado em modo compartilhado.  
  
2.  Na guia **Página Inicial** , no grupo **Conjunto de Dados Compartilhado** , clique em Conjunto de Dados. A caixa de diálogo **Propriedades do Conjunto de Dados** é aberta.  
  
3.  Clique em **Filtros**. Isso exibirá a lista atual de equações de filtros. Por padrão, a lista está vazia.  
  
4.  Clique em **Adicionar**. Uma nova equação de filtro em branco é exibida.  
  
5.  Em **Expressão**, digite ou selecione a expressão do campo a ser filtrada. Para editar a expressão, clique no botão de expressão (*fx*).  
  
6.  Na caixa de lista, selecione o tipo de dados que corresponde ao tipo de dados da expressão criada na etapa 5.  
  
7.  Na caixa **Operador** , selecione o operador que você deseja que o filtro use para comparar os valores nas caixas **Expressão** e **Valor** . O operador escolhido determinará o número de valores que serão usados na próxima etapa.  
  
8.  Na caixa **Valor**, digite a expressão ou o valor em relação ao qual você deseja que o filtro avalie o valor em **Expressão**.  
  
     Para obter exemplos de equações de filtro, consulte [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-filter-to-an-embedded-dataset-or-a-shared-dataset-instance"></a>Para adicionar um filtro a um conjunto de dados inserido ou uma instância de conjunto de dados compartilhada  
  
1.  Abra um relatório no modo de design de relatório.  
  
2.  Clique com o botão direito do mouse no painel **Dados do Relatório** e clique em **Propriedades do Conjunto de Dados**. A caixa de diálogo **Propriedades do Conjunto de Dados** é aberta.  
  
3.  Clique em **Filtros**. Isso exibirá a lista atual de equações de filtros. Por padrão, a lista está vazia.  
  
4.  Clique em **Adicionar**. Uma nova equação de filtro em branco é exibida.  
  
5.  Em **Expressão**, digite ou selecione a expressão do campo a ser filtrada. Para editar a expressão, clique no botão de expressão (*fx*).  
  
6.  Na caixa suspensa, selecione o tipo de dados que coincide com o tipo de dados da expressão criada na etapa 5.  
  
7.  Na caixa **Operador** , selecione o operador que você deseja que o filtro use para comparar os valores nas caixas **Expressão** e **Valor** . O operador escolhido determinará o número de valores que serão usados na próxima etapa.  
  
8.  Na caixa **Valor**, digite a expressão ou o valor em relação ao qual você deseja que o filtro avalie o valor em **Expressão**.  
  
     Para obter exemplos de equações de filtro, consulte [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar filtros de conjunto de dados, filtros de região de dados e filtros de grupo &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Exemplos de expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Adicionar um filtro &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/add-a-filter-report-builder-and-ssrs.md)  
  
  
