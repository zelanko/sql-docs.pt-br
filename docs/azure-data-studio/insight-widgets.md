---
title: Usar os widgets de Insights no estúdio de dados do Azure para monitorar servidores e bancos de dados
titleSuffix: Azure Data Studio
description: Saiba mais sobre os widgets de Insights no estúdio de dados do Azure
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
ms.openlocfilehash: c1ab90efa97878676b1adc2a62579527407d6ba6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959521"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>Gerenciar servidores e bancos de dados com os widgets de Insights em [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Widgets de Insights levar as consultas Transact-SQL (T-SQL) que você usa para monitorar os servidores e bancos de dados e as transforma em visualizações interessantes.

Insights são personalizáveis de gráficos que você adiciona ao servidor e painéis de monitoramento de banco de dados. Exibir informações de uma visão geral de seus servidores e bancos de dados, em seguida, analisar os detalhes mais e iniciar ações de gerenciamento que você definir.

Você pode compilar awesome banco de dados e servidor de gerenciamento painéis semelhantes ao exemplo a seguir:

![Painel de banco de dados](media/insight-widgets/database-dashboard.png)


Para entrar e iniciar a criação de diferentes tipos de widgets de Insights, confira os tutoriais a seguir:

- [Criar um widget de visão personalizada](tutorial-build-custom-insight-sql-server.md)
- *Habilitar widgets de Insights internos*
  - [Habilitar informações de monitoramento de desempenho](tutorial-qds-sql-server.md)
  - [Habilitar o insight de uso do espaço de tabela](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>Consultas SQL

[!INCLUDE[name-sos](../includes/name-sos-short.md)] tenta evitar introduzir ainda outro usuário de idioma ou com uso intenso de interface para que ele tenta usar o T-SQL tanto quanto possível com a configuração mínima do JSON. Configurar os widgets de Insights com o T-SQL aproveita o incontáveis número de fontes de consultas T-SQL úteis que podem ser ativadas em widgets criteriosos existentes.

Widgets de Insights são compostos de uma ou duas consultas do T-SQL:
* *Consulta de widget de Insight* é obrigatório e é a consulta que retorna os dados exibidos no widget.
* *Consulta de detalhes do Insight* é necessário apenas se você estiver criando uma página de detalhes de informações.

Uma consulta de widget insight define um conjunto de dados que processa uma contagem, gráfico ou gráfico. Consulta de detalhes de informações é usada para listar informações de detalhe de informações relevante em um formato tabular no painel de detalhes de informações. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] executa consultas de widget do insight e mapeia o conjunto de resultados de consulta ao conjunto de dados de um gráfico e renderiza-o. Quando os usuários abrem os detalhes de um insight, ele executa a consulta de detalhes do insight e imprime o resultado em uma exibição de grade, na caixa de diálogo.

A ideia básica é escrever uma consulta T-SQL de uma forma para que possa ser usado como um conjunto de dados de uma contagem, o gráfico e o widget de gráfico. 

## <a name="summary"></a>Resumo

A consulta T-SQL e seu conjunto de resultados determinam o comportamento de widget insight. Escrever uma consulta para um tipo de gráfico ou um tipo de gráfico à direita para a consulta existente de mapeamento é a principal consideração para criar um widget de insight em vigor.



## <a name="additional-resources"></a>Recursos adicionais
- [Editor de Consultas](tutorial-sql-editor.md)

