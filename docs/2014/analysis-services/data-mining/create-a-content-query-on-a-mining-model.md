---
title: Criar uma consulta de conteúdo em um modelo de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content queries [DMX]
ms.assetid: a0ce837a-89ed-46cf-9ce1-801ccb75fa04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d2e3607426ecbc51b1d04dfc97b12f83faf328b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085578"
---
# <a name="create-a-content-query-on-a-mining-model"></a>Criar uma consulta de conteúdo em um modelo de mineração
  Você pode consultar o conteúdo do modelo de mineração via programação usando AMO ou XML/A, mas é mais fácil criar consultas usando DMX. Também é possível criar consultas nos conjuntos de linhas de esquema de mineração de dados estabelecendo uma conexão com a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e criando uma consulta usando os DMVs fornecidos pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Os procedimentos a seguir demonstram como criar consultas em um modelo de mineração usando DMX e como consultar os conjuntos de linhas de esquema de mineração de dados.  
  
 Para obter um exemplo de como criar uma consulta semelhante usando XML/A, consulte [Criar uma consulta de mineração de dados usando XMLA](create-a-data-mining-query-by-using-xmla.md).  
  
## <a name="querying-data-mining-model-content-by-using-dmx"></a>Consultando o conteúdo do modelo de mineração de dados usando DMX  
  
#### <a name="to-create-a-dmx-model-content-query"></a>Para criar uma consulta ao conteúdo do modelo DMX  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Exibir** , clique em **Gerenciador de Modelos**.  
  
2.  No painel **Gerenciador de Modelos** , clique no ícone de cubo para alterar a lista e exibir modelos do Analysis Services.  
  
3.  Na lista de categorias de modelo, expanda **DMX**, expanda **Conteúdo do Modelo**e clique duas vezes em **Consulta de Conteúdo**.  
  
4.  Na caixa de diálogo **Conectar ao Analysis Services** , selecione a instância que contém o modelo de mineração que você deseja consultar e clique em **Conectar**.  
  
     O modelo **Consulta de Conteúdo** é aberto no editor de códigos apropriado. O painel de metadados lista os modelos que estão disponíveis no banco de dados atual. Para alterar o banco de dados, selecione outro banco de dados na lista **Bancos de Dados Disponíveis** .  
  
5.  Insira o nome de um modelo de mineração na linha, `FROM` [*\<modelo de mineração, nome, MyModel>*].`.CONTENT` Se o nome do modelo de mineração contiver espaços, coloque o nome entre parênteses.  
  
     Se não quiser digitar o nome, você poderá selecionar um modelo de mineração no **Pesquisador de Objetos** e arrastá-lo para o modelo.  
  
6.  Na linha, `SELECT` * \<selecione lista, lista de expr, \* *, digite os nomes das colunas no conjunto de linhas do esquema de conteúdo do modelo de mineração.  
  
     Para ver uma lista das colunas que podem ser retornadas em consultas ao conteúdo do modelo de mineração, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
7.  Se preferir, digite uma condição na cláusula WHERE do modelo para restringir as linhas retornadas a nós ou valores específicos.  
  
8.  Clique em **Executar**.  
  
## <a name="querying-the-data-mining-schema-rowsets"></a>Consultando os conjuntos de linhas de esquema de mineração de dados  
  
#### <a name="to-create-a-query-against-the-data-mining-schema-rowset"></a>Para criar uma consulta no conjunto de linhas do esquema de mineração de dados  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], na barra de ferramentas **Nova Consulta** , clique em **Consulta DMX do Analysis Services**ou em **Consulta MDX do Analysis Services**.  
  
2.  Na caixa de diálogo **Conectar ao Analysis Services** , selecione a instância que contém os objetos que você deseja consultar e clique em **Conectar**.  
  
     O modelo **Consulta de Conteúdo** é aberto no editor de códigos apropriado. O painel de metadados lista os objetos que estão disponíveis no banco de dados atual. Para alterar o banco de dados, selecione outro banco de dados na lista **Bancos de Dados Disponíveis** .  
  
3.  No editor de consultas, digite o seguinte:  
  
     `SELECT *`  
  
     `FROM $system.DMSCHEMA_MINING_MODEL_CONTENT`  
  
     `WHERE MODEL_NAME = '<model name>'`  
  
4.  Clique em **Executar**.  
  
     O painel Resultados exibe o conteúdo do modelo.  
  
    > [!NOTE]  
    >  Para ver uma lista de todos os conjuntos de linhas de esquema que você pode consultar na instância atual, use esta consulta: `SELECT * FROM $system.`DISCOVER_SCHEMA_ROWSETS. Para ver uma lista de conjuntos de linhas de esquema específicos de mineração de dados, consulte [Conjuntos de linhas de esquema de mineração de dados](../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conteúdo do modelo de mineração &#40;Analysis Services Mineração de dados&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Conjuntos de linhas de esquema de mineração de dados](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
  
