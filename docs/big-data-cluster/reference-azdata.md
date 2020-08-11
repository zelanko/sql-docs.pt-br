---
title: referência do azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7a3862dca974efc0ef035a0b52edfff39d2f5bcf
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942968"
---
# <a name="azdata"></a>azdata

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
| Comando | Descrição |
| --- | --- |
|[azdata app](reference-azdata-app.md) | Criar, excluir, executar e gerenciar aplicativos. |
|[azdata bdc](reference-azdata-bdc.md) | Selecionar, gerenciar e operar clusters de Big Data do SQL Server. |
|[azdata sql](reference-azdata-sql.md) | A CLI do banco de dados SQL permite que o usuário interaja com o SQL Server por meio de T-SQL. |
[azdata login](#azdata-login) | Faça logon no ponto de extremidade do controlador do cluster e defina seu namespace como seu contexto ativo. Para usar uma senha no logon, defina a variável de ambiente AZDATA_PASSWORD.
[azdata logout](#azdata-logout) | Fazer logoff do cluster.
|[azdata context](reference-azdata-context.md) | Comandos de gerenciamento de contexto. |
|[azdata extension](reference-azdata-extension.md) | Gerencia e atualiza as extensões da CLI. |
|[azdata notebook](reference-azdata-notebook.md) | Comandos para exibir, executar e gerenciar notebooks de um terminal. |
## <a name="azdata-login"></a>azdata login
Quando o cluster for implantado, ele listará o ponto de extremidade do controlador durante a implantação, que você deverá usar para fazer logon.  Se você não conhecer o ponto de extremidade do controlador, você poderá fazer logon colocando a configuração de kube do seu cluster na localização padrão <user home>/.kube/config ou usando a variável de ambiente KUBECONFIG, ou seja, exportar KUBECONFIG=path/to/.kube/config.  Quando você fizer logon, o namespace desse cluster será definido como seu contexto ativo.
```bash
azdata login [--auth] 
             [--endpoint -e]  
             
[--accept-eula -a]  
             
[--namespace -n]  
             
[--username -u]  
             
[--principal -p]
```
### <a name="examples"></a>Exemplos
Faça logon usando autenticação Básica.
```bash
azdata login --auth basic --username johndoe --endpoint https://<ip or domain name>:30080            
```
Faça logon usando o Active Directory.
```bash
azdata login --auth ad --endpoint https://<ip or domain name>:30080                
```
Faça logon usando o Active Directory com uma entidade de segurança explícita.
```bash
azdata login --auth ad --principal johndoe@COSTOSO.COM --endpoint https://<ip or domain name>:30080
```
Fazer logon interativamente. O nome do cluster será sempre solicitado se não for especificado como um argumento. Se você tiver as variáveis de env AZDATA_USERNAME, AZDATA_PASSWORD e ACCEPT_EULA definidas em seu sistema, elas não serão solicitadas. Se você tiver a configuração de kube em seu sistema ou estiver usando a variável de ambiente KUBECONFIG para especificar o caminho para a configuração, a experiência interativa primeiro tentará usar a configuração e, em seguida, a solicitará se a configuração falhar.
```bash
azdata login
```
Fazer logon (não interativamente). Fazer logon com o nome do cluster, o nome de usuário do controlador, o ponto de extremidade do controlador e o a aceitação do EULA definidos como argumentos. A variável de ambiente AZDATA_PASSWORD precisa ser definida.  Se você não quiser especificar o ponto de extremidade do controlador, coloque a configuração de kube em seu computador na localização padrão <user home>/.kube/config ou usando a variável de env KUBECONFIG, ou seja, exportar KUBECONFIG=path/to/.kube/config.
```bash
azdata login --namespace ClusterName --username johndoe@contoso.com  --endpoint https://<ip or domain name>:30080 --accept-eula yes
```
Fazer logon com configuração de kube no computador e definir as variáveis de ambiente AZDATA_USERNAME, AZDATA_PASSWORD e ACCEPT_EULA.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--auth`
A estratégia de autenticação. Autenticação básica ou do Active Directory. O padrão é a autenticação "básica".
#### `--endpoint -e`
Ponto de extremidade do controlador de cluster "https://host:port". Se não quiser usar esse argumento, você poderá usar a configuração de kube em seu computador. Verifique se a configuração está localizada na localização padrão de <user home>/.kube/config ou use a variável de ambiente KUBECONFIG.
#### `--accept-eula -a`
Você aceita os termos de licença? [sim/não]. Se não quiser usar esse argumento, você poderá definir a variável de ambiente ACCEPT_EULA como 'sim'. Os termos de licença desse produto podem ser exibidos em https://aka.ms/eula-azdata-en.
#### `--namespace -n`
Namespace do plano de controle do cluster.
#### `--username -u`
Usuário da conta. Se não quiser usar esse argumento, você poderá definir a variável de ambiente AZDATA_USERNAME.
#### `--principal -p`
Seu realm do Kerberos. Na maioria dos casos, o realm do Kerberos é seu nome de domínio em letras maiúsculas.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
