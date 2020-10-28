---
title: Criptografia em repouso
titleSuffix: SQL Server Big Data Clusters
description: Saiba tudo sobre a criptografia em repouso em um cluster de Big Data do SQL Server 2019.
author: dacoelho
ms.author: dacoelho
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/19/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: de0bc20d7551e8d42c5dc1463fada6ffcbb6a0fd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257146"
---
# <a name="encryption-at-rest-concepts-and-configuration-guide"></a>Guia de configuração e conceitos de criptografia em repouso

Começando com os Clusters de Big Data do SQL Server CU8, um conjunto de recursos de criptografia em repouso abrangente está disponível para fornecer criptografia em nível de aplicativo a todos os dados armazenados na plataforma. Este guia documenta os conceitos, a arquitetura e a configuração do conjunto de recursos de criptografia em repouso para Clusters de Big Data do SQL Server.

Os Clusters de Big Data do SQL Server armazenam dados nos seguintes dois locais:

* Instância mestra do __SQL Server__
* O __HDFS__ usado pelo pool de armazenamento e pelo Spark.

Para poder criptografar dados de modo transparente em Clusters de Big Data do SQL Server, há duas abordagens possíveis:

* __Criptografia de volume__ . Essa abordagem é compatível com a plataforma Kubernetes e é esperada como uma prática recomendada para implantações de Clusters de Big Data. Este guia não aborda a criptografia de volume. Consulte a documentação da plataforma Kubernetes ou do dispositivo para obter guias sobre como criptografar corretamente os volumes que serão usados para Clusters de Big Data do SQL Server.
* __Criptografia no nível de aplicativo__ . Essa arquitetura refere-se à criptografia de dados pelo aplicativo que manipula os dados antes que eles sejam gravados no disco. Se os volumes fossem expostos, um invasor não conseguiria restaurar os artefatos de dados em outro lugar, a menos que o sistema de destino também tenha sido configurado com as mesmas chaves de criptografia. 

O conjunto de recursos de criptografia em repouso dos Clusters de Big Data do SQL Server dá suporte ao cenário principal de criptografia no nível do aplicativo para os componentes do SQL Server e do HDFS.

As seguintes funcionalidades são fornecidas:

* __Criptografia em repouso gerenciada pelo sistema__ . Essa funcionalidade está disponível apenas no CU8.
* __BYOK (criptografia gerenciada pelo usuário em repouso)__ , com integrações de provedor de chave externa e gerenciada por serviço. Atualmente, somente as chaves criadas pelo usuário e gerenciadas por serviço são compatíveis.

## <a name="key-definitions"></a>Definições importantes

### <a name="sql-server-big-data-clusters-key-management-service-kms"></a>KMS (Serviço de Gerenciamento de Chaves) de Clusters de Big Data do SQL Server

Um serviço hospedado pelo controlador responsável por gerenciar chaves e certificados para o conjunto de recursos de criptografia em repouso para o cluster BDC do SQL Server. Esse é um serviço compatível com os seguintes recursos:

* Gerenciamento seguro e armazenamento de chaves e certificados usados para criptografia em repouso.
* Compatibilidade de KMS do Hadoop. Ele atua como o Serviço de Gerenciamento de Chaves para o componente HDFS no BDC.
* Gerenciamento de certificados TDE do SQL Server.

O seguinte recurso não é compatível no momento:
* *Suporte a controle de versão de chaves* . 

Chamaremos esse serviço de __KMS do BDC__ no restante deste documento. Além disso, o termo __BDC__ é usado para fazer referência à plataforma de computação de __Clusters de Big Data do SQL Server__ .

### <a name="system-managed-keys-and-certificates"></a>Chaves e certificados gerenciados pelo sistema

O serviço KMS do BDC gerenciará todas as chaves e certificados para SQL Server e HDFS.

### <a name="user-provided-certificates"></a>Certificados fornecidos pelo usuário

As chaves e os certificados fornecidos pelo usuário serão gerenciados pelo KMS do BDC, normalmente conhecido como BYOK (Bring Your Own Key).

### <a name="external-providers"></a>Provedores externos

Soluções de chave externa compatíveis com o KMS do BDC para delegação externa. Essa funcionalidade não é compatível no momento.

## <a name="encryption-at-rest-on-sql-server-big-data-clusters-cu8"></a>Criptografia em repouso em Clusters de Big Data do SQL Server CU8

Clusters de Big Data do SQL Server CU8 é a versão inicial do conjunto de recursos de criptografia em repouso. Leia este documento atentamente para avaliar seu cenário por completo.

O conjunto de recursos apresenta o __serviço controlador de KMS do BDC__ para fornecer chaves gerenciadas pelo sistema e certificados para criptografia de dados em repouso no SQL Server e no HDFS. Essas chaves e certificados são gerenciados pelo serviço e essa documentação fornece diretrizes operacionais sobre como interagir com o serviço.

* As instâncias do __SQL Server__ aproveitam a funcionalidade de [TDE (Transparent Data Encryption)](../relational-databases/security/encryption/transparent-data-encryption.md) estabelecida.
* O __HDFS__ usa o KMS nativo do Hadoop em cada pod para interagir com o KMS do BDC no controlador. Isso habilita as zonas de criptografia do HDFS, que fornecem caminhos seguros no HDFS.

### <a name="sql-server-instances"></a>Instâncias do SQL Server

* Um certificado gerado pelo sistema será instalado em pods do SQL Server para ser usado com comandos de TDE. O padrão de nomenclatura de certificado gerenciado pelo sistema é `TDECertificate` + `timestamp`. Por exemplo, `TDECertificate2020_09_15_22_46_27`.
* Bancos de dados provisionados por BDC de instância mestra e bancos de dados de usuário não serão criptografados automaticamente. Os DBAs podem usar o certificado instalado para criptografar qualquer banco de dados.
* O pool de computação e o pool de armazenamento serão criptografados automaticamente usando o certificado gerado pelo sistema.
* A criptografia do pool de dados, embora tecnicamente possível usando comandos `EXECUTE AT` de T-SQL, é desencorajada e não é compatível no momento. O uso dessa técnica para criptografar os bancos de dados do pool pode não ser eficaz e a criptografia pode não estar ocorrendo no estado desejado. Ela também cria um caminho de atualização incompatível para as próximas versões.
* Não há nenhuma rotação de certificado no momento. Há suporte para descriptografar e criptografar subsequentemente com um novo certificado usando comandos T-SQL é compatível, desde que não seja em implantações de HA.
* O monitoramento de criptografia ocorre por meio de DMVs de SQL Server padrão existentes para TDE.
* Há suporte para fazer backup de um banco de dados habilitado para TDE e restaurá-lo no cluster.
* Há suporte para HA. Se um banco de dados na instância primária do SQL Server for criptografado, todas as réplicas secundárias do banco de dados também serão criptografadas.

### <a name="hdfs-encryption-zones"></a>Zonas de criptografia de HDFS

* A [integração do Active Directory](active-directory-prerequisites.md) é necessária para habilitar o recurso de zonas de criptografia para o HDFS.
* Uma chave gerada pelo sistema será provisionada no KMS do Hadoop. O nome da chave é `securelakekey`. No CU8, a chave padrão é de 256 bits e damos suporte à criptografia AES de 256 bits.
* Uma zona de criptografia padrão será provisionada usando a chave gerada pelo sistema acima em um caminho chamado `/securelake`.
* Os usuários podem criar chaves adicionais e zonas de criptografia usando as instruções específicas fornecidas neste guia. Durante a criação da chave, os usuários poderão escolher o tamanho de 128, 192 ou 256 para ela.
* Não é possível usar rotação de chave no local para HDFS no CU8. Como alternativa, os dados podem ser movidos de uma zona de criptografia para outra usando distcp.
* Não há suporte para executar a montagem de camadas do HDFS na parte superior de uma zona de criptografia.

## <a name="configuration-guide"></a>Guia de configuração

A criptografia em repouso de Clusters de Big Data do SQL Server é um recurso gerenciado por serviço e, dependendo do seu caminho de implantação, pode exigir etapas adicionais.

Durante __novas implantações de Clusters de Big Data do SQL Server__ , do CU8 em diante, a __criptografia em repouso será habilitada e configurada por padrão__ . Isso significa que:

* O componente KMS do BDC vai ser implantado no controlador e gerar um conjunto padrão de chaves e certificados.
* O SQL Server será implantado com o TDE ativado e os certificados serão instalados pelo controlador.
* O KMS do Hadoop (para HDFS) será configurado para interagir com o KMS do BDC para operações de criptografia. As zonas de criptografia do HDFS estão configuradas e prontas para uso.

Os requisitos e os comportamentos padrão descritos na seção anterior se aplicam.

Se você __atualizar o cluster para o CU8__ , __leia atentamente a próxima seção__ .

### <a name="upgrading-to-cu8"></a>Atualização para o CU8

   > [!CAUTION]
   > Antes de atualizar para os Clusters de Big Data do SQL Server CU8, execute um backup completo dos seus dados.

Nos clusters existentes, o processo de atualização não imporá a criptografia nos dados do usuário nem configurará zonas de criptografia do HDFS. Esse comportamento é adotado por design e o seguinte precisa ser considerado por componente:

* __SQL Server__

    1. __Instância mestra do SQL Server__ . O processo de atualização não afetará nenhum banco de dados de instância mestra e certificados TDE instalados, mas é altamente recomendável fazer backup dos seus bancos de dados e dos certificados de TDE instalados manualmente antes do processo de atualização. Também é aconselhável armazenar esses artefatos fora do cluster BDC do SQL Server.
    1. __Computação e pool de armazenamento__ . Esses bancos de dados são gerenciados pelo sistema, voláteis e serão recriados e criptografados automaticamente na atualização do cluster.
    1. __Pool de dados__ . A atualização não afeta os bancos de dados na parte de instâncias do SQL Server do pool de dados.

* __HDFS__

    1. __HDFS__ . O processo de atualização não tocará arquivos e pastas do HDFS fora das zonas de criptografia.
    1. __As zonas de criptografia não serão configuradas__ . O componente KMS do Hadoop não será configurado para usar o KMS do BDC. Para configurar e habilitar o recurso de zonas de criptografia do HDFS após a atualização, siga a próxima seção.

### <a name="enable-hdfs-encryption-zones-after-upgrade"></a>Habilitar zonas de criptografia do HDFS após a atualização

Execute as ações a seguir se você atualizou o cluster para CU8 (`azdata upgrade`) e deseja habilitar as zonas de criptografia do HDFS.

Requisitos:

- Um cluster integrado ao [Active Directory](active-directory-prerequisites.md).

- [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] configurado e conectado ao cluster no modo AD.

Siga o procedimento a seguir para reconfigurar o cluster com suporte a zonas de criptografia.

1. Depois de executar a atualização com `azdata`, salve os scripts a seguir.

    Requisitos de execução de scripts:
        
    * Ambos os scripts devem estar localizados no mesmo diretório. 
    * `kubectl` em 'PATH
    * Arquivo ```config``` para Kubernetes na pasta ```$HOME/.kube```
    
    Esse script deve ser nomeado __```run-key-provider-patch.sh```__ :

    ```console
    #!/bin/bash
    
    if [[ -z "${BDC_DOMAIN}" ]]; then
      echo "BDC_DOMAIN environment variable with the domain name of the cluster is not defined."
      exit 1
    fi
    
    if [[ -z "${BDC_CLUSTER_NS}" ]]; then
      echo "BDC_CLUSTER_NS environment variable with the cluster namespace is not defined."
      exit 1
    fi
    
    kubectl get configmaps -n test
    
    diff <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py) <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | python -m json.tool)
    
    diff <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py) <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | python -m json.tool)
    
    # Replace the config maps.
    #
    kubectl replace -n $BDC_CLUSTER_NS -o json -f <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py)
    
    kubectl replace -n $BDC_CLUSTER_NS -o json -f <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py)
    
    # Restart the pods which need to have the necessary changes with the core-site.xml
    kubectl delete pods -n $BDC_CLUSTER_NS nmnode-0-0
    kubectl delete pods -n $BDC_CLUSTER_NS storage-0-0
    kubectl delete pods -n $BDC_CLUSTER_NS storage-0-1
    
    # Wait for sometime for pods to restart
    #
    sleep 300
    
    # Check for the KMS process status.
    #
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop nmnode-0-0 -- bash -c 'ps aux | grep kms'
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop storage-0-0 -- bash -c 'ps aux | grep kms'
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop storage-0-1 -- bash -c 'ps aux | grep kms'
    ```

    Esse script deve ser nomeado __```updatekeyprovider.py```__ :

    ```python
    #!/usr/bin/env python3
    
    import json
    import re
    import sys
    import xml.etree.ElementTree as ET
    import os
    
    class CommentedTreeBuilder(ET.TreeBuilder):
        def comment(self, data):
            self.start(ET.Comment, {})
            self.data(data)
            self.end(ET.Comment)
    
    domain_name = os.environ['BDC_DOMAIN']
    
    parser = ET.XMLParser(target=CommentedTreeBuilder())
    
    core_site = 'core-site.xml'
    j = json.load(sys.stdin)
    cs = j['data'][core_site]
    csxml = ET.fromstring(cs, parser=parser)
    props = [prop.find('value').text for prop in csxml.findall(
        "./property/name/..[name='hadoop.security.key.provider.path']")]
    
    kms_provider_path=''
    
    for x in range(5):
        if len(kms_provider_path) != 0:
            kms_provider_path = kms_provider_path + ';'
        kms_provider_path = kms_provider_path + 'nmnode-0-0.' + domain_name
    
    if len(props) == 0:
        prop = ET.SubElement(csxml, 'property')
        name = ET.SubElement(prop, 'name')
        name.text = 'hadoop.security.key.provider.path'
        value = ET.SubElement(prop, 'value')
        value.text = 'kms://https@' + kms_provider_path + ':9600/kms'
        cs = ET.tostring(csxml, encoding='utf-8').decode('utf-8')
    
    j['data'][core_site] = cs
    
    kms_site = 'kms-site.xml.tmpl'
    ks = j['data'][kms_site]
    
    kp_uri_regex = re.compile('(<name>hadoop.kms.key.provider.uri</name>\s*<value>\s*)(.*)(\s*</value>)', re.MULTILINE)
    
    def replace_uri(match_obj):
        key_provider_uri = 'bdc://https@hdfsvault-svc.' + domain_name
        if match_obj.group(2) == 'jceks://file@/var/run/secrets/keystores/kms/kms.jceks' or match_obj.group(2) == key_provider_uri:
            return match_obj.group(1) + key_provider_uri + match_obj.group(3)
        return match_obj.group(0)
    
    ks = kp_uri_regex.sub(replace_uri, ks)
    
    j['data'][kms_site] = ks
    print(json.dumps(j, indent=4, sort_keys=True))
    ```

    Execute __```run-key-provider-patch.sh```__ com os parâmetros apropriados. 

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como usar com eficácia a criptografia em repouso de Clusters de Big Data do SQL Server, confira os seguintes artigos:

- [Criptografia em repouso – TDE do SQL Server](encryption-at-rest-sql-server-tde.md)
- [Criptografia em repouso – zonas de criptografia do HDFS](encryption-at-rest-hdfs-encryption-zones.md)

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira a visão geral a seguir:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
