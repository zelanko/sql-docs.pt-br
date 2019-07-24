---
title: referência de azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8136c85f8c32e08423f3d199a021d4f60353b39
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425986"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para a ferramenta **azdata** para [clusters SQL Server 2019 Big data (versão prévia)](big-data-cluster-overview.md). Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para gerenciar SQL Server 2019 Big data clusters](deploy-install-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
|[aplicativo azdata](reference-azdata-app.md) | Crie, exclua, execute e gerencie aplicativos. |
|[BDC azdata](reference-azdata-bdc.md) | Selecione, gerencie e opere SQL Server clusters de Big Data. |
|[azdata Notebook](reference-azdata-notebook.md) | Comandos para exibir, executar e gerenciar blocos de anotações de um terminal. |
[logon do azdata](#azdata-login) | Faça logon no ponto de extremidade do controlador do cluster.
[azdata logout](#azdata-logout) | Faça logoff do cluster.
|[azdata SQL](reference-azdata-sql.md) | A CLI do banco de BD SQL permite que o usuário interaja com SQL Server por meio de T-SQL. |
## <a name="azdata-login"></a>logon do azdata
Quando o cluster for implantado, ele listará o ponto de extremidade do controlador durante a implantação, que você deve usar para fazer logon.  Se você não souber o ponto de extremidade do controlador, poderá fazer logon fazendo com que a configuração do Kube do cluster seja feita no seu <user home>sistema no local padrão de/.Kube/config ou usar o var de KUBECONFIG env, ou seja, exportar KUBECONFIG = caminho/para/. Kube/config.
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>Exemplos
Faça logon interativamente. O nome do cluster será sempre solicitado se não for especificado como um argumento. Se você tiver as variáveis CONTROLLER_USERNAME, CONTROLLER_PASSWORD e ACCEPT_EULA env definidas no seu sistema, elas não serão solicitadas. Se você tiver a configuração de Kube no seu sistema ou estiver usando o var de KUBECONFIG env para especificar o caminho para a configuração, a experiência interativa primeiro tentará usar a configuração e, em seguida, solicitará a você se a configuração falhar.
```bash
azdata login
```
Fazer logon (não interativamente). Faça logon com o nome do cluster, nome de usuário do controlador, ponto de extremidade do controlador e conjunto de aceitação do EULA como argumentos. A variável de ambiente CONTROLLER_PASSWORD deve ser definida.  Se você não quiser especificar o ponto de extremidade do controlador, tenha a configuração Kube em seu computador no local padrão de <user home>/.Kube/config ou use o var de KUBECONFIG env, ou seja, exporte KUBECONFIG = Path/to/. Kube/config.
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
Faça logon com Kube config no computador e env var set para CONTROLLER_USERNAME, CONTROLLER_PASSWORD e ACCEPT_EULA.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--cluster-name -n`
Nome do cluster.
#### `--controller-username -u`
Usuário da conta. Se você não quiser usar esse arg, poderá definir a variável de ambiente CONTROLLER_USERNAME.
#### `--controller-endpoint -e`
Ponto de extremidade do https://host:port controlador de cluster "". Se você não quiser usar esse arg, poderá usar a configuração Kube em seu computador. Verifique se a configuração está localizada no local padrão de <user home>/.Kube/config ou use o var de KUBECONFIG env.
#### `--accept-eula -a`
Você aceita os termos de licença? [Sim/não]. Se você não quiser usar esse arg, poderá definir a variável de ambiente ACCEPT_EULA como ' Sim '. Os termos de licença deste produto podem ser exibidos em https://aka.ms/azdata-eula.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-logout"></a>azdata logout
Faça logoff do cluster.
```bash
azdata logout 
```
### <a name="examples"></a>Exemplos
Faça logoff deste usuário.
```bash
azdata logout
```
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para gerenciar SQL Server 2019 Big data clusters](deploy-install-azdata.md).
