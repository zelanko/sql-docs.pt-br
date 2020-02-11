---
title: Usando o detalhamento em dados de estrutura (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a693979c-0564-4d6d-b35d-cbbc8f350469
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 68d5d29a4aed7380bd7a53c65d140aac24912392
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62745537"
---
# <a name="using-drillthrough-on-structure-data-basic-data-mining-tutorial"></a>Usando o detalhamento em dados de estrutura (Tutorial de mineração de dados básico)
  Como parte de sua campanha publicitária, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] o está enviando um mensageiro para clientes potenciais na era demográfica de 34-40. O departamento de marketing decidiu que também gostaria de enviar a mala direta aos clientes que compraram bicicletas da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] há mais de cinco anos. Nesta lição, você identificará clientes com bicicletas mais antigas e irá recuperar suas informações de contato. Essas informações não estão incluídas no modelo, mas na estrutura. Para recuperar as informações de contato, primeiro você terá de garantir que o detalhamento esteja habilitado para a estrutura para depois usá-lo para revelar os nomes e os endereços dos clientes-alvo.  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>Como habilitar o detalhamento em um modelo de mineração  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], na guia **modelos de mineração** do designer de mineração de dados, clique com o botão direito do mouse no modelo de **TM_Decision_Tree** e selecione **Propriedades**.  
  
2.  Nas janelas Propriedades , clique em **AllowDrillthrough**e selecione **True**.  
  
3.  Na guia Modelos de Mineração , clique com o botão direito do mouse no modelo e selecione **Modelo de Processo**.  
  
 Para obter mais informações, consulte [consultas de detalhamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>Para exibir dados de detalhamento de um modelo de mineração  
  
1.  No Designer de Mineração de Dados, clique na guia **Visualizador do Modelo de Mineração** .  
  
2.  Selecione o modelo de **TM_Decision_Tree** na lista **modelo de mineração** .  
  
3.  Altere o valor de plano `1`de **fundo** para. Assim, você mostra apenas a parte do modelo que está relacionada ao cliente que comprou bicicletas.  
  
4.  Selecione o Visualizador de Árvores da Microsoft na lista **Visualizador** . Isso forçará o visualizador a atualizar com as novas condições de filtro. Em seguida, localize o nó **idade >= 34 e <41** e clique com o botão direito do mouse no nó.  
  
5.  Selecione **Detalhar**e selecione **Colunas do Modelo e da Estrutura** para abrir a janela **Detalhar** .  
  
6.  Navegue até a coluna **Estrutura.Data da Primeira Compra** para exibir as datas de compra das bicicletas mais antigas.  
  
7.  Para copiar os dados para a Área de Transferência, clique com o botão direito do mouse na tabela e selecione **Copiar Tudo**.  
  
 Parabéns, você concluiu o tutorial de mineração de dados básico. Agora que você já está se sentindo confortável em usar as ferramentas de mineração de dados, recomendamos que conclua também o Tutorial de mineração de dados intermediário, que demonstra como criar modelos para previsão, análise de cesta básica e clustering de sequências.  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Criando previsões &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma consulta de previsão usando o construtor de consultas de previsão](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
