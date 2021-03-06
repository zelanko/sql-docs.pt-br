---
title: azdata bdc reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cc10491dc6fbdd09f543260ccd4ef751cb9a21d1
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358304"
---
# <a name="azdata-bdc"></a>bdc de azdata

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata bdc spark](reference-azdata-bdc-spark.md) | Os comandos do Spark permitem que o usuário interaja com o sistema Spark criando e gerenciando sessões, instruções e lotes.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | O módulo do HDFS fornece comandos para acessar um sistema de arquivos HDFS.
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
Implantação do BDC com argumentos e o perfil de configuração personalizado que foi inicializado por meio de `azdata bdc config init`.
```bash
azdata bdc create --accept-eula yes --config-profile ./path/to/config/profile
```
Implantação do BDC com o nome de cluster personalizado especificado e um perfil de configuração padrão aks-dev-test.
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test
```
Implantação de BDC com argumentos – nenhum prompt será fornecido, pois o sinalizador --Force será usado.
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do cluster de Big Data, usado para namespaces do Kubernetes.
#### `--config-profile -c`
Perfil de configuração do cluster de Big Data, usado para implantar o cluster: ['openshift-prod', 'aks-dev-test-ha', 'aro-dev-test-ha', 'aks-dev-test', 'kubeadm-prod', 'aro-dev-test', 'openshift-dev-test', 'kubeadm-dev-test']
#### `--accept-eula -a`
Você aceita os termos de licença? [sim/não]. Se não quiser usar esse argumento, você poderá definir a variável de ambiente ACCEPT_EULA como 'sim'. Veja os termos da licença do azdata em https://aka.ms/eula-azdata-en.
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-upgrade"></a>azdata bdc upgrade
Atualize as imagens implantadas em cada contêiner no cluster de Big Data do SQL Server. As imagens atualizadas são baseadas na imagem do Docker passada. Se as imagens atualizadas forem de um repositório de imagens do Docker diferente daquele das imagens atualmente implantadas, o parâmetro "Repository" também será necessário.
```bash
azdata bdc upgrade --name -n 
                   --tag -t  
                   
[--repository -r]  
                   
[--controller-timeout -k]  
                   
[--stability-threshold -s]  
                   
[--component-timeout -p]
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
Atualização do BDC para uma nova imagem com a marca "cu2" do mesmo repositório. A atualização aguardará 30 minutos para que o controlador seja atualizado e 30 minutos para que BD do controlador seja atualizado. Em seguida, ele aguardará até que o controlador e o BD do controlador sejam executados por três minutos sem falha, atualizando o restante do cluster. Cada fase seguinte da atualização terá quarenta minutos para ser concluída.
```bash
azdata bdc upgrade -t cu2 --controller-timeout=30 --component-timeout=40 --stability-threshold=3
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--name -n`
Nome do cluster de Big Data, usado para namespaces do Kubernetes.
#### `--tag -t`
A tag de imagem do Docker de destino para a qual atualizar todo o contêiner no cluster.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--repository -r`
O repositório do Docker do qual todos os contêineres no cluster devem extrair suas imagens.
#### `--controller-timeout -k`
O número de minutos de espera até o banco de dados do controlador ou o controlador ser atualizado antes de reverter a atualização.
#### `--stability-threshold -s`
O número de minutos de espera após uma atualização antes de marcá-la como estável.
#### `--component-timeout -p`
O número de minutos de espera para cada fase da atualização (após a atualização do controlador) ser concluída antes de pausar a atualização.
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

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

Para saber mais sobre como instalar a ferramenta **azdata**, confira [Instalar azdata](..\install\deploy-install-azdata.md).

