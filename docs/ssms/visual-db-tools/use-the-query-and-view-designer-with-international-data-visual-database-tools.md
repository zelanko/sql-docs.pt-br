---
title: Usar o Designer de Consulta e Exibição com os dados internacionais   Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Visual Database Tools [SQL Server], international data
- queries [SQL Server], international data
- languages [SQL Server], Query and View Designer
- international considerations [SQL Server], Query and View Designer
- Criteria pane
- View Designer, international data
- Query Designer [SQL Server], international data
- localized information in Query and View Designer [SQL Server]
- global considerations [SQL Server], Query and View Designer
- SQL pane [Visual Database Tools]
- multiple language support [SQL Server], Query and View Designer
ms.assetid: 4b51c56f-f902-4e72-b919-e36127369b63
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 19598f44624629850f1116d74b25f4f9ab488c67
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669954"
---
# <a name="use-the-query-and-view-designer-with-international-data-visual-database-tools"></a>Usar o Designer de Consulta e Exibição com dados internacionais (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode usar o [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) com dados de qualquer idioma e em qualquer versão do sistema operacional Windows. As diretrizes a seguir mostram as diferenças existentes e fornecem informações sobre como gerenciar dados em aplicativos internacionais.  
  
## <a name="localized-information-in-the-criteria-and-sql-panes"></a>Informações localizadas nos painéis Critérios e SQL  
Ao usar o painel Critérios para criar uma consulta, você poderá inserir informações no formato que corresponda às Configurações regionais do Windows do seu computador. Por exemplo, ao pesquisar dados, você poderá inserir os dados nas colunas de critérios, usando qualquer formato que esteja acostumado a usar, com as seguintes exceções:  
  
-   Não há suporte para formatos de dados longos.  
  
-   Símbolos de moeda não devem ser inseridos no painel Critérios.  
  
-   Símbolos de moeda não são exibidos no painel Resultados.  
  
    > [!NOTE]  
    > No painel Resultados, de fato é possível inserir o símbolo de moeda correspondente às Configurações regionais do Windows do seu computador, mas o símbolo é removido e não é exibido no painel Resultados.  
  
-   O unário de subtração aparece sempre do lado esquerdo (por exemplo, -1) independentemente das opções de configurações regionais.  
  
Por outro lado, dados e palavras-chave do painel SQL devem estar sempre em formato ANSI (EUA). Por exemplo, à medida que o Designer de Consulta e Exibição cria uma consulta, ele insere o formulário ANSI de todas as palavras-chave SQL como SELECT e FROM. Para adicionar elementos à instrução no painel SQL, certifique-se de usar o formulário padrão ANSI para os elementos.  
  
Quando dados são inseridos usando formato específico de local no painel Critérios, o Designer de Consulta e Exibição traduz  automaticamente esses dados para o formato ANSI no painel SQL. Por exemplo, se as Configurações regionais estiverem definidas como padrão alemão, você poderá inserir dados no painel Critérios em formato "31.12.96". Porém, a data aparecerá no painel SQL em formato ANSI de data e hora como `{ ts '1996-12-31 00:00:00' }.` . Se você inserir dados diretamente no painel SQL, será necessário inseri-los em formato ANSI.  
  
## <a name="sort-order"></a>Sort Order  
A ordem de classificação dos dados de uma consulta é determinada pelo banco de dados. As opções definidas na caixa de diálogo Configurações regionais do Windows não afetam a ordem de classificação das consultas. Em qualquer consulta particular, porém, você pode solicitar que as linhas sejam retornadas em determinada ordem.  
  
## <a name="using-double-byte-characters"></a>Usando caracteres de dois bytes  
É possível inserir caracteres DBCS de literais e de nomes de objeto de banco de dados, como nomes de tabelas e de exibições, ou aliases. Você também poderá usar caracteres DBCS para nomes de parâmetro e caracteres de marcador de parâmetro. Porém, não será possível usar caracteres DBCS em elementos de linguagem SQL, como nomes de função ou palavras-chave de SQL.  
  
## <a name="see-also"></a>Consulte Também  
[Tópicos de instruções de como criar consultas e exibições (Ferramentas de Banco de Dados Visual)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
