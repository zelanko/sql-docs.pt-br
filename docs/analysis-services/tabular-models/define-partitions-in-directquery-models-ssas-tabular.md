---
title: Definir partições em modelos DirectQuery do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6de0417055adc506fc6d9940aa3fa349f59c658
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072273"
---
# <a name="define-partitions-in-directquery-models"></a>Definir partições em modelos DirectQuery
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Esta seção explica como as partições são usadas em modelos DirectQuery. Para obter mais informações sobre partições em modelos tabulares, consulte [partições](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
> [!NOTE]  
>  Embora uma tabela possa ter várias partições, no modo DirectQuery, somente uma delas pode ser designada para uso na execução da consulta. O requisito de partição única se aplica a modelos DirectQuery em todos os níveis de compatibilidade.  
  
## <a name="using-partitions-in-directquery-mode"></a>Usando partições no modo DirectQuery  
 Para cada tabela, você deve especificar uma única partição para usar como a fonte de dados DirectQuery.  Se houver várias partições, quando você alternar o modelo para habilitar o modo DirectQuery, por padrão a primeira partição que foi criada na tabela será sinalizada como a partição DirectQuery. Você pode alterar isso posteriormente usando o Gerenciador de Partições no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Por que permitir apenas uma partição única no modo DirectQuery?  
  
 Em modelos de tabela (como em modelos OLAP), as partições de uma tabela são definidas através de consultas SQL. O desenvolvedor que cria a definição de partição é responsável por assegurar que não haja sobreposição de partições. O Analysis Services não verifica se os registros pertencem em uma ou várias partições.  
  
 As partições em um modelo de tabela armazenado em cache se comportam da mesma forma. Se você estiver usando um modelo na memória, enquanto o cache estiver sendo acessado, fórmulas DAX serão avaliadas para cada partição e os resultados serão combinados. Porém, quando um modelo de tabela usa o modo DirectQuery, é impossível avaliar várias partições, combinar os resultados e converter isso em uma instrução SQL a ser enviada ao repositório de dados relacional. Essa ação pode causar a perda inaceitável de desempenho e imprecisões em potencial, já que os resultados são agregados.  
  
 Portanto, para consultas respondidas no modo DirectQuery, o servidor usa uma única partição que foi marcada como a partição primária para acesso do DirectQuery, chamada de *partição DirectQuery*.  A consulta SQL especificada na definição dessa partição define o conjunto completo de dados que podem ser usados para responder a consultas no modo DirectQuery.  
  
 Se você não definir a partição explicitamente, o mecanismo simplesmente emitirá uma consulta SQL à fonte de dados relacional inteira, executará qualquer operação baseada em conjunto ditada pela fórmula DAX e retornará os resultados da consulta.  
  
  
## <a name="change-a-directquery-partition"></a>Alterar uma partição DirectQuery  
 Como apenas uma partição em uma tabela pode ser designada como a partição DirectQuery, por padrão, o Analysis Services usa a primeira partição criada na tabela. Durante a criação do projeto de modelo, você pode alterar a partição DirectQuery usando a caixa de diálogo Gerenciador de Partições no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para modelos implantados, você pode alterar a partição DirectQuery usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>Alterar a partição DirectQuery para um projeto de modelo de tabela  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], no designer de modelos, clique na tabela (guia) que contém a tabela particionada.  
  
2.  Clique no menu **Tabela** e clique em **Partições**.  
  
3.  No **Gerenciador de Partições**, a partição que é a partição atual Direct Query é indicada pelo prefixo **(DirectQuery)** no nome da partição.  
  
     Selecione outra partição na lista **Partições** e clique em **Definir como DirectQuery**. O botão **Definir como DirectQuery** não é habilitado quando a partição DirectQuery atual é selecionada e não fica visível quando o modelo não está habilitado no modo Direct Query.  
  
4.  Se necessário, altere as opções de processamento e clique em **OK**.  
  
#### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>Alterar a partição DirectQuery para um modelo de tabela implantado  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o banco de dados modelo no Pesquisador de Objetos.  
  
2.  Expanda o nó **Tabelas** , clique com o botão direito do mouse na tabela particionada e selecione **Partições**.  
  
     A partição que é designada para uso com o modo DirectQuery tem o prefixo (DirectQuery) no nome da partição.  
  
3.  Para alterar para uma partição diferente, clique no ícone da barra de ferramentas **Direct Query** para abrir a caixa de diálogo **Definir Partição DirectQuery** . O ícone da barra de ferramentas DirectQuery não está disponível em modelos não habilitados para Direct Query.  
  
4.  Escolha outra partição na lista suspensa **Nome da Partição** e altere opções de processamento na partição, caso seja necessário.  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>Partições em modelos armazenados em cache e em modelos DirectQuery  
 Quando você configura uma partição DirectQuery, deve especificar opções de processamento para a partição.  
  
 Há duas opções de processamento para a partição DirectQuery. Para definir essa propriedade, use o **Gerenciador de Partições** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e selecione a propriedade **Opção de Processamento** . A tabela a seguir lista os valores desta propriedade e descreve os efeitos de cada valor quando combinados com a propriedade DirectQueryUsage na cadeia de conexão:  
  
|Propriedades**Cadeia de Conexão** |Propriedade**Opção de Processamento** |Observações|  
|------------------------------------|------------------------------------|-----------|  
|DirectQuery|Nunca processar esta partição|Quando o modelo só estiver usando o DirectQuery, o processamento nunca será necessário.<br /><br /> Em modelos híbridos, você pode configurar a partição DirectQuery para nunca ser processada. Por exemplo, se você estiver operando em um conjunto de dados muito grande e não desejar adicionar os resultados completos ao cache, poderá especificar que a partição DirectQuery inclua a união de resultados para todas as outras partições na tabela e que nunca processe a união. As consultas destinadas à fonte relacional não serão afetadas e as consultas em dados armazenados em cache combinarão dados das outras partições|  
|DataView=Sample<br /><br /> Aplica-se a modelos tabulares usando modos de exibição de dados de exemplo|Permitir que a partição seja processada|Se o modelo estiver usando dados de exemplo, você poderá processar a tabela para retornar um conjunto de dados filtrado que fornece indicações visuais durante o design do modelo.|  
|DirectQueryUsage=InMemory With DirectQuery<br /><br /> Aplica-se a modelos de tabela 1100 ou 1103 em execução em uma combinação de modo na memória e DirectQuery|Permitir que a partição seja processada|Se o modelo estiver usando o modo híbrido, você deve usar a mesma partição para consultas na fonte de dados em memória e DirectQuery.|  
  
## <a name="see-also"></a>Confira também  
 [Partições](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
