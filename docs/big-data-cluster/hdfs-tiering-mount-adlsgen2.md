---
title: Montagem ADLS Gen2 para camadas do HDFS
titleSuffix: How to mount ADLS Gen2
description: Este artigo explica como configurar a camada do HDFS para montar um sistema de arquivos Azure Data Lake Storage externo no HDFS em um cluster SQL Server 2019 Big Data (versão prévia).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7d8a6dd53452700853dca9774ed0196ed7546fe
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419351"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>Como montar ADLS Gen2 para a disposição em camadas do HDFS em um cluster Big Data

As seções a seguir fornecem um exemplo de como configurar a disposição em camadas do HDFS com uma fonte de dados Azure Data Lake Storage Gen2.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster Big Data implantado](deployment-guidance.md)
- [Ferramentas de Big data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a>Carregar dados em Azure Data Lake Storage

A seção a seguir descreve como configurar Azure Data Lake Storage Gen2 para testar a disposição em camadas do HDFS. Se você já tiver dados armazenados no Azure Data Lake Storage, poderá ignorar esta seção para usar seus próprios dados.

1. [Crie uma conta de armazenamento com recursos de data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Crie um contêiner de blob](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) nesta conta de armazenamento para seus dados externos.

1. Carregue um arquivo CSV ou parquet no contêiner. Estes são os dados de HDFS externos que serão montados no HDFS no cluster Big Data.

## <a name="credentials-for-mounting"></a>Credenciais para montagem

## <a name="use-oauth-credentials-to-mount"></a>Usar credenciais do OAuth para montar

Para usar as credenciais do OAuth para montar, você precisa seguir as etapas abaixo:

1. Vá para o [portal do Azure](https://portal.azure.com)
1. Vá para "serviços" no painel de navegação à esquerda e com o relógio "Azure Active Directory"
1. Usando "registros do aplicativo" no menu, crie um "aplicativo Web e siga o assistente. **Lembre-se do nome que você criar aqui**. Será necessário adicionar esse nome à sua conta do ADLS como um usuário autorizado.
1. Depois que o aplicativo Web for criado, vá para "chaves" em "configurações" para o aplicativo.
1. Selecione uma duração de chave e clique em salvar. **Salve a chave gerada.**
1.  Volte para a página registros do aplicativo e clique no botão "pontos de extremidade" na parte superior. **Anote a URL do "ponto de extremidade do token"**
1. Agora você deve ter os seguintes itens anotados para o OAuth:

    - A "ID do aplicativo" do aplicativo Web que você criou acima na etapa 3
    - A chave que você acabou de gerar na etapa 5
    - O ponto de extremidade do token da etapa 6

### <a name="adding-the-service-principal-to-your-adls-account"></a>Adicionando a entidade de serviço à sua conta do ADLS

1. Acesse o portal novamente e abra sua conta do ADLS e selecione controle de acesso (IAM) no menu à esquerda.
1. Selecione "adicionar uma atribuição de função" e procure o nome que você criou no etapa 3 acima (Observe que ele não aparece na lista, mas será encontrado se você pesquisar o nome completo).
1. Agora, adicione a função "colaborador de dados de blob de armazenamento (versão prévia)".

Aguarde 5-10 minutos antes de usar as credenciais para montar

### <a name="set-environment-variable-for-oauth-credentials"></a>Definir variável de ambiente para credenciais OAuth

Abra um prompt de comando em um computador cliente que possa acessar o cluster Big Data. Defina uma variável de ambiente usando o seguinte formato: Observe que as credenciais precisam estar em uma lista separada por vírgulas. O comando ' Set ' é usado no Windows. Se você estiver usando o Linux, use "exportar" em seu lugar.

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>Usar chaves de acesso para montar

Você também pode montar usando chaves de acesso que você pode obter para sua conta do ADLS no portal do Azure.

 > [!TIP]
   > Para obter mais informações sobre como encontrar a chave de acesso`<storage-account-access-key>`() para sua conta de armazenamento, consulte [Exibir chaves de conta e cadeia de conexão](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string).

### <a name="set-environment-variable-for-access-key-credentials"></a>Definir variável de ambiente para credenciais de chave de acesso

1. Abra um prompt de comando em um computador cliente que possa acessar o cluster Big Data.

1. Abra um prompt de comando em um computador cliente que possa acessar o cluster Big Data. Defina uma variável de ambiente usando o formato a seguir. Observe que as credenciais precisam estar em uma lista separada por vírgulas. O comando ' Set ' é usado no Windows. Se você estiver usando o Linux, use "exportar" em seu lugar.

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a>Montar o armazenamento HDFS remoto

Agora que você definiu a variável de ambiente MOUNT_CREDENTIALS para chaves de acesso ou usando OAuth, você pode iniciar a montagem. As etapas a seguir montam o armazenamento HDFS remoto em Azure Data Lake ao armazenamento HDFS local de seu cluster Big Data.

1. Use **kubectl** para localizar o endereço IP para o serviço controlador de ponto de extremidade **-svc-external** no cluster Big Data. Procure o **IP externo**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Faça logon com **azdata** usando o endereço IP externo do ponto de extremidade do controlador com o nome de usuário e a senha do cluster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. Definir a variável de ambiente MOUNT_CREDENTIALS (role para cima para obter instruções)

1. Monte o armazenamento HDFS remoto no Azure usando o **azdata BDC Storage-Pool Mount criar**. Substitua os valores de espaço reservado antes de executar o seguinte comando:

   ```bash
   azdata bdc storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > O comando Mount Create é assíncrono. Neste momento, não há nenhuma mensagem indicando se a montagem foi bem-sucedida. Consulte a seção [status](#status) para verificar o status de suas montagens.

Se montado com êxito, você deve ser capaz de consultar os dados do HDFS e executar trabalhos do Spark em relação a ele. Ele aparecerá no HDFS para o cluster Big Data no local especificado por `--mount-path`.

## <a id="status"></a>Obter o status de montagens

Para listar o status de todas as montagens no cluster Big Data, use o seguinte comando:

```bash
azdata bdc storage-pool mount status
```

Para listar o status de uma montagem em um caminho específico no HDFS, use o seguinte comando:

```bash
azdata bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Atualizar uma montagem

O exemplo a seguir atualiza a montagem.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a>Excluir a montagem

Para excluir a montagem, use o comando **azdata BDC Storage-Pool Mount Delete** e especifique o caminho de montagem no HDFS:

```bash
azdata bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters SQL Server de Big Data 2019, consulte [o que são SQL Server Big data clusters de 2019?](big-data-cluster-overview.md).
