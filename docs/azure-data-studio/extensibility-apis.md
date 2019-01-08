---
title: APIs de extensibilidade
titleSuffix: Azure Data Studio
description: Saiba mais sobre as APIs de extensibilidade para o estúdio de dados do Azure
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7a13a171024aecbe39bc7c83f77f109914bc4250
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53029747"
---
# <a name="azure-data-studio-extensibility-apis"></a>APIs de extensibilidade do Studio de dados do Azure

[!INCLUDE[name-sos](../includes/name-sos.md)] Fornece uma API que extensões podem usar para interagir com outras partes do Studio de dados do Azure, como o Pesquisador de objetos. Essas APIs estão disponíveis a partir de [ `src/sql/sqlops.d.ts` ](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.d.ts) de arquivo e são descritos abaixo.

## <a name="connection-management"></a>Gerenciamento de Conexão
`sqlops.connection`

### <a name="top-level-functions"></a>Funções de nível superior

- `getCurrentConnection(): Thenable<sqlops.connection.Connection>` Obtém a conexão atual com base na seleção do Pesquisador de objetos ou editor ativo.

- `getActiveConnections(): Thenable<sqlops.connection.Connection[]>` Obtém uma lista de todos os as conexões do usuário que estão ativos. Retorna uma lista vazia se não houver nenhum tais conexões.

- `getCredentials(connectionId: string): Thenable<{ [name: string]: string }>` Obtém um dicionário que contém as credenciais associadas a uma conexão. Eles caso contrário, seriam retornados como parte do dicionário opções sob um `sqlops.connection.Connection` objeto, mas são removidas do objeto. 

### `Connection`
- `options: { [name: string]: string }` O dicionário de opções de conexão
- `providerName: string` O nome do provedor de conexão (por exemplo, "MSSQL")
- `connectionId: string` O identificador exclusivo para a conexão

### <a name="example-code"></a>Código de exemplo
```
> let connection = sqlops.connection.getCurrentConnection();
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
> let credentials = sqlops.connection.getCredentials(connection.connectionId);
credentials: {
    password: 'abc123'
}

```

## <a name="object-explorer"></a>Pesquisador de Objetos

`sqlops.objectexplorer`


### <a name="top-level-functions"></a>Funções de nível superior
- `getNode(connectionId: string, nodePath?: string): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` Obtenha um nó do Pesquisador de objetos correspondente a determinada conexão e o caminho. Se nenhum caminho for fornecido, ele retorna o nó de nível superior para a determinada conexão. Não se houver nenhum nó no caminho especificado, ele retorna `undefined`. Observação: O `nodePath` para um objeto é gerado pelo back-end do serviço de ferramentas do SQL e é difícil construir manualmente. Melhorias futuras da API permitirá que você obter nós com base nos metadados que você fornece sobre o nó, como nome, tipo e esquema.

- `getActiveConnectionNodes(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` Obter todos os nós de conexão do Pesquisador de objetos ativos.

- `findNodes(connectionId: string, type: string, schema: string, name: string, database: string, parentObjectNames: string[]): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` Localize todos os nós do Pesquisador de objetos que correspondem aos metadados fornecidos. O `schema`, `database`, e `parentObjectNames` argumentos devem ser `undefined` quando eles não são aplicáveis. `parentObjectNames` é uma lista de objetos pai de banco de dados não, da mais alta para o nível mais baixo no Pesquisador de objetos, o que o objeto desejado está sob. Por exemplo, ao pesquisar por uma coluna "Coluna1" que pertence a uma tabela "schema1.table1" e o banco de dados "database1" com a ID de conexão `connectionId`, chame `findNodes(connectionId, 'Column', undefined, 'column1', 'database1', ['schema1.table1'])`. Consulte também o [lista de tipos SQL Operations Studio oferece suporte ao padrão de](https://github.com/Microsoft/azuredatastudio/wiki/Object-Explorer-types-supported-by-FindNodes-API) para essa chamada à API.

### <a name="objectexplorernode"></a>ObjectExplorerNode
- `connectionId: string` A id da conexão que o nó existe sob

- `nodePath: string` O caminho do nó, conforme usado para chamar o `getNode` função.

- `nodeType: string` Uma cadeia de caracteres que representa o tipo do nó

- `nodeSubType: string` Uma cadeia de caracteres que representa o subtipo do nó

- `nodeStatus: string` Uma cadeia de caracteres que representa o status do nó

- `label: string` O rótulo do nó como ele aparece no Pesquisador de objetos

- `isLeaf: boolean` Se o nó é um nó folha e, portanto, não tem filhos

- `metadata: sqlops.ObjectMetadata` Metadados que descrevem o objeto representado por este nó

- `errorMessage: string` Mensagem mostrada se o nó está em um estado de erro

- `isExpanded(): Thenable<boolean>` Se o nó está atualmente expandido no Pesquisador de objetos

- `setExpandedState(expandedState: vscode.TreeItemCollapsibleState): Thenable<void>` Defina se o nó é expandido ou recolhido. Se o estado é definido como None, o nó não será alterado.

- `setSelected(selected: boolean, clearOtherSelections?: boolean): Thenable<void>` Defina se o nó é selecionado. Se `clearOtherSelections` for true, desmarque todas as outras seleções ao fazer a nova seleção. Se for false, deixe as seleções existentes. `clearOtherSelections` o padrão é true quando `selected` é true e false quando `selected` é false.

- `getChildren(): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` Obter todos os filhos nós deste nó. Retorna uma lista vazia se não houver nenhum filho.

- `getParent(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` Obtém o nó pai deste nó. Retorna indefinido se não houver nenhum pai.

### <a name="example-code"></a>Código de exemplo

```cs
private async interactWithOENode(selectedNode: sqlops.objectexplorer.ObjectExplorerNode): Promise<void> {
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
    let nextNode: sqlops.objectexplorer.ObjectExplorerNode = undefined;
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
        let updatedNode = await sqlops.objectexplorer.getNode(nextNode.connectionId, nextNode.nodePath);
        this.interactWithOENode(updatedNode);
    }
}

vscode.commands.registerCommand('mssql.objectexplorer.interact', () => {
    sqlops.objectexplorer.getActiveConnectionNodes().then(activeConnections => {
        vscode.window.showQuickPick(activeConnections.map(connection => connection.label + ' ' + connection.connectionId)).then(selection => {
            let selectedNode = activeConnections.find(connection => connection.label + ' ' + connection.connectionId === selection);
            this.interactWithOENode(selectedNode);
        });
    });
});
```

## <a name="proposed-apis"></a>APIs de proposta

Adicionamos APIs propostas para permitir extensões exibir a interface do usuário personalizada em guias de documento, entre outros recursos, assistentes e caixas de diálogo. Consulte a [propostas no arquivo tipos API](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.proposed.d.ts) para obter mais documentação, porém lembre-se que essas APIs estão sujeitos a alterações a qualquer momento. Exemplos de como usar algumas dessas APIs podem ser encontrados na [extensão de exemplo "sqlservices"](https://github.com/Microsoft/azuredatastudio/tree/master/samples/sqlservices).


