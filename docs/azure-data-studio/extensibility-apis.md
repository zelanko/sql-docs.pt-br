---
title: APIs de extensibilidade
description: Saiba mais sobre as APIs de extensibilidade do Azure Data Studio, que permitem que extensões interajam com outras partes do Azure Data Studio (como o Pesquisador de Objetos).
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 0ef95d4b77e91bcd950b2d8aa5dddf5bb95b3841
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411132"
---
# <a name="azure-data-studio-extensibility-apis"></a>APIs de extensibilidade do Azure Data Studio

O Azure Data Studio fornece uma API que as extensões podem usar para interagir com outras partes do Azure Data Studio, como o Pesquisador de Objetos. Essas APIs estão disponíveis no arquivo [`src/sql/azdata.d.ts`](https://github.com/Microsoft/azuredatastudio/blob/main/src/sql/azdata.d.ts) e são descritas abaixo.

## <a name="connection-management"></a>Gerenciamento de conexões
`azdata.connection`

### <a name="top-level-functions"></a>Funções de nível superior

- O `getCurrentConnection(): Thenable<azdata.connection.Connection>` obtém a conexão atual com base no editor ativo ou na seleção do Pesquisador de Objetos.

- O `getActiveConnections(): Thenable<azdata.connection.Connection[]>` obtém uma lista de todas as conexões do usuário que estão ativas. Retornará uma lista vazia se não houver essas conexões.

- O `getCredentials(connectionId: string): Thenable<{ [name: string]: string }>` obtém um dicionário que contém as credenciais associadas a uma conexão. De outra forma, seriam retornados como parte do dicionário de opções `azdata.connection.Connection` em um objeto, mas são removidos desse objeto. 

### `Connection`
- `options: { [name: string]: string }` O dicionário de opções de conexão
- `providerName: string` O nome do provedor de conexão (por exemplo, "MSSQL")
- `connectionId: string` O identificador exclusivo para a conexão

### <a name="example-code"></a>Código de exemplo
```
> let connection = azdata.connection.getCurrentConnection();
connection: {
    providerName: 'MSSQL',
    connectionId: 'd97bb63a-466e-4ef0-ab6f-00cd44721dcc',
    options: {
        server: 'mairvine-sql-server',
        user: 'sa',
        authenticationType: 'sqlLogin',
        ...
    },
    ...
}
> let credentials = azdata.connection.getCredentials(connection.connectionId);
credentials: {
    password: 'abc123'
}

```

## <a name="object-explorer"></a>Pesquisador de Objetos

`azdata.objectexplorer`


### <a name="top-level-functions"></a>Funções de nível superior
- `getNode(connectionId: string, nodePath?: string): Thenable<azdata.objectexplorer.ObjectExplorerNode>` Obtenha um nó do Pesquisador de Objetos correspondente à conexão e ao caminho fornecidos. Se nenhum caminho for fornecido, ele retornará o nó de nível superior para a conexão especificada. Se não houver nenhum nó no caminho fornecido, ele retornará `undefined`. Observação: O `nodePath` para um objeto é gerado pelo back-end do Serviço de Ferramentas do SQL e é difícil de construir manualmente. Futuros aprimoramentos de API permitirão que você obtenha nós com base nos metadados fornecidos sobre o nó, como nome, tipo e esquema.

- `getActiveConnectionNodes(): Thenable<azdata.objectexplorer.ObjectExplorerNode>` Obter todos os nós de conexão ativa do Pesquisador de Objetos.

- `findNodes(connectionId: string, type: string, schema: string, name: string, database: string, parentObjectNames: string[]): Thenable<azdata.objectexplorer.ObjectExplorerNode[]>` Localiza todos os nós do Pesquisador de Objetos que correspondem aos metadados especificados. Os argumentos `schema`, `database` e `parentObjectNames` devem ser `undefined` quando não são aplicáveis. O `parentObjectNames` é uma lista de objetos pai que não são do banco de dados, do nível mais alto ao mais baixo no Pesquisador de Objetos, sob o qual o objeto desejado está. Por exemplo, ao procurar uma coluna "column1" que pertença a uma tabela "schema1.table1" e ao banco de dados "database1" com a ID de conexão `connectionId`, chame `findNodes(connectionId, 'Column', undefined, 'column1', 'database1', ['schema1.table1'])`. Confira também a [lista de tipos compatíveis por padrão com o Azure Data Studio](https://github.com/Microsoft/azuredatastudio/wiki/Object-Explorer-types-supported-by-FindNodes-API) para essa chamada à API.

### <a name="objectexplorernode"></a>ObjectExplorerNode
- `connectionId: string` A ID da conexão sob a qual o nó existe

- `nodePath: string` O caminho do nó, conforme usado para chamar a função `getNode`.

- `nodeType: string` Uma cadeia de caracteres que representa o tipo do nó

- `nodeSubType: string` Uma cadeia de caracteres que representa o subtipo do nó

- `nodeStatus: string` Uma cadeia de caracteres que representa o status do nó

- `label: string` O rótulo do nó como ele aparece no Pesquisador de Objetos

- `isLeaf: boolean` Se o nó é um nó folha e, portanto, não tem filhos

- `metadata: azdata.ObjectMetadata` Metadados que descrevem o objeto representado por esse nó

- `errorMessage: string` Mensagem mostrada se o nó está em um estado de erro

- `isExpanded(): Thenable<boolean>` Se o nó está atualmente expandido no Pesquisador de Objetos

- `setExpandedState(expandedState: vscode.TreeItemCollapsibleState): Thenable<void>` Defina se o nó está expandido ou recolhido. Se o estado for definido como Nenhum, o nó não será alterado.

- `setSelected(selected: boolean, clearOtherSelections?: boolean): Thenable<void>` Defina se o nó está selecionado. Se `clearOtherSelections` for verdadeiro, desmarque as outras seleções ao fazer a nova seleção. Se for falso, deixe as seleções existentes. `clearOtherSelections` usa verdadeiro como padrão quando `selected` é verdadeiro e falso quando `selected` é falso.

- `getChildren(): Thenable<azdata.objectexplorer.ObjectExplorerNode[]>` Obtenha todos os nós filho deste nó. Retornará uma lista vazia se não houver nenhum filho.

- `getParent(): Thenable<azdata.objectexplorer.ObjectExplorerNode>` Obtenha o nó pai deste nó. Retornará indefinido se não houver nenhum pai.

### <a name="example-code"></a>Código de exemplo

```cs
private async interactWithOENode(selectedNode: azdata.objectexplorer.ObjectExplorerNode): Promise<void> {
    let choices = ['Expand', 'Collapse', 'Select', 'Select (multi)', 'Deselect', 'Deselect (multi)'];
    if (selectedNode.isLeaf) {
        choices[0] += ' (is leaf)';
        choices[1] += ' (is leaf)';
    } else {
        let expanded = await selectedNode.isExpanded();
        if (expanded) {
            choices[0] += ' (is expanded)';
        } else {
            choices[1] += ' (is collapsed)';
        }
    }
    let parent = await selectedNode.getParent();
    if (parent) {
        choices.push('Get Parent');
    }
    let children = await selectedNode.getChildren();
    children.forEach(child => choices.push(child.label));
    let choice = await vscode.window.showQuickPick(choices);
    let nextNode: azdata.objectexplorer.ObjectExplorerNode = undefined;
    if (choice === choices[0]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Expanded);
    } else if (choice === choices[1]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Collapsed);
    } else if (choice === choices[2]) {
        selectedNode.setSelected(true);
    } else if (choice === choices[3]) {
        selectedNode.setSelected(true, false);
    } else if (choice === choices[4]) {
        selectedNode.setSelected(false);
    } else if (choice === choices[5]) {
        selectedNode.setSelected(false, true);
    } else if (choice === 'Get Parent') {
        nextNode = parent;
    } else {
        let childNode = children.find(child => child.label === choice);
        nextNode = childNode;
    }
    if (nextNode) {
        let updatedNode = await azdata.objectexplorer.getNode(nextNode.connectionId, nextNode.nodePath);
        this.interactWithOENode(updatedNode);
    }
}

vscode.commands.registerCommand('mssql.objectexplorer.interact', () => {
    azdata.objectexplorer.getActiveConnectionNodes().then(activeConnections => {
        vscode.window.showQuickPick(activeConnections.map(connection => connection.label + ' ' + connection.connectionId)).then(selection => {
            let selectedNode = activeConnections.find(connection => connection.label + ' ' + connection.connectionId === selection);
            this.interactWithOENode(selectedNode);
        });
    });
});
```

## <a name="proposed-apis"></a>APIs propostas

Adicionamos APIs propostas para permitir que as extensões exibam a interface do usuário personalizada em caixas de diálogo, assistentes e guias de documentos, entre outros recursos. Confira o [arquivo de tipos de API propostos](https://github.com/Microsoft/azuredatastudio/blob/main/src/sql/azdata.proposed.d.ts) para obter mais documentação, mas lembre-se de que essas APIs estão sujeitas a alterações a qualquer momento. Exemplos de como usar algumas dessas APIs podem ser encontrados na [extensão de exemplo "SqlServices"](https://github.com/Microsoft/azuredatastudio/tree/main/samples/sqlservices).


