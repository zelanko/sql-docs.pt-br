---
title: referência do azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 33cc3070647c58e6ae57c8bff3d587a76ae0a28d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653095"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para a ferramenta **azdata** para [ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versão prévia)](big-data-cluster-overview.md). Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]gerenciar ](deploy-install-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
|[azdata app](reference-azdata-app.md) | Criar, excluir, executar e gerenciar aplicativos. |
|[azdata bdc](reference-azdata-bdc.md) | Selecionar, gerenciar e operar clusters de Big Data do SQL Server. |
|[azdata login](#azdata-login) | Fazer logon no ponto de extremidade do controlador do cluster.
|[azdata logout](#azdata-logout) | Fazer logoff do cluster.

## <a name="azdata-login"></a>azdata login
Quando o cluster for implantado, ele listará o ponto de extremidade do controlador durante a implantação, que você deve usar para fazer logon.  Se você não souber o ponto de extremidade do controlador, poderá fazer logon fazendo com que a configuração do Kube do cluster seja feita no seu sistema <user home>no local padrão de/.Kube/config ou usar o var de KUBECONFIG env, ou seja, exportar KUBECONFIG = caminho/para/. Kube/config.
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
Fazer logon (não interativamente). Fazer logon com o nome do cluster, o nome de usuário do controlador, o ponto de extremidade do controlador e o a aceitação do EULA definidos como argumentos. A variável de ambiente CONTROLLER_PASSWORD precisa ser definida.  Se você não quiser especificar o ponto de extremidade do controlador, tenha a configuração Kube em seu computador no local padrão de <user home>/.Kube/config ou use KUBECONFIG env var, ou seja, exporte KUBECONFIG = Path/to/. Kube/config.
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
Ponto de extremidade do controlador de cluster "https://host:port". Se não quiser usar esse argumento, você poderá usar a configuração de kube em seu computador. Verifique se a configuração está localizada no local padrão de <user home>/.Kube/config ou use o var de KUBECONFIG env.
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
Cadeia de caracteres de consulta JMESPath. Para obter mais informações, [http://jmespath.org/](http://jmespath.org/]) consulte para obter mais informações e exemplos.
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
Cadeia de caracteres de consulta JMESPath. Para obter mais informações, [http://jmespath.org/](http://jmespath.org/]) consulte para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]gerenciar ](deploy-install-azdata.md).
