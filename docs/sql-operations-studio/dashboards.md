---
title: Acessar rapidamente informações e tarefas comuns no Studio de operações do SQL (visualização) | Microsoft Docs
description: Saiba mais sobre como exibir widgets criteriosos no Studio de operações do SQL (visualização).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 8ed47935a863a14d68385c540ce68d0e75e99799
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34235576"
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>Painéis no [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Para exibir um painel, com o botão direito um servidor ou banco de dados e selecione **gerenciar**.

![Painel de exemplo](media/dashboards/sample-dashboard.png)

**Propriedades do servidor** contém as propriedades do servidor, incluindo a versão, edição, nome do computador e versão do sistema operacional.

**Tarefas** contém tarefas commons como restauração e nova consulta.

**Bancos de dados de pesquisa** pesquisar facilmente bancos de dados existentes armazenados no servidor, incluindo as tabelas.

**Status de backup** pesquisar facilmente o status do backup de bancos de dados existentes.

## <a name="configuring-insight-widgets"></a>Configurando o Insight Widgets
É altamente recomendável que você siga o tutorial para configurar seu painel, que pode ser encontrado [aqui](tutorial-build-custom-insight-sql-server.md).

Além disso, certifique-se de fazer check-out de [instruções sobre como configurar os widgets insight]().

Depois de seguir este tutorial, continue lendo para saber mais sobre widgets específicas que não são abordados no tutorial.

## <a name="insight-detail"></a>Detalhes de informações
O submenu de detalhes de informações fornece informações mais detalhadas para um widget de informações relacionadas. 
- Um widget Insight renderiza uma exibição de resumo de um instantâneo com a contagem de linha, gráfico etc. 
- O submenu de detalhes do Insight fornece detalhes "fazer uma busca de", listando os insights mais profundos de dados para cada item listado no widget de análise de alto nível. 
  - O conteúdo de submenu detalhes é definido com uma consulta SQL separada para a consulta do widget principal. 

Não há nenhum requisito de conjunto para uma consulta de detalhes de análise, mas o layout é o padrão.
- A metade superior do modo de exibição é sempre um modo de exibição "Resumo" 2 colunas. Quais colunas usar são definidas pelas propriedades de "rótulo" e "value" da configuração de JSON
- Quando você clicar em uma linha na tabela de resumo, a parte inferior metade do submenu listará o conjunto completo de informações de coluna para aquela linha.

### <a name="insight-detail-configuration-in-packagejson"></a>Configuração de detalhe de informações em Package. JSON

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
|detalhes|objeto JSON|||propriedade obrigatória para definir as definições de detalhe de informações dentro de sua estrutura||
|queryFile|cadeia de caracteres|||o caminho do arquivo de consulta do insight detalhes sql e o nome do arquivo relativo ao local de Package. JSON||
|Rótulo|objeto JSON|||propriedade obrigatória para definir cada item de linha na exibição de lista de resumo|no futuro, o nome dessa propriedade para alterar como 'summaryList'|
|Ícone|cadeia de caracteres|||Indique o nome do ícone para renderização para cada item de exibição de lista de resumo.|será documentada à lista (tbd) dos ícones com suporte|
|column|cadeia de caracteres|||Indique o nome da primeira coluna na exibição de lista de resumo do conjunto de resultados de consulta|no futuro o nome dessa propriedade será alterado para nome mais intuitivo|
|value|cadeia de caracteres|||Indique o nome da segunda coluna na exibição de lista de resumo do conjunto de resultados de consulta. O valor dessa coluna é usado para verificar condições e definir a cor de ponto de cor do cada lista de resumo exibir itens|no futuro o nome dessa propriedade será alterado para algo mais intuitiva|
|condição|objeto JSON|||Define a verificação de condição de valor da coluna e determinar a cor de cada item de exibição de lista de resumo||
|Se|cadeia de caracteres|sempre, é igual a, notEquals, greaterThan, lessThan, greaterThanOrEqauls, lessThanOrEquals||operador de seleção da condição|no futuro o nome da propriedade será alterado para operador|
|equals|cadeia de caracteres|||valor de verificação de condição|no futuro o nome da propriedade será alterado para 'value'|

## <a name="insight-actions"></a>Ações de análise
Com um widget insight e detalhes de análise, você pode facilmente encontrar um plano de ação para solucionar um problema ou gerenciar. Por exemplo, você será pensar em execução de DBCC CHECKDB, logs de erros de leitura ou restaurar o banco de dados quando um banco de dados está em uma recuperação pendente. Ou pode ser qualquer uma das ações que você deseja executar.

Usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]da configuração de ações de análise, você pode mapear um ações internas, como restaurar ou Traga sua própria ação definida com um script sql.

> Configuração de ações personalizadas usando o script sql está em desenvolvimento e ainda não está disponível na compilação de visualização particular.

## <a name="sample-insight-action-definition"></a>Definição de ação de análise de exemplo

```"actions"{}``` define uma ação de análise. Ação pode ser definida em um escopo específico, como ```"server"```, ```"database"``` e assim por diante e [!INCLUDE[name-sos](../includes/name-sos-short.md)] passa as informações de contexto de conexão atual para a ação. 

Por exemplo, quando a ação de restauração é iniciada do banco de dados de WideWorldImporters ```"database": "${Database}"``` definição indica para passar ```Database``` valor da coluna no seu resultado de consulta para a ação de restauração. Ação de restauração inicia para o banco de dados. ```"types"``` é uma matriz json e várias ações podem ser listadas na matriz. É basicamente um menu de contexto na caixa de diálogo de detalhes de informações que o usuário pode clicar em e executar a ação. 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] visualização 0.17.1 habilitou "backup", "restore", "nova consulta" e "novo banco de dados" como tipos de ação.

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
