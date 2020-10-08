---
title: Proteger contêineres do SQL Server no Docker
description: Entenda as diferentes maneiras de proteger contêineres do SQL Server no Docker e como você pode executar contêineres como outro usuário não raiz no host
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 60ee13c6715362ba821575a3f8b9f9d5bc3e2bfa
ms.sourcegitcommit: 764f90cf2eeca8451afdea2753691ae4cf032bea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91589325"
---
# <a name="secure-sql-server-docker-containers"></a>Proteger contêineres do SQL Server no Docker

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Por padrão, os contêineres do SQL Server 2017 são iniciados como o usuário raiz. Isso pode causar algumas preocupações com a segurança. Este artigo aborda as opções de segurança disponíveis ao executar contêineres do SQL Server no Docker e como criar um contêiner do SQL Server como um usuário não raiz.

## <a name="build-and-run-non-root-sql-server-2017-containers"></a><a id="buildnonrootcontainer"></a> Compilar e executar contêineres não raiz do SQL Server 2017

Siga as etapas abaixo para criar um contêiner do SQL Server 2017 que é iniciado como o usuário `mssql` (não raiz).

> [!NOTE]
> Os contêineres do SQL Server 2019 são iniciados automaticamente como não raiz, portanto, as etapas a seguir se aplicam somente a contêineres SQL Server 2017, que iniciam como raiz por padrão.

1. Baixe o [Dockerfile de exemplo para o Contêiner do SQL Server não raiz](https://raw.githubusercontent.com/microsoft/mssql-docker/master/linux/preview/examples/mssql-server-linux-non-root/Dockerfile) e salve-o como `dockerfile`.

2. Execute o seguinte comando no contexto do diretório do Dockerfile para criar o contêiner de SQL Server não raiz:

    ```bash
    cd <path to dockerfile>
    docker build -t 2017-latest-non-root .
    ```

3. Inicie o contêiner.

    ```bash
    docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword@" --cap-add SYS_PTRACE --name sql1 -p 1433:1433 -d 2017-latest-non-root
    ```

    > [!NOTE]
    > O sinalizador `--cap-add SYS_PTRACE` é necessário para contêineres de SQL Server não raiz para gerar despejos para fins de solução de problemas.

4. Verifique se o contêiner está sendo executado como um usuário não raiz:

    ```bash
    docker exec -it sql1 bash
    ```

    Execute `whoami`, que retornará o usuário em execução dentro do contêiner.
    
    ```bash
    whoami
    ```

## <a name="run-container-as-a-different-non-root-user-on-the-host"></a><a id="nonrootuser"></a> Executar o contêiner como um usuário não raiz diferente no host

Para executar o contêiner do SQL Server como um usuário não raiz diferente, adicione o sinalizador -u ao comando de execução do docker. O contêiner não raiz tem a restrição de que precisa ser executado como parte do grupo raiz, a menos que um volume seja montado em `/var/opt/mssql`, ao qual o usuário não raiz tenha acesso. O grupo raiz não concede permissões de raiz extras ao usuário não raiz.

#### <a name="run-as-a-user-with-a-uid-4000"></a>Executar como um usuário com UID 4000

Você pode iniciar o SQL Server com uma UID personalizada. Por exemplo, o comando a seguir inicia o SQL Server com UID 4000:

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> Verifique se o contêiner do SQL Server tem um usuário nomeado como 'mssql' ou 'root' ou o SQLCMD não poderá ser executado no contêiner. Você pode verificar se o contêiner do SQL Server está sendo executado como um usuário nomeado executando `whoami` dentro do contêiner.

#### <a name="run-the-non-root-container-as-the-root-user"></a>Executar o contêiner não raiz como o usuário raiz

Você pode executar o contêiner não raiz como o usuário raiz, se necessário. Isso também concede todas as permissões de arquivo automaticamente para o contêiner, porque ele tem um privilégio mais elevado.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

#### <a name="run-as-a-user-on-your-host-machine"></a>Executar como um usuário em seu computador host

Você pode iniciar o SQL Server com um usuário existente no computador host com o seguinte comando:
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

#### <a name="run-as-a-different-user-and-group"></a>Executar como um usuário e grupo diferentes

Você pode iniciar o SQL Server com um usuário e um grupo personalizados. Neste exemplo, o volume montado tem permissões configuradas para o usuário ou o grupo no computador host.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="configure-persistent-storage-permissions-for-non-root-containers"></a><a id="storagepermissions"></a> Configurar permissões de armazenamento persistente para contêineres não raiz

Para permitir que o usuário não raiz acesse arquivos de banco de dados que estão em volumes montados, verifique se o usuário ou o grupo no qual o contêiner é executado pode fazer leituras/gravações no armazenamento de arquivos persistente.  

Você pode obter a propriedade atual dos arquivos de banco de dados com este comando.

```bash
ls -ll <database file dir>
```

Execute um dos comandos a seguir se o SQL Server não tiver acesso aos arquivos de banco de dados persistentes.

#### <a name="grant-the-root-group-rw-access-to-the-db-files"></a>Conceder ao grupo raiz acesso de leitura/gravação aos arquivos de banco de dados

Conceda as permissões do grupo raiz aos seguintes diretórios para que o contêiner do SQL Server não raiz tenha acesso aos arquivos de banco de dados.

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

#### <a name="set-the-non-root-user-as-the-owner-of-the-files"></a>Definir o usuário não raiz como o proprietário dos arquivos

Esse pode ser o usuário não raiz padrão ou qualquer outro usuário não raiz que você queira especificar. Neste exemplo, definimos a UID 10001 como o usuário não raiz.

```bash
chown -R 10001:0 <database file dir>
```
## <a name="encrypting-connections-to-sql-server-linux-containers"></a>Criptografar conexões com os Contêineres do SQL Server no Linux

Para criptografar conexões com os contêineres do SQL Server no Linux, você precisará de um certificado dos requisitos que estão documentados [aqui].

Veja abaixo um exemplo de como a conexão pode ser criptografada para os contêineres do SQL Server no Linux. Aqui, usamos um Certificado Autoassinado, que não deve ser usado para cenários de produção nesses ambientes. Nesse caso, você precisa usar certificados de autoridade de certificação.

1. Crie um certificado autoassinado, que é adequado somente para ambientes de teste e de não produção.
  
      ```bash
      openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=sql1.contoso.com' -keyout /container/sql1/mssql.key -out /container/sql1/mssql.pem -days 365
      ```
     Em que sql1 é o nome do host do contêiner de SQL, portanto, ao se conectar a esse contêiner, o nome usado na cadeia de conexão será \'sql1.contoso.com,port\'.

    > [!NOTE]
    > Verifique se o caminho da pasta /container/sql1/ já existe antes de executar o comando acima.

2. Certifique-se de definir as permissões corretas nos arquivos mssql.key e mssql.pem, para evitar erros ao montar os arquivos no contêiner de SQL:

    ```bash
    chmod 440 /container/sql1/mssql.pem
    chmod 440 /container/sql1/mssql.key
    ```

3. Agora, crie um arquivo mssql.conf com o conteúdo abaixo para habilitar a criptografia Iniciada pelo Servidor. Na criptografia Iniciada pelo cliente, altere a última linha para 'forceencryption = 0\'.

    ```bash
    [network]
    tlscert = /etc/ssl/certs/mssql.pem
    tlskey = /etc/ssl/private/mssql.key
    tlsprotocols = 1.2
    forceencryption = 1
    ```

    > [!NOTE]
    > Para algumas distribuições do Linux, o caminho para armazenar o certificado e a chave também pode ser /etc/pki/tls/certs/ e /etc/pki/tls/private/, respectivamente. Verifique o caminho antes de atualizar o mssql.conf para contêineres de SQL. A localização definida no mssql.conf será a localização que o SQL Server no contêiner usará para pesquisar o certificado e a chave. Nesse caso, essa localização é /etc/ssl/certs/ e /etc/ssl/private/.

    O arquivo mssql.conf também é criado na mesma localização da pasta /container/sql1/. Depois de executar as etapas acima, você deverá ter três arquivos: mssql.conf, mssql.key e mssql.pem na pasta sql1.

4. Implante o contêiner de SQL com o comando mostrado abaixo:

    ```bash
    docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=P@ssw0rd" -p 5434:1433 --name sql1 -h sql1 -v /container/sql1/mssql.conf:/var/opt/mssql/mssql.conf -v   /container/sql1/mssql.pem:/etc/ssl/certs/mssql.pem -v /container/sql1/mssql.key:/etc/ssl/private/mssql.key -d mcr.microsoft.com/mssql/server:2019-latest
    ```

    No comando acima, montamos os arquivos mssql.conf, mssql.pem e mssql.key para o contêiner e mapeamos a porta 1433 (porta padrão do SQL Server) no contêiner para a porta 5434 do host. 

    > [!NOTE]
    > Se você estiver usando o RHEL 8 e superiores, também poderá usar o comando \'podman run\' em vez de \'docker run\'. 

Siga as seções \"Registrar o certificado no computador cliente\" e \"Cadeias de conexão de exemplo\" documentadas [aqui][1] para iniciar a criptografia de conexões aos contêineres do SQL Server em Linux.

  [Encrypting connection to SQL Server Linux]: https://docs.microsoft.com/sql/linux/sql-server-linux-encrypted-connections?view=sql-server-ver15&preserve-view=true
  [aqui]: https://docs.microsoft.com/sql/linux/sql-server-linux-encrypted-connections?view=sql-server-ver15&preserve-view=true#requirements-for-certificates
  [1]: https://docs.microsoft.com/sql/linux/sql-server-linux-encrypted-connections?view=sql-server-ver15&preserve-view=true#client-initiated-encryption

## <a name="next-steps"></a>Próximas etapas

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- Comece a usar as imagens de contêiner do SQL Server 2017 no Docker acompanhando o [guia de início rápido](quickstart-install-connect-docker.md?view=sql-server-2017)

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

- Comece a usar as imagens de contêiner do SQL Server 2019 no Docker acompanhando o [guia de início rápido](quickstart-install-connect-docker.md?view=sql-server-ver15)

::: moniker-end

- [Implantar contêineres do SQL Server no Docker e conectar-se a eles](sql-server-linux-docker-container-deployment.md)

- [Referenciar uma configuração e uma personalização adicionais em contêineres do Docker](sql-server-linux-docker-container-configure.md)

- [Solução de problemas de contêineres do SQL Server no Docker](sql-server-linux-docker-container-troubleshooting.md)
