---
title: referência do azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f4cecd27865b069764944021639ae1a2e553d76
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304713"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
|[azdata notebook](reference-azdata-notebook.md) | Comandos para exibir, executar e gerenciar notebooks de um terminal. |
|[azdata sql](reference-azdata-sql.md) | A CLI do banco de dados SQL permite que o usuário interaja com o SQL Server por meio de T-SQL. |
|[azdata app](reference-azdata-app.md) | Criar, excluir, executar e gerenciar aplicativos. |
|[azdata bdc](reference-azdata-bdc.md) | Selecionar, gerenciar e operar clusters de Big Data do SQL Server. |
|[controle azdata](reference-azdata-control.md) | Criar, excluir e gerenciar planos de controle. |
[azdata login](#azdata-login) | Fazer logon no ponto de extremidade do controlador do cluster.
[azdata logout](#azdata-logout) | Fazer logoff do cluster.
## <a name="azdata-login"></a>azdata login
Quando o cluster for implantado, ele listará o ponto de extremidade do controlador durante a implantação, que você deverá usar para fazer logon.  Se você não conhecer o ponto de extremidade do controlador, você poderá fazer logon colocando a configuração de kube do seu cluster na localização padrão <user home>/.kube/config ou usando a variável de ambiente KUBECONFIG, ou seja, exportar KUBECONFIG=path/to/.kube/config.
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>Exemplos
Fazer logon interativamente. O nome do cluster será sempre solicitado se não for especificado como um argumento. Se você tiver as variáveis de env CONTROLLER_USERNAME, CONTROLLER_PASSWORD e ACCEPT_EULA definidas em seu sistema, elas não serão solicitadas. Se você tiver a configuração de kube em seu sistema ou estiver usando a variável de ambiente KUBECONFIG para especificar o caminho para a configuração, a experiência interativa primeiro tentará usar a configuração e, em seguida, a solicitará se a configuração falhar.
```bash
azdata login
```
Fazer logon (não interativamente). Fazer logon com o nome do cluster, o nome de usuário do controlador, o ponto de extremidade do controlador e o a aceitação do EULA definidos como argumentos. A variável de ambiente CONTROLLER_PASSWORD precisa ser definida.  Se você não quiser especificar o ponto de extremidade do controlador, coloque a configuração de kube em seu computador na localização padrão <user home>/.kube/config ou usando a variável de env KUBECONFIG, ou seja, exportar KUBECONFIG=path/to/.kube/config.
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
Fazer logon com configuração de kube no computador e definir as variáveis de ambiente CONTROLLER_USERNAME, CONTROLLER_PASSWORD e ACCEPT_EULA.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--cluster-name -n`
Nome do cluster.
#### `--controller-username -u`
Usuário da conta. Se não quiser usar esse argumento, você poderá definir a variável de ambiente CONTROLLER_USERNAME.
#### `--controller-endpoint -e`
Ponto de extremidade do controlador de cluster "https://host:port". Se não quiser usar esse argumento, você poderá usar a configuração de kube em seu computador. Verifique se a configuração está localizada na localização padrão de <user home>/.kube/config ou use a variável de ambiente KUBECONFIG.
#### `--accept-eula -a`
Você aceita os termos de licença? [sim/não]. Se não quiser usar esse argumento, você poderá definir a variável de ambiente ACCEPT_EULA como 'sim'. 
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-logout"></a>azdata logout
Fazer logoff do cluster.
```bash
azdata logout 
```
### <a name="examples"></a>Exemplos
Fazer logoff deste usuário.
```bash
azdata logout
```
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

- Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
