---
title: azdata bdc reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5d5cb5256f4a1b8389d882300a89f0ee0012a99
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74820979"
---
# <a name="azdata-bdc"></a>bdc de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

O artigo a seguir fornece referência para os comandos `bdc` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | Criar cluster de Big Data.
[azdata bdc delete](#azdata-bdc-delete) | Excluir cluster de Big Data.
[azdata bdc upgrade](#azdata-bdc-upgrade) | Atualize as imagens implantadas em cada contêiner no cluster de Big Data do SQL Server.
[azdata bdc config](reference-azdata-bdc-config.md) | Comandos de configuração.
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | Comandos de ponto de extremidade.
[azdata bdc debug](reference-azdata-bdc-debug.md) | Comandos de depuração.
[azdata bdc status](reference-azdata-bdc-status.md) | Comandos de status do BDC.
[azdata bdc control](reference-azdata-bdc-control.md) | Comandos do serviço de controle.
[azdata bdc sql](reference-azdata-bdc-sql.md) | Comandos do serviço do Sql.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Comandos do serviço do Hdfs.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Comandos do serviço do Spark.
[azdata bdc gateway](reference-azdata-bdc-gateway.md) | Comandos do serviço do gateway.
[azdata bdc app](reference-azdata-bdc-app.md) | Comandos do serviço de aplicativo.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Os comandos do Spark permitem que o usuário interaja com o sistema Spark criando e gerenciando sessões, instruções e lotes.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | O módulo do HDFS fornece comandos para acessar um sistema de arquivos HDFS.
## <a name="azdata-bdc-create"></a>azdata bdc create
A configuração Criar um Cluster de Big Data do SQL Server – Kubernetes é necessária em seu sistema, juntamente com as seguintes variáveis de ambiente ['AZDATA_USERNAME', 'AZDATA_PASSWORD'].
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>Exemplos
Experiência de implantação de BDC orientada – você receberá prompts para obter os valores necessários.
```bash
azdata bdc create
```
Implantação de BDC com argumentos.
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
Implantação de BDC com o nome especificado em vez do nome padrão no perfil.
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```
Implantação de BDC com argumentos – nenhum prompt será fornecido, pois o sinalizador --Force será usado.
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do cluster de Big Data, usado para namespaces do Kubernetes.
#### `--config-profile -c`
Perfil de configuração de cluster de Big Data, usado para implantar o cluster: ['kubeadm-dev-test', 'kubeadm-prod', 'aks-dev-test', 'aks-dev-test-ha']
#### `--accept-eula -a`
Você aceita os termos de licença? [sim/não]. Se não quiser usar esse argumento, você poderá definir a variável de ambiente ACCEPT_EULA como 'sim'. Os termos de licença para azdata podem ser exibidos em https://aka.ms/eula-azdata-en e os termos de licença para o cluster de Big Data podem ser vistos em – Enterprise: https://go.microsoft.com/fwlink/?linkid=2104292, Standard: https://go.microsoft.com/fwlink/?linkid=2104294, Developer: https://go.microsoft.com/fwlink/?linkid=2104079.
#### `--node-label -l`
Rótulo do nó de cluster de Big Data, usado para designar em quais nós implantar.
#### `--force -f`
Force a criação, não será solicitado que o usuário forneça nenhum valor e todos os problemas serão impressos como parte do stderr.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-delete"></a>azdata bdc delete
A configuração Excluir o Cluster de Big Data do SQL Server – Kubernetes é necessária no seu sistema.
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>Exemplos
Exclusão de BDC.
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--name -n`
Nome do cluster de Big Data, usado para namespaces de Kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--force -f`
Forçar exclusão do cluster de Big Data.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-upgrade"></a>azdata bdc upgrade
Atualize as imagens implantadas em cada contêiner no cluster de Big Data do SQL Server. As imagens atualizadas são baseadas na imagem do Docker passada. Se as imagens atualizadas forem de um repositório de imagens do Docker diferente daquele das imagens atualmente implantadas, o parâmetro "Repository" também será necessário.
```bash
azdata bdc upgrade --name -n 
                   --tag -t  
                   [--repository -r]
```
### <a name="examples"></a>Exemplos
Atualização do BDC para uma nova tag de imagem "cu2" do mesmo repositório.
```bash
azdata bdc upgrade -t cu2
```
Atualização do BDC para uma nova imagem com a tag "cu2" de um novo repositório "foo/bar/baz".
```bash
azdata bdc upgrade -t cu2 -r foo/bar/baz
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--name -n`
Nome do cluster de Big Data, usado para namespaces do Kubernetes.
#### `--tag -t`
A tag de imagem do Docker de destino para a qual atualizar todo o contêiner no cluster.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--repository -r`
O repositório do Docker do qual todos os contêineres no cluster devem extrair suas imagens.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
