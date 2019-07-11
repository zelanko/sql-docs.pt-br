---
title: Referência do mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a30f78b24a85f85b85beb914dc0f26af652242fd
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728539"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **mssqlctl** ferramenta para [clusters de big data de 2019 do SQL Server (visualização)](big-data-cluster-overview.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
|[aplicativo mssqlctl](reference-mssqlctl-app.md) | Criar, excluir, executar e gerenciar aplicativos. |
|[mssqlctl bdc](reference-mssqlctl-bdc.md) | Selecionar, gerenciar e operar Clusters grandes de dados do SQL Server. |
|[mssqlctl hdfs](reference-mssqlctl-hdfs.md) | O módulo HDFS fornece sistema de arquivos de comandos para acessar um HDFS. |
[logon de mssqlctl](#mssqlctl-login) | Faça logon no ponto de extremidade de controlador do cluster.
[mssqlctl logout](#mssqlctl-logout) | Faça logoff do cluster.
|[mssqlctl sql](reference-mssqlctl-sql.md) | A CLI do banco de dados SQL permite que o usuário interaja com o SQL Server por meio do T-SQL. |
## <a name="mssqlctl-login"></a>logon de mssqlctl
Quando o cluster é implantado, ele listará o ponto de extremidade de controlador durante a implantação, o que você deve usar para fazer logon.  Se você não souber o ponto de extremidade de controlador, você poderá logon fazendo com que a configuração do kube do seu cluster em seu sistema no local padrão de <user home>/.kube/config ou usar o KUBECONFIG env var, ou seja, exportar KUBECONFIG=path/to/.kube/config.
```bash
mssqlctl login [--cluster-name -n] 
               [--controller-username -u]  
               [--controller-endpoint -e]  
               [--accept-eula -a]
```
### <a name="examples"></a>Exemplos
Faça logon interativamente. Nome do cluster será sempre ser solicitado a fornecer se não for especificado como um argumento. Se você tiver as variáveis de env CONTROLLER_USERNAME, CONTROLLER_PASSWORD e ACCEPT_EULA definido em seu sistema, eles não serão solicitados para. Se você tiver a configuração do kube em seu sistema ou estiver usando o KUBECONFIG env var para especificar o caminho para a configuração, a experiência interativa primeiro tentará usar a configuração e, em seguida, solicita que você se a configuração falhar.
```bash
mssqlctl login
```
Faça logon no (não interativo). Faça logon com o nome do cluster, o nome de usuário do controlador, o ponto de extremidade de controlador e aceitação do EULA definido como argumentos. A variável de ambiente CONTROLLER_PASSWORD deve ser definido.  Se você não quiser especificar o ponto de extremidade de controlador, ter a configuração do kube em seu computador no local padrão de <user home>/.kube/config ou usar o KUBECONFIG env var, ou seja, exportar KUBECONFIG=path/to/.kube/config.
```bash
mssqlctl login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
Faça logon com a configuração do kube na máquina e var env definido para CONTROLLER_USERNAME, CONTROLLER_PASSWORD e ACCEPT_EULA.
```bash
mssqlctl login -n ClusterName
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--cluster-name -n`
Nome do cluster.
#### `--controller-username -u`
Conta do usuário. Se você não quiser usar esse arg, você pode definir a variável de ambiente CONTROLLER_USERNAME.
#### `--controller-endpoint -e`
Ponto de extremidade de controlador de cluster "https://host:port". Se você não quiser usar esse arg, você pode usar a configuração do kube em seu computador. Verifique se a configuração está localizada no local padrão do <user home>/.kube/config ou use o env KUBECONFIG var.
#### `--accept-eula -a`
Você aceita os termos de licença? [Sim/não]. Se você não quiser usar esse arg, você pode definir a variável de ambiente ACCEPT_EULA como 'Sim'
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-logout"></a>mssqlctl logout
Faça logoff do cluster.
```bash
mssqlctl logout 
```
### <a name="examples"></a>Exemplos
Fazer logoff deste usuário.
```bash
mssqlctl logout
```
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).