---
title: Detectar categorias (ferramentas de análise de tabela para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- clustering [data mining]
- mining model, decision tree
- category detection
ms.assetid: 3c7e9ebb-d0c9-498e-a9ba-cc13eaa43520
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c54c6f369d519812bb79cacf51bd1ad00a1dfb5
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175215"
---
# <a name="detect-categories-table-analysis-tools-for-excel"></a>Detectar Categorias (Ferramentas de Análise de Tabela para Excel)
  ![Botão Detectar Categorias na faixa de opções](media/tat-detectcat.gif "Botão Detectar Categorias na faixa de opções")

 A ferramenta **detectar categorias** localiza automaticamente linhas em uma tabela que têm características semelhantes.

 Quando a ferramenta termina, cria um relatório que lista as categorias encontradas, junto com suas características de distinção. Por padrão, ela adiciona uma nova coluna à tabela de dados que contém a categoria proposta para cada linha de dados. Assim, você pode examinar as categorias e renomeá-las.

## <a name="using-the-detect-categories-tool"></a>Usando a ferramenta Detectar Categorias

1.  Abra uma tabela do Excel.

2.  Clique em **detectar categorias**.

3.  Especifique as colunas a serem usadas na análise. Você pode desmarcar colunas que tenham valores discretos, como nomes pessoais ou IDs de registro, porque essas colunas talvez não sejam úteis para análise.

4.  Se desejar, especifique o número máximo de categorias a serem criadas. Por padrão, a ferramenta cria automaticamente tantas categorias quantas encontra.

5.  Clique em **Executar**.

6.  A ferramenta cria uma nova planilha, denominada Relatório de Categorias, que contém a lista de categorias e suas características.

 Para obter mais informações sobre como especificar opções para a ferramenta, consulte [caixa de diálogo detectar categorias (ferramentas de análise de tabela para Excel)](detect-categories-table-analysis-tools-for-excel.md).

## <a name="understanding-the-categories-report"></a>Compreendendo o Relatório de Categorias
 O **relatório categorias** contém duas tabelas, a **lista de categorias** e as características da **categoria**e um gráfico de perfis de **categoria** .

### <a name="category-list"></a>Lista de categorias
 A primeira tabela lista as categorias encontradas. A coluna **contagem de linhas** indica quantas linhas de dados foram atribuídas a cada categoria.

 O modelo cria nomes temporários para cada categoria, mas você pode renomear as categorias como quiser. Por exemplo, no exemplo a seguir, a primeira categoria foi renomeada como **baixa renda**, pois esse era o atributo superior do cluster.

 ![relatório criado pela ferramenta Detectar Categorias](media/dm13-tat-detectcat-report1.gif "relatório criado pela ferramenta Detectar Categorias")

 Assim que você digita o novo rótulo, a alteração é propagada para todos os outros gráficos, bem como para a lista de categorias adicionada à planilha de dados de origem.

### <a name="category-characteristics"></a>Características da Categoria
 A segunda tabela, **características da categoria**, mostra detalhes sobre a composição de cada categoria. Clique no botão **Filtrar** na parte superior da coluna **categoria** para ver o foco em uma ou apenas algumas categorias.

 ![relatório criado pela ferramenta Detectar Categorias](media/dm13-tat-detectcat-report2.gif "relatório criado pela ferramenta Detectar Categorias")

 O sombreamento na coluna, **importância relativa**, indica a importância dessa combinação de atributo e valor como um fator de distinção. Quanto maior a barra, maior a probabilidade de que esse atributo represente fortemente essa categoria.

### <a name="categories-profile-chart"></a>Gráfico Perfil de Categorias
 O gráfico final na planilha de **relatório categorias** , **perfis de categoria**, é um **gráfico dinâmico** interativo que você pode usar para reorganizar e ocultar campos, filtrar valores e personalizar a aparência do gráfico.

 O Excel 2013 agora fornece controles de **gráfico** e de **elementos de gráfico** diretamente na superfície de design que facilita a melhoria do design do gráfico.

 ![relatório criado pela ferramenta Detectar Categorias](media/dm13-tat-detectcat-report3.gif "relatório criado pela ferramenta Detectar Categorias")

## <a name="requirements"></a>Requisitos
 A ferramenta **detectar categorias** não tem requisitos para a quantidade ou o tipo de dados.

> [!NOTE]
>  Quando você usa a ferramenta **detectar categorias** , ela cria uma nova coluna, categoria, na tabela de dados original. Se você deixar essa coluna na tabela de dados e, em seguida, executar operações subsequentes de mineração de dados, a presença dessa coluna poderá influenciar os resultados. Para assegurar que isso não afete outras operações, faça uma cópia da tabela de dados sem a coluna Categoria, antes de usar outras ferramentas de mineração de dados.

## <a name="related-tools"></a>Ferramentas relacionadas
 Quando a ferramenta **detectar categorias** analisa seus dados, ela cria uma estrutura de data mining e um modelo de Data Mining usando [!INCLUDE[msCoName](../includes/msconame-md.md)] o algoritmo de clustering.

 Depois de criar um modelo de Data Mining usando a ferramenta **analisar influenciadores principais** , você pode usar o cliente de mineração de dados para Excel para procurar o modelo e explorar relações com mais detalhes. O Cliente de Mineração de Dados para Excel é um suplemento separado que fornece funções de mineração de dados mais avançadas. Para obter informações, consulte [procurando modelos no Excel &#40;SQL Server suplementos de mineração de dados&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md).

 Para obter mais informações sobre como usar os recursos de modelagem de dados no cliente de mineração de dados para Excel, consulte [criando um modelo de mineração de dados](creating-a-data-mining-model.md).

 Para obter mais informações sobre o algoritmo usado pela ferramenta **detectar categorias** , consulte o tópico "algoritmo de clustering da Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] " nos manuais online do.

## <a name="see-also"></a>Consulte Também
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)


