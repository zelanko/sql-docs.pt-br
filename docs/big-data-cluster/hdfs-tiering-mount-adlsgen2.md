---
title: Montagem ADLS Gen2 para camadas do HDFS
titleSuffix: How to mount ADLS Gen2
description: Este artigo explica como configurar a camada do HDFS para montar um sistema de arquivos de Azure Data Lake Storage externo no HDFS [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]em um.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 822c10ad41232d213302e4bb5e328449d9f5f764
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652314"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>Como montar o ADLS Gen2 para a camada do HDFS em um cluster de Big Data

As seções a seguir fornecem um exemplo de como configurar a camada do HDFS com uma fonte de dados do Azure Data Lake Storage Gen2.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data implantado](deployment-guidance.md)
- [Ferramentas de Big Data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a> Carregar dados no Azure Data Lake Storage

A seção a seguir descreve como configurar o Azure Data Lake Storage Gen2 para testar a camada do HDFS. Caso você já tenha dados armazenados no Azure Data Lake Storage, ignore esta seção para usar seus próprios dados.

1. [Crie uma conta de armazenamento com funcionalidades do Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Crie um contêiner de blob](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) nesta conta de armazenamento para seus dados externos.

1. Faça upload de um arquivo CSV ou Parquet no contêiner. Estes são os dados do HDFS externos que serão montados no HDFS no cluster de Big Data.

## <a name="credentials-for-mounting"></a>Credenciais para montagem

## <a name="use-oauth-credentials-to-mount"></a>Usar credenciais do OAuth para montagem

Para usar as credenciais do OAuth para montagem, é necessário seguir as etapas abaixo:

1. Acesse o [portal do Azure](https://portal.azure.com)
1. Acesse "serviços" no painel de navegação à esquerda e clique em "Azure Active Directory"
1. Usando “Registros de Aplicativo” no menu, crie um “Aplicativo Web” e siga o assistente. **Lembre-se do nome que você criar aqui**. Você precisará adicionar esse nome à sua conta do ADLS como um usuário autorizado.
1. Depois que o aplicativo Web for criado, acesse “chaves” em “configurações” no aplicativo.
1. Selecione uma duração de chave e clique em Salvar. **Salve a chave gerada.**
1.  Volte à página Registros de Aplicativo e clique no botão “Pontos de Extremidade” na parte superior. **Anote a URL do “Ponto de Extremidade do Token”**
1. Agora você deverá ter os seguintes itens anotados para o OAuth:

    - A “ID do Aplicativo” do Aplicativo Web criado acima na etapa 3
    - A chave recém-gerada na etapa 5
    - O ponto de extremidade do token da etapa 6

### <a name="adding-the-service-principal-to-your-adls-account"></a>Como adicionar a entidade de serviço à sua conta do ADLS

1. Acesse o portal novamente, abra sua conta do ADLS e selecione Controle de acesso (IAM) no menu à esquerda.
1. Selecione "Adicionar uma atribuição de função" e procure o nome criado na Etapa 3 acima (observe que ele não aparece na lista, mas será encontrado se você pesquisar o nome completo).
1. Agora, adicione a função “Colaborador de Dados do Storage Blob (Versão Prévia)”.

Aguarde 5 a 10 minutos para usar as credenciais para montagem

### <a name="set-environment-variable-for-oauth-credentials"></a>Definir uma variável de ambiente para as credenciais do OAuth

Abra um prompt de comando em um computador cliente que possa acessar o cluster de Big Data. Defina uma variável de ambiente usando o seguinte formato: Observe que as credenciais precisam estar em uma lista separada por vírgula. O comando 'set' é usado no Windows. Se estiver usando o Linux, use 'export'.

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>Usar chaves de acesso para montagem

Você também pode fazer a montagem usando chaves de acesso que podem ser obtidas para sua conta do ADLS no portal do Azure.

 > [!TIP]
   > Para obter mais informações sobre como encontrar a chave de acesso (`<storage-account-access-key>`) para sua conta de armazenamento, confira [Exibir chaves de conta e cadeia de conexão](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string).

### <a name="set-environment-variable-for-access-key-credentials"></a>Definir variável de ambiente para credenciais de chave de acesso

1. Abra um prompt de comando em um computador cliente que possa acessar o cluster de Big Data.

1. Abra um prompt de comando em um computador cliente que possa acessar o cluster de Big Data. Defina uma variável de ambiente usando o formato a seguir. Observe que as credenciais precisam estar em uma lista separada por vírgula. O comando 'set' é usado no Windows. Se estiver usando o Linux, use 'export'.

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a> Montar o armazenamento HDFS remoto

Agora que você definiu a variável de ambiente MOUNT_CREDENTIALS para chaves de acesso ou usando o OAuth, inicie a montagem. As etapas a seguir montam o armazenamento HDFS remoto do Azure Data Lake no armazenamento HDFS local do cluster de Big Data.

1. Use **kubectl** para localizar o endereço IP do serviço **controller-svc-external** do ponto de extremidade em seu cluster de Big Data. Procure **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Faça logon com **azdata** usando o endereço IP externo do ponto de extremidade do controlador com o nome de usuário e a senha do cluster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. Defina a variável de ambiente MOUNT_CREDENTIALS (role a página para acima para obter as instruções)

1. Monte o armazenamento HDFS remoto no Azure usando a **criação de montagem do azdata BDC HDFS**. Substitua os valores de espaço reservado antes de executar o seguinte comando:

   ```bash
   azdata bdc hdfs mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > O comando mount create é assíncrono. Neste momento, não há nenhuma mensagem indicando se a montagem foi bem-sucedida. Confira a seção [status](#status) para verificar o status das montagens.

Se a montagem tiver sido bem-sucedida, você poderá consultar os dados do HDFS e executar trabalhos do Spark com eles. Ela será exibida no HDFS do cluster de Big Data na localização especificada por `--mount-path`.

## <a id="status"></a> Obter o status das montagens

Para listar o status de todas as montagens no cluster de Big Data, use o seguinte comando:

```bash
azdata bdc hdfs mount status
```

Para listar o status de uma montagem em um caminho específico no HDFS, use o seguinte comando:

```bash
azdata bdc hdfs mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Atualizar uma montagem

O exemplo a seguir atualiza a montagem.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Excluir a montagem

Para excluir a montagem, use o comando **azdata BDC HDFS Mount Delete** e especifique o caminho de montagem no HDFS:

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sobre o, consulte [o que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
