---
title: Compilar uma consulta no designer de consultas relacionais (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 28b25861-f3b4-4c3e-a9b0-03d6e4cfea26
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 98aafe228a4dfe8a2e38667fcf58a61527e103e1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37212376"
---
# <a name="build-a-query-in-the-relational-query-designer-report-builder-and-ssrs"></a>Compilar uma consulta no designer de consulta relacional (Construtor de Relatórios e SSRS)
  Um designer de consulta ajuda a especificar quais dados devem ser recuperados de uma fonte de dados externa para um conjunto de dados de relatório. Você usa um designer de consulta quando compila uma consulta em um assistente ou cria uma consulta de conjunto de dados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Um conjunto de dados se baseia em uma fonte de dados. O tipo de fonte de dados e o ambiente de criação determinam qual designer de consulta é aberto quando você define a consulta de conjunto de dados. Os recursos do designer de consulta variam de acordo com a fonte de dados subjacente. Para obter mais informações sobre as camadas de dados, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no construtor de relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md) ou [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) .  
  
 É possível usar um designer de consulta para as seguintes tarefas:  
  
-   Explorar os metadados de vários esquemas na fonte de dados externa  
  
-   Especificar campos a serem recuperados para o conjunto de dados  
  
-   Especificar relações entre dois objetos, como tabelas  
  
-   Especificar filtros para restringir os dados antes de serem recuperados como dados de relatório  
  
-   Indicar se é necessário criar parâmetros  
  
-   Especificar agregações para executar cálculos na fonte de dados externa  
  
 Depois de abrir um designer de consulta, você cria uma consulta da mesma forma para um conjunto de dados inserido ou um compartilhado. Os procedimentos a seguir usam uma consulta do conjunto de dados inserida.  
  
 Para obter mais informações, consulte [Interface do usuário do Designer de Consultas Relacionais &#40;Construtor de Relatórios&#41;](relational-query-designer-user-interface-report-builder.md).  
  
### <a name="to-build-a-query-for-an-embedded-dataset-in-report-design-view"></a>Para compilar uma consulta para um conjunto de dados inserido na exibição Design do Relatório  
  
1.  Abra o designer de consulta. No painel Dados do Relatório, clique com o botão direito do mouse no conjunto de dados e clique em **Consulta**.  
  
     O designer de consulta associado à fonte de dados é aberto.  
  
2.  No painel de exibição Banco de dados, expanda as pastas que mostrem uma exibição hierárquica dos objetos de esquema de banco de dados, como tabelas, exibições e procedimentos armazenados. Clique na caixa de seleção para selecionar todos os campos para um objeto ou expanda o nó para selecionar campos individuais.  
  
     À medida que você seleciona campos no painel de exibição Banco de Dados, o painel **Selecionar campos** exibe suas seleções.  
  
     Se você selecionar campos de mais de uma tabela de banco de dados relacionada, use o painel Relações para exibir as relações de tabelas detectadas no esquema de banco de dados.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     A lista de campos do conjunto de dados é exibida no painel de dados do relatório.  
  
### <a name="to-specify-limits-for-a-query"></a>Para especificar limites para uma consulta  
  
1.  No designer de consultas relacionais, verifique se você tem campos selecionados e se os campos são exibidos no painel **Campos selecionados** .  
  
2.  Na barra de ferramentas do painel Filtros aplicados, clique em **Adicionar Filtro**. Uma nova linha de filtro é exibida.  
  
3.  Em **Nome do campo**, clique para exibir a lista suspensa de campos e clique no nome do campo pelo qual você deseja filtrar. Por exemplo, para filtrar por quantidade, clique no campo que contém o número de itens.  
  
4.  Em **Operador**, clique para exibir a lista suspensa de operadores e selecione o operador de comparação a ser usado no filtro.  
  
5.  Em **Valor**, digite o valor pelo qual você deseja filtrar. Por exemplo, para filtrar quantidade maior que 100, digite 100.  
  
6.  Selecione a opção de parâmetro nessa linha para criar um parâmetro de conjunto de dados e permitir a um usuário especificar um valor de filtro. Um parâmetro de relatório correspondente ao parâmetro do conjunto de dados é criado automaticamente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 A lista de campos do conjunto de dados é exibida no painel de dados do relatório.  
  
### <a name="to-view-a-query-result-set"></a>Para exibir um conjunto de resultados da consulta  
  
1.  Na barra de ferramentas do designer de consultas, clique em **Executar Consulta (!)**.  
  
    > [!NOTE]  
    >  O designer de consulta usa credenciais do momento do design para executar a consulta e recuperar o conjunto de resultados. Para obter mais informações, consulte [Especificar as credenciais no Construtor de Relatórios](../specify-credentials-in-report-builder.md).  
  
 A consulta é executada na fonte de dados e retorna dados de exemplo no painel de resultados Consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-datasets-ssrs.md)   
 [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md)   
 [Designers de Consultas &#40;Construtor de Relatórios&#41;](../query-designers-report-builder.md)   
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Modo de exibição de Design de relatório &#40;Construtor de Relatórios&#41;](../report-builder/report-design-view-report-builder.md)   
 [Modo de exibição de Design de conjunto de dados compartilhados &#40;Construtor de Relatórios&#41;](../report-builder/shared-dataset-design-view-report-builder.md)   
 [Designers de Consultas do Reporting Services](../reporting-services-query-designers.md)  
  
  
