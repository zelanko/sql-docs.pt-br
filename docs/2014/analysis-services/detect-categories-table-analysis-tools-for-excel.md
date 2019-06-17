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
ms.openlocfilehash: 06c466eb5e3275818a710a9f9d90c705ed93c957
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081862"
---
# <a name="detect-categories-table-analysis-tools-for-excel"></a>Detectar Categorias (Ferramentas de Análise de Tabela para Excel)
  ![Botão de categorias de detectar na faixa de opções](media/tat-detectcat.gif "botão detectar categorias na faixa de opções")  
  
 O **detectar categorias** ferramenta encontra automaticamente as linhas em uma tabela que têm características semelhantes.  
  
 Quando a ferramenta termina, cria um relatório que lista as categorias encontradas, junto com suas características de distinção. Por padrão, ela adiciona uma nova coluna à tabela de dados que contém a categoria proposta para cada linha de dados. Assim, você pode examinar as categorias e renomeá-las.  
  
## <a name="using-the-detect-categories-tool"></a>Usando a ferramenta Detectar Categorias  
  
1.  Abra uma tabela do Excel.  
  
2.  Clique em **detectar categorias**.  
  
3.  Especifique as colunas a serem usadas na análise. Você pode desmarcar colunas que tenham valores discretos, como nomes pessoais ou IDs de registro, porque essas colunas talvez não sejam úteis para análise.  
  
4.  Se desejar, especifique o número máximo de categorias a serem criadas. Por padrão, a ferramenta cria automaticamente tantas categorias quantas encontra.  
  
5.  Clique em **Executar**.  
  
6.  A ferramenta cria uma nova planilha, denominada Relatório de Categorias, que contém a lista de categorias e suas características.  
  
 Para obter mais informações sobre como especificar opções para a ferramenta, consulte [detectar uma caixa de diálogo categorias (ferramentas de análise de tabela para Excel)](detect-categories-table-analysis-tools-for-excel.md).  
  
## <a name="understanding-the-categories-report"></a>Compreendendo o Relatório de Categorias  
 O **relatório de categorias** contém duas tabelas, **lista de categorias** e **características da categoria**e um **perfis de categoria** gráfico.  
  
### <a name="category-list"></a>Lista de categorias  
 A primeira tabela lista as categorias encontradas. O **contagem de linhas** coluna indica quantas linhas de dados que foram atribuídas a cada categoria.  
  
 O modelo cria nomes temporários para cada categoria, mas você pode renomear as categorias como quiser. Por exemplo, no exemplo a seguir, a primeira categoria foi renomeada **baixa renda**, já que foi o principal atributo do cluster.  
  
 ![relatório criado pela ferramenta detectar categorias](media/dm13-tat-detectcat-report1.gif "relatório criado pela ferramenta detectar categorias")  
  
 Assim que você digita o novo rótulo, a alteração é propagada para todos os outros gráficos, bem como para a lista de categorias adicionada à planilha de dados de origem.  
  
### <a name="category-characteristics"></a>Características da Categoria  
 A segunda tabela, **características da categoria**, mostra detalhes sobre a criação de cada categoria. Clique o **filtro** botão na parte superior das **categoria** coluna para ver o foco em uma ou algumas categorias.  
  
 ![relatório criado pela ferramenta detectar categorias](media/dm13-tat-detectcat-report2.gif "relatório criado pela ferramenta detectar categorias")  
  
 O sombreamento na coluna, **importância relativa**, indica que a combinação de atributo e valor é como fatores de distinção importante. Quanto maior a barra, maior a probabilidade de que esse atributo represente fortemente essa categoria.  
  
### <a name="categories-profile-chart"></a>Gráfico Perfil de Categorias  
 O gráfico final na **relatório de categorias** planilha **perfis de categoria**, é interativo **gráfico dinâmico** que você pode usar para reorganizar e ocultar campos, filtrar valores e personalizar a aparência do gráfico.  
  
 Excel 2013 agora oferece **estilos de gráfico** e **elementos do gráfico** controles na superfície de design que facilitam a aprimorar o design do gráfico.  
  
 ![relatório criado pela ferramenta detectar categorias](media/dm13-tat-detectcat-report3.gif "relatório criado pela ferramenta detectar categorias")  
  
## <a name="requirements"></a>Requisitos  
 O **detectar categorias** ferramenta não tem nenhum requisito para a quantidade ou o tipo de dados.  
  
> [!NOTE]  
>  Quando você usa o **detectar categorias** ferramenta, ele cria uma nova coluna, categoria, na tabela de dados original. Se você deixar essa coluna na tabela de dados e, em seguida, executar operações subsequentes de mineração de dados, a presença dessa coluna poderá influenciar os resultados. Para assegurar que isso não afete outras operações, faça uma cópia da tabela de dados sem a coluna Categoria, antes de usar outras ferramentas de mineração de dados.  
  
## <a name="related-tools"></a>Ferramentas relacionadas  
 Quando o **detectar categorias** ferramenta analisa os dados, ele cria uma estrutura de mineração de dados e o modelo de mineração de dados usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de Clustering.  
  
 Depois de criar um modelo de mineração de dados usando o **analisar os influenciadores principais** ferramenta, você pode usar o cliente de mineração de dados para Excel para procurar o modelo e explorar relações com mais detalhes. O Cliente de Mineração de Dados para Excel é um suplemento separado que fornece funções de mineração de dados mais avançadas. Para obter informações, consulte [procurando modelos no Excel &#40;SQL Server Data Mining Add-ins&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md).  
  
 Para obter mais informações sobre como usar os dados de recursos no cliente de mineração de dados de modelagem para Excel, consulte [criando um modelo de mineração de dados](creating-a-data-mining-model.md).  
  
 Para obter mais informações sobre o algoritmo usado pelas **detectar categorias** ferramenta, consulte o tópico "Algoritmo Microsoft Clustering" nos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
