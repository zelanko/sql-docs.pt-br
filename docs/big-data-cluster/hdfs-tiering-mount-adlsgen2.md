---
title: Montagem ADLS Gen2 para camadas do HDFS
titleSuffix: How to mount ADLS Gen2
description: Este artigo fornece um exemplo de como configurar a camada do HDFS com uma fonte de dados do Azure Data Lake Storage Gen2.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 06/29/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a4bfb894112f071cc7a628146265ede17b3f0a14
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521033"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>Como montar o ADLS Gen2 para a camada do HDFS em um cluster de Big Data

As seções a seguir fornecem um exemplo de como configurar a camada do HDFS com uma fonte de dados do Azure Data Lake Storage Gen2.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data implantado](deployment-guidance.md)
- [Ferramentas de Big Data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="load-data-into-azure-data-lake-storage"></a><a id="load"></a> Carregar dados no Azure Data Lake Storage

A seção a seguir descreve como configurar o Azure Data Lake Storage Gen2 para testar a camada do HDFS. Caso você já tenha dados armazenados no Azure Data Lake Storage, ignore esta seção para usar seus próprios dados.

1. [Crie uma conta de armazenamento com funcionalidades do Data Lake Storage Gen2](/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Crie um sistema de arquivos](/azure/storage/blobs/data-lake-storage-explorer) nesta conta de armazenamento para seus dados.

1. Faça upload de um arquivo CSV ou Parquet no contêiner. Estes são os dados do HDFS externos que serão montados no HDFS no cluster de Big Data.

## <a name="credentials-for-mounting"></a>Credenciais para montagem

### <a name="use-oauth-credentials-to-mount"></a>Usar credenciais do OAuth para montagem

Para usar as credenciais do OAuth para montagem, é necessário seguir as etapas abaixo:

1. Vá para o [Portal do Azure](https://portal.azure.com)
1. Navegue para o "Azure Active Directory". Você deve ver esse serviço na barra de navegação à esquerda.
1. Na barra de navegação à direita, selecione "Registros de aplicativo" e crie um registro
1. Crie um "Aplicativo Web" e siga o assistente. **Lembre-se do nome do aplicativo que você cria aqui**. Você precisará adicionar esse nome à sua conta do ADLS como um usuário autorizado. Observe também a ID do cliente do aplicativo na visão geral ao selecionar o aplicativo.
1. Depois que o aplicativo Web for criado, vá para "Certificados e segredos" e crie um **Segredo do cliente** e selecione uma duração de chave. **Adicione** o segredo.
1. Volte à página Registros de aplicativo e clique em "Pontos de Extremidade" na parte superior. **Anote a URL do "Ponto de extremidade do token OAuth (v2)"**
1. Agora você deverá ter os seguintes itens anotados para o OAuth:

    - A "ID do Cliente do Aplicativo" do aplicativo Web
    - O segredo do cliente
    - O ponto de extremidade do token

### <a name="adding-the-service-principal-to-your-adls-account"></a>Como adicionar a entidade de serviço à sua conta do ADLS

1. Acesse o portal novamente e navegue até o sistema de arquivos da conta de armazenamento do ADLS e selecione controle de acesso (IAM) no menu à esquerda.
1. Selecione "Adicionar uma atribuição de função" 
1. Selecione a função "Colaborador de Dados de Blob de Armazenamento"
1. Pesquise o nome criado acima (observe que ele não aparece na lista, mas será encontrado se você pesquisar o nome completo).
1. Salve a função.

Aguarde 5 a 10 minutos para usar as credenciais para montagem

### <a name="set-environment-variable-for-oauth-credentials"></a>Definir uma variável de ambiente para as credenciais do OAuth

Abra um prompt de comando em um computador cliente que possa acessar o cluster de Big Data. Defina uma variável de ambiente usando o formato a seguir. As credenciais precisam estar em uma lista separada por vírgula. O comando 'set' é usado no Windows. Se estiver usando o Linux, use 'export'.

**Observe** que você precisa remover qualquer quebra de linha ou espaço entre as vírgulas "," ao fornecer as credenciais. A formatação abaixo é apenas para facilitar a leitura.

```console
   set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
   fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
   fs.azure.account.oauth2.client.endpoint=[token endpoint],
   fs.azure.account.oauth2.client.id=[Application client ID],
   fs.azure.account.oauth2.client.secret=[client secret]
```

## <a name="use-access-keys-to-mount"></a>Usar chaves de acesso para montagem

Você também pode fazer a montagem usando chaves de acesso que podem ser obtidas para sua conta do ADLS no portal do Azure.

 > [!TIP]
   > Para obter mais informações sobre como encontrar a chave de acesso (`<storage-account-access-key>`) para sua conta de armazenamento, confira [Exibir chaves de conta e cadeia de conexão](/azure/storage/common/storage-account-keys-manage#view-access-keys-and-connection-string).

### <a name="set-environment-variable-for-access-key-credentials"></a>Definir variável de ambiente para credenciais de chave de acesso

1. Abra um prompt de comando em um computador cliente que possa acessar o cluster de Big Data.

1. Abra um prompt de comando em um computador cliente que possa acessar o cluster de Big Data. Defina uma variável de ambiente usando o formato a seguir. As credenciais precisam estar em uma lista separada por vírgula. O comando 'set' é usado no Windows. Se estiver usando o Linux, use 'export'.

**Observe** que você precisa remover qualquer quebra de linha ou espaço entre as vírgulas "," ao fornecer as credenciais. A formatação abaixo é apenas para facilitar a leitura.

```console
set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
```

## <a name="mount-the-remote-hdfs-storage"></a><a id="mount"></a> Montar o armazenamento HDFS remoto

Agora que você definiu a variável de ambiente MOUNT_CREDENTIALS para chaves de acesso ou usando o OAuth, inicie a montagem. As etapas a seguir montam o armazenamento HDFS remoto do Azure Data Lake no armazenamento HDFS local do cluster de Big Data.

1. Use **kubectl** para localizar o endereço IP do serviço **controller-svc-external** do ponto de extremidade em seu cluster de Big Data. Procure **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Faça logon com **azdata** usando o endereço IP externo do ponto de extremidade do controlador com o nome de usuário e a senha do cluster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080
   ```
1. Defina a variável de ambiente MOUNT_CREDENTIALS (role a página para acima para obter as instruções)

1. Monte o armazenamento HDFS remoto no Azure usando **azdata bdc hdfs mount create**. Substitua os valores de espaço reservado antes de executar o seguinte comando:

   ```bash
   azdata bdc hdfs mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > O comando mount create é assíncrono. Neste momento, não há nenhuma mensagem indicando se a montagem foi bem-sucedida. Confira a seção [status](#status) para verificar o status das montagens.

Se a montagem tiver sido bem-sucedida, você poderá consultar os dados do HDFS e executar trabalhos do Spark com eles. Ela será exibida no HDFS do cluster de Big Data na localização especificada por `--mount-path`.

## <a name="get-the-status-of-mounts"></a><a id="status"></a> Obter o status das montagens

Para listar o status de todas as montagens no cluster de Big Data, use o seguinte comando:

```bash
azdata bdc hdfs mount status
```

Para listar o status de uma montagem em um caminho específico no HDFS, use o seguinte comando:

```bash
azdata bdc hdfs mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Atualizar uma montagem

O exemplo a seguir atualiza a montagem. Essa atualização também limpará o cache de montagem.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a name="delete-the-mount"></a><a id="delete"></a> Excluir a montagem

Para excluir a montagem, use o comando **azdata bdc hdfs mount delete** e especifique o caminho da montagem no HDFS:

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
