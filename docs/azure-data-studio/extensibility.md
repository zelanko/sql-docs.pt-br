---
title: Como adicionar funcionalidade por meio de extensibilidade
titleSuffix: Azure Data Studio
description: Saiba mais sobre o modelo de extensibilidade e as principais áreas de extensibilidade para estender a funcionalidade do Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 20158894567c1452a8d605f5cec84354654c5e96
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959593"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>Introdução à extensibilidade do [!INCLUDE[name-sos](../includes/name-sos-short.md)]

O [!INCLUDE[name-sos](../includes/name-sos.md)] tem vários mecanismos de extensibilidade para personalizar a experiência do usuário e tornar essas personalizações disponíveis para toda a comunidade de usuários. A plataforma [!INCLUDE[name-sos](../includes/name-sos.md)] principal se baseia em Visual Studio Code, portanto, a maioria das APIs de extensibilidade do Visual Studio Code está disponível. Além disso, fornecemos pontos de extensibilidade adicionais para atividades específicas de gerenciamento de dados.

Alguns dos principais pontos de extensibilidade são:

- APIs de extensibilidade do Visual Studio Code
- Ferramentas de criação de extensão do Azure Data Studio
- Gerenciar contribuições do painel da guia Painéis
- Insights com experiências de Ações
- APIs de extensibilidade do Azure Data Studio
- APIs do Provedor de Dados personalizadas

## <a name="visual-studio-code-extensibility-apis"></a>APIs de extensibilidade do Visual Studio Code

Como a plataforma [!INCLUDE[name-sos](../includes/name-sos.md)] principal se baseia em Visual Studio Code, detalhes sobre as APIs de extensibilidade do Visual Studio Code são encontrados na documentação de [Criação de Extensão](https://code.visualstudio.com/docs/extensions/overview) e [API de Extensão](https://code.visualstudio.com/docs/extensionAPI/overview) no site do Visual Studio Code.

## <a name="manage-dashboard-tab-panel-contributions"></a>Gerenciar contribuições do painel da guia Painéis

Para obter detalhes, confira [Pontos de Contribuição](#contribution-points) e [Variáveis de Contexto](#context-variables).

## <a name="azure-data-studio-extensibility-apis"></a>APIs de extensibilidade do Azure Data Studio

Para obter detalhes, confira [APIs de Extensibilidade](extensibility-apis.md).


## <a name="contribution-points"></a>Pontos de contribuição

Esta seção aborda os vários pontos de contribuição definidos no manifesto de extensão package.json.

O IntelliSense tem suporte no azuredatastudio.

## <a name="contributes-dashboard"></a>Painel Contribui

Guia Contribuir, contêiner, widget insight para o painel.

![Painel](media/extensibility/dashboard-page.png)

`dashboard.tabs`

O Dashboard.tabs cria as seções de guia dentro da página do painel. Ele espera um objeto ou uma matriz de objetos.  

```json
"dashboard.tabs": [
{
    "id": "test-tab1",
    "title": "Test 1",
    "description": "The test 1 displays a list of widgets.",
    "when": "connectionProvider == 'MSSQL' && !mssql:iscloud",
    "alwaysShow": true,
    "container": {
        ...
    }
}
]
```

`dashboard.containers`

Em vez de especificar o contêiner de painel embutido (dentro do dashboard.tab). Você pode registrar contêineres usando dashboard.containers. Ele aceita um objeto ou uma matriz do objeto.

```json
"dashboard.containers": [
{
    "id": "innerTab1",
    "container": {
        ...
    }
},
{
    "id": "innerTab2",
    "container": {
       ...
    }
}
]
```

Para consultar o contêiner registrado, especifique a ID do contêiner

```json
"dashboard.tabs": [
{
    ...
    "container": {
        "innerTab1": {             
        }
    }
}
]

```

`dashboard.insights`

Você pode registrar insights usando dashboard.insights. Isso é semelhante ao [Tutorial: Criar um widget de insight personalizado](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)

```json
"dashboard.insights": {
"id": "my-widget"
"type": {
    "count": {
        "dataDirection": "vertical",
        "dataType": "number",
        "legendPosition": "none",
           "labelFirstColumn": false,
        "columnsAsLabels": false
       }
   },
   "queryFile": "{your file folder}/activeSession.sql"
}
```


### <a name="dashboard-container-types"></a>Tipos de contêiner de painéis

No momento, há quatro tipos de contêineres com suporte:

1. `widgets-container`

    ![Contêiner de widgets](media/extensibility/widgets-container.png)

    A lista de widgets que será exibida no contêiner. É um layout de fluxo. Ele aceita a lista de widgets.

    ```json
    "container": {
        "widgets-container": [
        {
            "widget": {
                "query-data-store-db-insight": {
                }
            }
        },
        {
            "widget": {
                "explorer-widget": {
                }
            }
        }
      ]
    }
    ```

2. `webview-container`

    ![contêiner de webview](media/extensibility/webview-container.png)

    A webview será exibida em todo o contêiner. Ela espera que a ID da webview seja igual à ID da guia

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![contêiner de grade](media/extensibility/grid-container.png)

   A lista de widgets ou webviews que serão exibidos no layout de grade

    ```json
    "container": {
        "grid-container": [
        {
            "name": "widget 1",
            "widget": {
                "explorer-widget": {
                }
            },
            "row":0,
            "col":0
        },
        {
            "name": "widget 2",
            "widget": {
                "tasks-widget": {
                    "backup", 
                    "restore",
                    "configureDashboard",
                    "newQuery"
                }
            },
            "row":0,
            "col":1
        },
        {
            "name": "Webview 1",
            "webview": {
                "id": "google"
            },
            "row":1,
            "col":0,
            "colspan":2
        },
        {
            "name": "widget 3",
            "widget": {
                "explorer-widget": {}
            },
            "row":0,
            "col":3,
            "rowspan":2
        },
    ]
    ```

4.  `nav-section`

    ![seção de navegação](media/extensibility/nav-section.png)

    A seção de navegação será exibida no contêiner

    ```json
    "container": {
        "nav-section": [
            {
                "id": "innerTab1",
                "title": "inner-tab1",
                "icon": {
                    "light": "./icons/tab1Icon.svg",
                    "dark": "./icons/tab1Icon_dark.svg"
                }
                "container": {
                    ...
                }
            },
            {
                "id": "innerTab2",
                "title": "inner-tab2",
                "icon": {
                    "light": "./icons/tab2Icon.svg",
                    "dark": "./icons/tab2Icon_dark.svg"
                }
                "container": {
                    ...
                }
            }
        ]
    }
    ```



## <a name="context-variables"></a>Variáveis de contexto

Para obter informações gerais sobre o contexto no Visual Studio Code e depois no Azure Data Studio, confira [Extensibilidade](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example).

No Azure Data Studio, temos um contexto específico em relação às conexões de banco de dados disponíveis para extensões.

### <a name="dashboard"></a>Painel

No painel, fornecemos as seguintes variáveis de contexto:

|variável de contexto| descrição|
|:---|:---|
|`connectionProvider` | Uma cadeia de caracteres do identificador para o provedor da conexão atual. Ex. `connectionProvider == 'MSSQL'`.|
|`serverName`|Uma cadeia de caracteres do nome do servidor da conexão atual. Ex. `serverName == 'localhost'`.|
|`databaseName` | Uma cadeia de caracteres do nome do banco de dados da conexão atual. Ex. `databaseName == 'master'`.|
|`connection` | O objeto de perfil de conexão completo para a conexão atual (IConnectionProfile)|
|`dashboardContext` | Uma cadeia de caracteres do contexto da página do painel está atualmente ativada. Ou 'database' ou 'server'. Ex. `dashboardContext == 'database'`|
