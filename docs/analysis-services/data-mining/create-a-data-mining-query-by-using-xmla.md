---
title: "Criar uma consulta de mineração de dados usando o XMLA | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: content queries [DMX]
ms.assetid: 8f6b6008-006c-4792-9bd1-64c30dc3fd41
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fa60ad8ee91839e04c424c5fe2d23723e495bbd4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-data-mining-query-by-using-xmla"></a>Criar uma consulta de mineração de dados usando XMLA
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Você pode criar várias consultas em objetos de mineração de dados usando o AMO, DMX ou XML/a.  
  
 O XML é usado para comunicação entre o servidor Analysis Services e todos os clientes. Assim, embora geralmente seja muito mais fácil criar consultas de conteúdo usando DMX, você pode escrever consultas usando as instruções DISCOVER e COMMAND em XML/A, com um cliente que dê suporte a protocolo SOAP ou criando uma consulta XML/A no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Este tópico explica como usar os modelos XML/A disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar uma consulta de conteúdo de modelo referente a um modelo de mineração armazenado no servidor atual.  
  
## <a name="querying-data-mining-schema-rowsets-by-using-xmla"></a>Consultando conjuntos de linhas de esquema de mineração de dados usando XML/A  
  
#### <a name="to-open-an-xmla-template"></a>Para abrir um modelo XML/A  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Exibir** , clique em **Gerenciador de Modelos**.  
  
2.  Clique no ícone de cubo para abrir a lista de modelos do Analysis Services.  
  
3.  Na lista de categorias de modelo, expanda **XMLA**, **Conjuntos de Linhas do Esquema**e clique duas vezes em **Descobrir Conjuntos de Linhas do Esquema** para abrir o modelo no editor de código apropriado.  
  
4.  Na caixa de diálogo **Conectar ao Analysis Services** , preencha as informações de conexão e clique em **Conectar**. Uma nova janela do editor de consulta é aberta, populada com o modelo **Descobrir Conjuntos de Linhas do Esquema** .  
  
#### <a name="to-discover-column-names-from-the-mining-model-content-schema-rowset"></a>Para descobrir nomes de coluna do conjunto de linhas de esquema MINING MODEL CONTENT  
  
1.  Com o modelo **Descobrir Conjuntos de Linhas do Esquema** aberto, clique em **Executar**.  
  
     Uma lista dos conjuntos de linha de esquema é retornada no painel **Resultados** que contém os nomes de todos os conjuntos de linhas disponíveis na instância atual.  
  
2.  No **consulta** painel, coloque o cursor depois  **\<lista de restrições >** e pressione ENTER para adicionar uma nova linha.  
  
3.  Posicione o cursor na linha em branco e digite  **\<SchemaName > DMSCHEMA_MINING_MODEL_CONTENT\</SchemaName >**  
  
     A seção completa de restrições deverá ser parecida com esta:  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<SchemaName>DMSCHEMA_MINING_MODEL_CONTENT</SchemaName>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
4.  Clique em **Executar**.  
  
     O painel **Resultados** mostra uma lista de nomes de colunas do conjunto de linhas do esquema especificado.  
  
#### <a name="to-create-a-content-query-using-the-mining-model-content-schema-rowset"></a>Para criar uma consulta de conteúdo usando o conjunto de linhas do esquema de MINING MODEL CONTENT  
  
1.  No modelo **Descobrir Conjuntos de Linhas do Esquema** , altere o tipo de solicitação substituindo o texto dentro das marcas de tipo de solicitação.  
  
     Substitua esta linha:  
  
     `<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>`  
  
     pela seguinte linha:  
  
     **\<RequestType > DMSCHEMA_MINING_MODEL_CONTENT\</RequestType >**  
  
2.  Altere a lista de restrições para especificar um modelo de mineração pelo nome, adicionando uma nova condição às listas de restrições.  
  
3.  No modelo, coloque o cursor depois de `<Restriction List>` e pressione a ENTER para adicionar uma nova linha.  
  
4.  Coloque o cursor na linha em branco e digite **<MODEL_NAME>Nome do meu domínio</MODEL_NAME>**  
  
     A seção completa de restrições deverá ser parecida com esta:  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<MODEL_NAME>My model name</MODEL_NAME>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
5.  Clique em **Executar**.  
  
     O painel Resultados exibe a definição de esquema, junto com os valores para o modelo especificado.  
  
## <a name="see-also"></a>Consulte Também  
 [Conteúdo do modelo de mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Conjuntos de linhas de esquema de mineração de dados](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
