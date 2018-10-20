---
title: Estender a funcionalidade do estúdio de dados do Azure | Microsoft Docs
description: Saiba mais sobre como estender o estúdio de dados do Azure
ms.custom: tools|sos
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d218f80067c3dd5a03ced864b815c68aa84a582e
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460241"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>Guia de Introdução [!INCLUDE[name-sos](../includes/name-sos-short.md)] extensibilidade

[!INCLUDE[name-sos](../includes/name-sos.md)] tem vários mecanismos de extensibilidade para personalizar a experiência do usuário e tornar essas personalizações disponíveis para a comunidade de usuário inteiro. O núcleo [!INCLUDE[name-sos](../includes/name-sos.md)] plataforma baseia-se se o Visual Studio Code, portanto, a maioria das APIs de extensibilidade do Visual Studio Code está disponível. Além disso, fornecemos pontos de extensibilidade adicionais para atividades de gerenciamento específicas de dados.

Estes são alguns dos pontos de extensibilidade principais:

- APIs de extensibilidade do Visual Studio Code
- Ferramentas de criação de extensão de dados Studio do Azure
- Gerenciar as contribuições do painel de controle guia Painel
- Insights com experiências de ações
- APIs de extensibilidade do Studio de dados do Azure
- APIs do provedor de dados personalizados

## <a name="visual-studio-code-extensibility-apis"></a>APIs de extensibilidade do Visual Studio Code

Porque o núcleo [!INCLUDE[name-sos](../includes/name-sos.md)] plataforma é compilada em cima do Visual Studio Code, detalhes sobre as APIs de extensibilidade do Visual Studio Code são encontrados a [criação de extensão](https://code.visualstudio.com/docs/extensions/overview) e [extensão API](https://code.visualstudio.com/docs/extensionAPI/overview) documentação no site do Visual Studio Code.

## <a name="manage-dashboard-tab-panel-contributions"></a>Gerenciar as contribuições do painel de controle guia Painel

Para obter detalhes, consulte [pontos de contribuição](#contribution-points) e [variáveis de contexto](#context-variables).

## <a name="azure-data-studio-extensibility-apis"></a>APIs de extensibilidade do Studio de dados do Azure

Para obter detalhes, consulte [APIs de extensibilidade](extensibility-apis.md).


## <a name="contribution-points"></a>Pontos de contribuição

Esta seção aborda os vários pontos de contribuição que são definidos no manifesto de extensão do Package. JSON.

O IntelliSense tem suporte dentro de azuredatastudio.

## <a name="contributes-dashboard"></a>Contribui com o painel de controle

Contribuir com tab, o contêiner, o widget de visão para o painel.

![Painel](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.Tabs cria as seções do guia da página de painel. Ele espera um objeto ou uma matriz de objetos.  

```json
"dashboard.tabs": [
{
    "id": "test-tab1",
    "title": "Test 1",
    "description": "The test 1 displays a list of widgets.",
    "when": "connectionProvider == 'MSSQL' && !mssql:iscloud",
    "alwaysShow": true,
    "container": {
        …
    }
}
]
```

`dashboard.containers`

Em vez de especificar embutido de contêiner do painel (dentro de dashboard.tab). Você pode registrar usando dashboard.containers de contêineres. Ele aceita um objeto ou uma matriz do objeto.

```json
"dashboard.containers": [
{
    "id": "innerTab1",
    "container": {
        …
    }
},
{
    "id": "innerTab2",
    "container": {
       …
    }
}
]
```

Para fazer referência ao contêiner registrado, especifique a id do contêiner

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

Você pode registrar informações usando dashboard.insights. Isso é semelhante ao [Tutorial: compilar um widget de visão personalizada](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)

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


### <a name="dashboard-container-types"></a>Tipos de contêineres do painel

Atualmente, há quatro tipos de contêiner com suporte:

1. `widgets-container`

    ![Contêiner de widgets](media/extensibility/widgets-container.png)

    A lista de widgets que serão exibidos no contêiner. É um layout de fluxo. Ele aceita a lista de widgets.

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

    ![contêiner do WebView](media/extensibility/webview-container.png)

    A exibição da Web será exibida em todo o contêiner. Ele espera que a id do webview para ser a mesma ID de guia

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
                    …
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
                    …
                }
            }
        ]
    }
    ```



## <a name="context-variables"></a>Variáveis de contexto

Para obter informações gerais sobre o contexto no Visual Studio Code e subsequentemente no Studio de dados do Azure, consulte [extensibilidade](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example).

No estúdio de dados do Azure, temos um contexto específico em torno de conexões de banco de dados disponíveis para extensões.

### <a name="dashboard"></a>Painel

No painel, fornecemos as seguintes variáveis de contexto:

|variável de contexto| descrição|
|:---|:---|
|`connectionProvider` | Uma cadeia de caracteres do identificador para o provedor da conexão atual. Ex. `connectionProvider == 'MSSQL'`.|
|`serverName`|Uma cadeia de caracteres do nome do servidor da conexão atual. Ex. `serverName == 'localhost'`.|
|`databaseName` | Uma cadeia de caracteres do nome do banco de dados da conexão atual. Ex. `databaseName == 'master'`.|
|`connection` | O objeto de perfil de conexão completa para a conexão atual (IConnectionProfile)|
|`dashboardContext` | Uma cadeia de caracteres do contexto da página do painel está atualmente em. 'Database' ou 'server'. Ex. `dashboardContext == 'database'`|
