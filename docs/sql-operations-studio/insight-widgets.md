---
title: "Usar widgets Insight para monitorar servidores e bancos de dados no Studio de operações do SQL (visualização) | Microsoft Docs"
description: "Saiba mais sobre widgets insight no Studio de operações do SQL (visualização)."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d810e0b5ed89b93ac3d56a12758285fbd297092b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>Gerenciar servidores e bancos de dados com os widgets de informações de[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Widgets Insight levar as consultas Transact-SQL (T-SQL) que você pode usar para monitorar servidores e bancos de dados e as transforma em visualizações criteriosos. 

Insights são personalizáveis de gráficos que você adicionar ao servidor e painéis de monitoramento de banco de dados. Exibir informações de um instantâneo de servidores e bancos de dados, em seguida, faça drill para obter mais detalhes e iniciar ações de gerenciamento que você definir. 

Você pode criar o incríveis banco de dados e servidor de gerenciamento painéis semelhantes ao exemplo a seguir:

![Painel de banco de dados](media/insight-widgets/database-dashboard.png)


Para entrar e iniciar a criação de tipos diferentes de widgets de informações, confira os tutoriais a seguir:

- [Criar um widget de informações personalizadas](tutorial-build-custom-insight-sql-server.md)
- *Habilitar widgets internos insight*
   - [Habilitar o monitoramento de análise de desempenho](tutorial-qds-sql-server.md)
   - [Habilitar a análise de uso de espaço de tabela](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>Consultas SQL 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]tenta evitar introduzir ainda outro usuário de idioma ou pesadas interface para que ele tentará usar o máximo possível de T-SQL com a configuração mínima do JSON. Configurando widgets insight com T-SQL aproveita o inúmeros número de fontes de consultas T-SQL úteis que podem ser convertidas em widgets criteriosos existentes.

Widgets Insight são compostas de uma ou duas consultas do T-SQL:
* *Consulta de widget Insight* é obrigatório e é a consulta que retorna os dados que aparecem no widget.
* *Consulta de detalhes do Insight* é necessário apenas se você estiver criando uma página de detalhes de análise.

Uma consulta de widget insight define um conjunto de dados que processa uma contagem ou um gráfico. Consulta de detalhes de informações é usada para listar informações de detalhe de informações relevantes em um formato tabular no painel de detalhes de análise. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]executa consultas de widget insight e mapeia o conjunto de resultados de consulta ao conjunto de dados do gráfico e é processada. Quando os usuários abrem os detalhes da perspectiva, ele executa a consulta de detalhes do insight e imprime o resultado em uma exibição da grade a caixa de diálogo.

A ideia básica é gravar uma consulta T-SQL de uma maneira para que ele pode ser usado como um conjunto de dados de uma contagem, o gráfico e o widget de gráfico. 

## <a name="summary"></a>Resumo

A consulta T-SQL e seu conjunto de resultados determinam o comportamento de widget de análise. Escrever uma consulta para um tipo de gráfico ou um tipo de gráfico à direita para a consulta existente de mapeamento é a consideração importante para criar um widget de análise efetiva.



## <a name="additional-resources"></a>Recursos adicionais
- [Editor de consultas](tutorial-sql-editor.md)

