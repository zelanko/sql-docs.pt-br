---
title: Painel de design (exibição de previsão do modelo de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.prediction.design.f1
ms.assetid: 17f24c8d-43cd-4f4d-83b3-a41ee8fbe8e8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 743eefc1bd13dec480ec8773a8602773ded7ca6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081847"
---
# <a name="design-pane-mining-model-prediction-view"></a>Painel Design (Exibição da Previsão do Modelo de Mineração)
  O painel **Design** contém o Construtor de Consulta de Previsão, que você pode utilizar para criar previsões de mineração de dados. É possível projetar consultas de previsão que usam tabelas de dados de entrada de uma exibição da fonte de dados, gerar previsões em massa ou criar consultas de previsão singleton, que permitem fornecer valores individuais.  
  
 Para executar a consulta e exibir os resultados, alterne para a exibição de resultados de consulta.  
  
 A visualização da **Consulta** mostra a consulta de DMX (extensões DMX) criada pelo Construtor de Consultas de Previsão. Se você estiver familiarizado com DMX, poderá personalizar esta consulta.  
  
> [!NOTE]  
>  Se você fizer alguma alteração manual na consulta, suas alterações serão perdidas ao voltar para a exibição Design. Se desejar salvar a consulta DMX, copie-a na área de transferência do Windows e cole-a em um arquivo de texto.  
  
 **Para obter mais informações:** [consultas de mineração de dados](data-mining/data-mining-queries.md)  
  
## <a name="options"></a>Opções  
 **Alternar para a exibição de resultado da consulta**  
 Clique para mudar entre os painéis **Design**, **Consulta**e **Resultado** . A consulta é executada ao alternar para o painel **Resultado** .  
  
 **Salvar o resultado da consulta**  
 Abre a caixa de diálogo **Salvar Resultado da Consulta de Mineração de Dados** .  
  
 **Consulta singleton**  
 Permite a criação de uma consulta singleton, na qual você pode fornecer valores diretamente para a consulta em vez de fornecer uma tabela como fonte de dados conhecidos. A tabela **Selecionar Tabela(s) de Entrada** será substituída por uma tabela **Entrada de Consultas Singleton** .  
  
 **Atualizar resultados de consulta**  
 Processa novamente a consulta de previsão. Isso está habilitado apenas no painel **Resultado** .  
  
 **Modelo de mineração**  
 Exibe o modelo de mineração selecionado no qual você deseja basear as previsões.  
  
 **Selecionar modelo**  
 Abre a caixa de diálogo **Selecionar Modelo de Mineração** .  
  
 **Selecionar Tabela(s) de Entrada**  
 Exibe as tabelas de entrada selecionadas que contêm dados conhecidos nos quais as previsões serão fundamentadas.  
  
 **Excluir tabela**  
 Exclui a tabela selecionada. Esse botão será desabilitado se uma tabela não tiver sido selecionada ou não existir.  
  
 **Selecionar Tabela de Casos**  
 Abre a caixa de diálogo **Selecionar Tabela** . Esse botão só será exibido se uma tabela da caixa não tiver sido selecionada.  
  
 **Selecionar Tabela Aninhada**  
 Abre a caixa de diálogo **Selecionar Tabela** . Esse botão só será exibido se uma tabela do casos tiver sido selecionada. Se a estrutura de mineração associada não contiver uma tabela aninhada, esse botão será desabilitado.  
  
 **Modificar Junção**  
 Abre a caixa de diálogo **Especificar Junção Aninhada** . Esse botão só será ativado se a tabela aninhada for selecionada.  
  
 **Entrada de Consultas Singleton**  
 Habilitado quando você seleciona o botão **Consulta Singleton** . Contém as seguintes colunas:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Coluna do Modelo de Mineração**|Lista as colunas de modelo de mineração contidas no modelo de mineração que for selecionado na tabela **Modelo de Mineração** .|  
|**Valor**|Selecione um valor da lista que contém cada estado possível da coluna de modelos de mineração selecionada.<br /><br /> Se a coluna for uma coluna de tabela aninhada, clicar na célula de valor abrirá a caixa de diálogo **Entrada de Tabela Aninhada** .|  
  
 **Origem**  
 Selecione a origem que contém o campo que você utilizará para a coluna. Você pode usar o modelo de mineração selecionado na tabela **Modelo de Mineração** , a tabela ou as tabelas selecionadas na tabela **Selecionar Tabela(s) de Entrada** , uma função de previsão ou uma expressão personalizada.  
  
 As colunas podem ser arrastadas das tabelas que contêm o modelo de mineração e as tabelas de entrada até a célula.  
  
 **Campo**  
 Selecione uma coluna na lista de colunas derivada da tabela de origem. Se você selecionou a opção **Função de Previsão** em **Origem**, ela conterá a função de previsão disponível para o modelo de mineração selecionado.  
  
 **Agrupar**  
 Use com a coluna **E/ou** para agrupar expressões. Por exemplo, `(expr1 Or expr2) And expr3`.  
  
 **E/ou**  
 Use para criar uma consulta lógica. Por exemplo, `(expr1 Or expr2) And expr3`.  
  
 **Critério/argumento**  
 Especifique uma condição ou expressão de usuário que se aplica à coluna. As colunas podem ser arrastadas das tabelas que contêm o modelo de mineração e as tabelas de entrada até a célula.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](/sql/dmx/data-mining-extensions-dmx-statements)   
 [Interfaces de consulta de mineração de dados](data-mining/data-mining-query-tools.md)   
 [Construtor de Consultas de &#40;de mineração de dados de previsão&#41;](prediction-query-builder-data-mining.md)  
  
  
