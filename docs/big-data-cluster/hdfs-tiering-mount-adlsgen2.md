---
title: Montagem ADLS Gen2 para camadas do HDFS
titleSuffix: How to mount ADLS Gen2
description: Este artigo explica como configurar o HDFS disposição em camadas para montar um sistema de arquivo externo do armazenamento do Azure Data Lake no HDFS em um cluster de big data do SQL Server 2019 (visualização).
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9f5d1ce4724f95b511272bb4df8d41ee0df75d90
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993966"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>Como Gen2 ADLS de montagem para o HDFS disposição em camadas em um cluster de big data

As seções a seguir fornecem um exemplo de como configurar o HDFS disposição em camadas com uma fonte de dados do armazenamento do Azure Data Lake Gen2.

## <a name="prerequisites"></a>Prerequisites

- [Cluster de big data implantados](deployment-guidance.md)
- [Ferramentas de big data](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a id="load"></a> Carregar dados no armazenamento do Azure Data Lake

A seção a seguir descreve como configurar o Azure Data Lake armazenamento Gen2 para testar a disposição em camadas do HDFS. Se você já tiver dados armazenados no armazenamento do Azure Data Lake, você pode ignorar esta seção para usar seus próprios dados.

1. [Criar uma conta de armazenamento com os recursos do Data Lake armazenamento Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Criar um contêiner de blob](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) nessa conta de armazenamento para os dados externos.

1. Carrega um arquivo CSV ou Parquet no contêiner. Isso é que os dados externos do HDFS que serão montados no HDFS no cluster de big data.

## <a name="credentials-for-mounting"></a>Credenciais para a montagem

## <a name="use-oauth-credentials-to-mount"></a>Use credenciais OAuth para montar

Para usar credenciais OAuth para montar, você precisará seguir as etapas a seguir:

1. Vá para o [portal do Azure](https://portal.azure.com)
1. Vá para "serviços" no painel de navegação à esquerda e relógio em "Azure Active Directory"
1. Usando "Registros do aplicativo" no menu, crie um "aplicativo Web e siga o assistente. **Lembre-se o nome que você criar aqui**. Você precisará adicionar esse nome à sua conta do ADLS como um usuário autorizado.
1. Depois que o aplicativo web é criado, vá para "chaves" em "configurações" para o aplicativo.
1. Selecione que uma duração de chave e clique em salvam. **Salve a chave gerada.**
1.  Volte para a página de registros do aplicativo e clique no botão "Pontos de extremidade" na parte superior. **Anote a URL de "Ponto de extremidade de Token"**
1. Agora você deve ter o seguinte anotou para o OAuth:

    - A "ID do aplicativo" do aplicativo Web criado anteriormente na etapa 3
    - A chave que você acabou de gerar na etapa 5
    - O ponto de extremidade de token da etapa 6

### <a name="adding-the-service-principal-to-your-adls-account"></a>Adicionar a entidade de serviço à sua conta do ADLS

1. Novamente, acesse o portal e abra sua conta do ADLS e selecione o controle de acesso (IAM) no menu à esquerda.
1. Selecione "Adicionar uma atribuição de função" e pesquise pelo nome que você criou na etapa 3 acima (Observe que ele não aparece na lista, mas será encontrado se você pesquisar o nome completo).
1. Agora, adicione a função de ""armazenamento Blob dados Colaborador (visualização).

Aguarde de 5 a 10 minutos antes de usar as credenciais para a montagem

### <a name="create-credential-file"></a>Criar arquivo de credencial

Abra um prompt de comando em um computador cliente que possa acessar seu cluster de big data.

Crie um arquivo local chamado **filename.creds** que contém suas credenciais de conta de armazenamento do Azure Data Lake Gen2 usando o seguinte formato:

   ```text
    fs.azure.account.auth.type=OAuth
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above]
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above]
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>Use as teclas de acesso para montar

Você também pode montar usando chaves de acesso que você pode obter para sua conta do ADLS no portal do Azure.

 > [!TIP]
   > Para obter mais informações sobre como localizar a chave de acesso (`<storage-account-access-key>`) para sua conta de armazenamento, consulte [exibir e copiar chaves de acesso](https://docs.microsoft.com/azure/storage/common/storage-account-manage?#view-and-copy-access-keys).

### <a name="create-credential-file"></a>Criar arquivo de credencial

1. Abra um prompt de comando em um computador cliente que possa acessar seu cluster de big data.

1. Crie um arquivo local chamado **filename.creds** que contém suas credenciais de conta de armazenamento do Azure Data Lake Gen2 usando o seguinte formato:

   ```text
   fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a> Montar o armazenamento HDFS remoto

Agora que você preparou um arquivo de credencial com chaves de acesso ou usando o OAuth, você pode começar a montagem. As etapas a seguir montagem o armazenamento HDFS remoto no Azure Data Lake para o armazenamento local de HDFS do seu cluster de big data.

1. Use **kubectl** para localizar o endereço IP para o ponto de extremidade **controlador-svc-externo** serviço em seu cluster de big data. Procure os **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-cluster-name>
   ```

1. Faça logon com **mssqlctl** usando o endereço IP externo do ponto de extremidade de controlador com seu nome de usuário do cluster e a senha:

   ```bash
   mssqlctl login -e https://<IP-of-controller-svc-external>:30080/
   ```

1. Montar o armazenamento HDFS remoto no Azure usando **mssqlctl montagem do pool de armazenamento do cluster crie**. Substitua os valores de espaço reservado antes de executar o comando a seguir:

   ```bash
   mssqlctl cluster storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name> --credential-file <path-to-adls-credentials>/file.creds
   ```

   > [!NOTE]
   > A montagem criar comando é assíncrona. Neste momento, não há nenhuma mensagem que indica se a montagem foi bem-sucedida. Consulte a [status](#status) seção para verificar o status do seu montagens.

Se montado com êxito, você deve ser capaz de consultar os dados do HDFS e executar trabalhos do Spark em relação a ela. Ele aparecerá no HDFS para o cluster de big data no local especificado pelo `--mount-path`.

## <a id="status"></a> Obter o status de montagens

Para listar o status de todas as montagens no seu cluster de big data, use o seguinte comando:

```bash
mssqlctl cluster storage-pool mount status
```

Para listar o status de uma montagem de um caminho específico no HDFS, use o seguinte comando:

```bash
mssqlctl cluster storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Excluir a montagem

Para excluir a montagem, use o **mssqlctl exclusão de montagem de pool de armazenamento de cluster** de comando e especifique o caminho de montagem no HDFS:

```bash
mssqlctl cluster storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data de 2019 do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
