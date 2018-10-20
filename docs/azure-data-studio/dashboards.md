---
title: Acessar rapidamente informações e tarefas comuns no estúdio de dados do Azure | Microsoft Docs
description: Saiba mais sobre como exibir widgets criteriosos no estúdio de dados do Azure.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: b163d110353d07811f0feb991772c90053651659
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356189"
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>Painéis no [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Para exibir um painel, clique com botão direito um servidor ou banco de dados e selecione **gerenciar**.

![Painel de exemplo](media/dashboards/sample-dashboard.png)

**Propriedades do servidor** contém as propriedades do servidor, incluindo a versão, edição, nome do computador e versão do sistema operacional.

**Tarefas** contém tarefas commons como nova consulta e de restauração.

**Bancos de dados de pesquisa** pesquisar facilmente bancos de dados existentes armazenados no servidor, incluindo as tabelas.

**Status de backup** pesquisar facilmente o status do backup para bancos de dados existentes.

## <a name="configuring-insight-widgets"></a>Configurando os Widgets de Insights
É altamente recomendável que você siga o tutorial para configurar o painel, que pode ser encontrado [aqui](tutorial-build-custom-insight-sql-server.md).

Além disso, certifique-se de fazer check-out a [instruções sobre como configurar os widgets de Insights]().

Depois de seguir este tutorial, continue lendo para saber mais sobre widgets específicos que não são abordados no tutorial.

## <a name="insight-detail"></a>Detalhes de Insight
O submenu de detalhes de informações fornece informações mais detalhadas para um widget de informações relacionadas. 
- Um widget de Insight renderiza uma exibição de resumo de uma visão geral com contagem, linha, gráfico etc. 
- O submenu de detalhes de informações fornece detalhes "analisar", listando as informações mais aprofundadas de dados para cada item listado no widget de Insight de alto nível. 
  - O conteúdo do menu suspenso de detalhes é definido com uma consulta SQL separada para consulta do widget principal. 

Não há nenhum requisito de conjunto para uma consulta de detalhes do Insight, mas o layout é o padrão.
- A metade superior do modo de exibição é sempre um modo de exibição "Resumo" 2 colunas. Quais colunas usar são definidas pelas propriedades da configuração do JSON "label" e "value"
- Clicando em uma linha na tabela de resumo, a parte inferior metade do submenu listará o conjunto completo de informações de coluna para aquela linha.

### <a name="insight-detail-configuration-in-packagejson"></a>Configuração de detalhe de Insight em Package. JSON

Exemplo de configuração de submenu Insight detalhes
```json
"details": {
    "queryFile": "./relative_path_to_sqlfile_from_package_json_file.sql",
    "label": {
        "icon": "database",
        "column": "first_column_name_for_summary_list_view",
        "state": [
            {
                "condition": {
                    "if": "equals",
                    "equals": "0"
                },
                "color": "red"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "1"
                },
                "color": "orange"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "2"
                },
                "color": "green"
            }
        ]
    },
    "value": "second_column_and_condition_check_value_column_for_summary_list_view",
```
|propriedade|Tipo|value|Valor padrão|descrição|comment|
|:---|:---|:---|:---|:---|:---|
|detalhes|objeto JSON|||propriedade obrigatória para definir as definições de detalhes de informações dentro de sua estrutura||
|queryFile|cadeia de caracteres|||o caminho do arquivo de consulta do insight detalhes sql e o nome do arquivo relativo ao local do Package. JSON||
|Rótulo|objeto JSON|||propriedade obrigatória para definir cada item de linha na exibição de lista de resumo|no futuro, o nome dessa propriedade para alterar, como 'summaryList'|
|Ícone|cadeia de caracteres|||indica o nome do ícone para renderização para cada item de exibição de lista de resumo.|lista (tbd) dos ícones com suporte será documentada|
|column|cadeia de caracteres|||Indique o nome da primeira coluna na exibição de lista de resumo do conjunto de resultados de consulta|no futuro o nome dessa propriedade será alterado para um nome mais intuitivo|
|value|cadeia de caracteres|||Indique o nome da segunda coluna na exibição de lista de resumo do conjunto de resultados de consulta. O valor desta coluna é usado para verificar condições e definir a cor de ponto de cor do cada lista de resumo exibir itens|no futuro, o nome dessa propriedade será alterado para algo mais intuitiva|
|Condição|objeto JSON|||Define o valor da coluna a verificação de condição e determinar a cor para cada item de exibição de lista de resumo||
|if|cadeia de caracteres|sempre, equals, notEquals, greaterThan, lessThan, greaterThanOrEqauls, lessThanOrEquals||operador de seleção de condição|no futuro, o nome da propriedade será alterado para operador|
|equals|cadeia de caracteres|||valor de verificação de condição|no futuro o nome da propriedade será alterado para 'value'|

## <a name="insight-actions"></a>Ações de Insight
Com um widget do insight e detalhes de insight, é possível produzir facilmente um plano de ação para solucionar um problema ou gerenciar. Por exemplo, você será pensar em execução de DBCC CHECKDB, ler logs de erros ou restaurar o banco de dados quando um banco de dados está em uma recuperação pendente. Ou pode ser qualquer uma das ações que você deseja realizar.

Usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]da configuração de ações de Insight, você pode mapear um ações internas, como restaurar ou Traga sua própria ação definida com um script sql.

> Configuração de ações personalizadas usando o script sql está em desenvolvimento e ele ainda não está disponível na compilação de versão prévia privada.

## <a name="sample-insight-action-definition"></a>Exemplo de definição de ação de análise

```"actions"{}``` define uma ação de análise. Ação pode ser definida em um escopo específico, como ```"server"```, ```"database"``` e assim por diante e [!INCLUDE[name-sos](../includes/name-sos-short.md)] passa as informações de contexto de conexão atual para a ação. 

Por exemplo, quando a ação de restauração for iniciada para o banco de dados de WideWorldImporters ```"database": "${Database}"``` definição indica para passar ```Database``` valor da coluna em que o resultado da consulta para a ação de restauração. Em seguida, restaure o início da ação para o banco de dados. ```"types"``` é uma matriz json e várias ações podem ser listadas na matriz. Basicamente, torna-se um menu de contexto na caixa de diálogo de detalhes de informações que o usuário pode clicar e executar a ação. 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] visualização 0.17.1 habilitou "backup", "restauração", "nova consulta" e "novo banco de dados" como tipos de ação.

```json
"details": {
    "queryFile": "./sql/database_state_detail.sql",
    "label": {...},
    "value": "state",
    "actions": {
        "database": "${Database}",
        "types": ["restore"]
    }
}
```
