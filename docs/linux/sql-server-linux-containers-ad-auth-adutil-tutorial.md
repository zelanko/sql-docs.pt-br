---
title: Configurar a autenticação do Active Directory com contêineres baseados no SQL Server em Linux usando adutil
description: Passo a passo sobre como configurar a autenticação do Active Directory com contêineres do SQL Server em Linux usando adutil
author: amvin87
ms.author: amitkh
ms.reviewer: vanto
ms.date: 12/10/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 318fb046adc25cc2ff485b14974bb756e586162b
ms.sourcegitcommit: 18e2f0706e03d0b2b6324845244fbafaa077a8dd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97103271"
---
# <a name="tutorial-configure-active-directory-authentication-with-sql-server-on-linux--containers"></a>Tutorial: Configurar a autenticação do Active Directory com contêineres do SQL Server em Linux

> [!NOTE]
> O **adutil** está em **versão prévia pública**

Este tutorial explica como configurar contêineres do SQL Server em Linux para dar suporte à autenticação do AD (Active Directory), também conhecida como autenticação integrada. Para obter uma visão geral, confira [Autenticação do Active Directory para SQL Server em Linux](sql-server-linux-active-directory-auth-overview.md).

Este tutorial é composto pelas seguintes etapas:

> [!div class="checklist"]
> - Instalar o adutil-preview
> - Ingressar o host Linux no domínio do AD
> - Criar um usuário do AD para o SQL Server e definir SPN (ServicePrincipalName) usando a ferramenta adutil
> - Criar o arquivo keytab do serviço SQL Server
> - Criar os arquivos mssql.conf e krb5.conf para serem usados pelo contêiner do SQL Server
> - Montar os arquivos de configuração e implantar o contêiner de SQL Server
> - Criar logons do SQL Server baseados no AD usando Transact-SQL
> - Conectar-se ao SQL Server usando a autenticação do AD

## <a name="prerequisites"></a>Pré-requisitos

Os itens a seguir são necessários antes de configurar a autenticação do AD:

- Ter um controlador de domínio do AD (Windows) em sua rede.
- Instale a ferramenta adutil-preview em um computador host Linux, que é ingressado em um domínio. Siga a seção [Instalar o adutil-preview](#install-adutil-preview) abaixo com base na distribuição do Linux que você está executando para instalar a ferramenta adutil-preview.

## <a name="container-deployment-and-preparation"></a>Preparação e implantação de contêiner

Para configurar seu contêiner, você precisará saber antecipadamente a porta que será usada por ele no host. A porta padrão, 1433, pode estar mapeada de modo diferente no host do contêiner. Para este tutorial, a porta 5433 no host será mapeada para a porta 1433 do contêiner. Para obter mais informações, confira nosso início rápido, [Executar imagens de contêiner do SQL Server com o Docker](quickstart-install-connect-docker.md)

Ao registrar SPNs (nomes de entidade de serviço), você pode usar o nome do host do computador ou do contêiner, mas configure-o de acordo com o que você gostaria de ver ao se conectar ao contêiner externamente.

Verifique se há uma entrada de host de encaminhamento (A) adicionada no Active Directory para o endereço IP do host do Linux, mapeando para o nome do contêiner do SQL Server. Neste tutorial, o endereço IP do computador host `myubuntu` é `10.0.0.10` e o nome do contêiner do SQL Server é `sql1`. Adicionamos a entrada do host de encaminhamento no Active Directory, conforme mostrado abaixo. A entrada garante que, quando os usuários se conectarem a sql1.contoso.com, o host correto será atingido.

:::image type="content" source="media/sql-server-linux-containers-ad-auth-adutil-tutorial/host-a-record.png" alt-text="adicionar registro de host":::

Para este tutorial, estamos usando um ambiente no Azure com três VMs. Uma VM que atua como o DC (controlador de domínio) do Windows, com o nome de domínio `contoso.com`. O controlador de domínio se chama `adVM.contoso.com`. O segundo computador é um computador Windows chamado `winbox`, executando o Windows 10 desktop, que é usado como uma caixa cliente e tem o SSMS (SQL Server Management Studio) instalado. O terceiro computador é um computador Ubuntu 18.04 LTS chamado `myubuntu`, que hospeda os contêineres do SQL Server. Todos os computadores foram ingressados no domínio `contoso.com`. Para saber mais, confira [Ingressar o SQL Server em um host Linux em um domínio do Active Directory](sql-server-linux-active-directory-join-domain.md).

> [!NOTE]
> Ingressar o computador do contêiner de host no domínio não é obrigatório, como você pode ver mais adiante neste artigo.

## <a name="install-adutil-preview"></a>Instalar o adutil-preview

No computador host Linux, use os comandos a seguir para instalar o adutil-preview com base na distribuição do Linux.

> [!NOTE]
> Para esta versão prévia, estamos cientes de que, em determinadas distribuições do Linux, se a instalação do adutil for tentada sem o parâmetro `ACCEPT_EULA`, a experiência de instalação será prejudicada. Nossa recomendação abaixo é instalar a ferramenta adutil-preview com `ACCEPT_EULA=Y` definido. Você pode ler o [EULA](https://go.microsoft.com/fwlink/?linkid=2151376) da versão prévia antes da instalação. Estamos trabalhando ativamente nisso, que deve ser corrigido para a versão de GA.

### <a name="rhel"></a>RHEL

1. Baixe o arquivo de configuração do repositório do Red Hat da Microsoft.

    ```bash
    sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/8/prod.repo
    ```

1. Se você tiver uma versão anterior do adutil instalada, remova os pacotes do adutil mais antigos.

    ```bash
    sudo yum remove adutil
    ```

1. Execute os comandos a seguir para instalar o adutil-preview. `ACCEPT_EULA=Y` aceita o EULA da versão prévia do adutil. O EULA é colocado no caminho `/usr/share/adutil/`.

    ```bash
    sudo ACCEPT_EULA=Y yum install -y adutil-preview
    ```

### <a name="ubuntu"></a>Ubuntu

1. Registre o repositório do Microsoft Ubuntu.

    ```bash
    sudo curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
    ```

1. Se você tiver uma versão anterior do adutil instalada, remova os pacotes do adutil mais antigos usando os comandos abaixo

    ```bash
    sudo apt-get remove adutil
    ```

1. Execute o comando a seguir para instalar o adutil-preview. `ACCEPT_EULA=Y` aceita o EULA da versão prévia do adutil. O EULA é colocado no caminho `/usr/share/adutil/`.

    ```bash
    sudo ACCEPT_EULA=Y apt-get install -y adutil-preview
    ```

### <a name="sles"></a>SLES

1. Adicione o repositório do Microsoft SQL Server ao Zypper.

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo
    ```

1. Se você tiver uma versão anterior do adutil instalada, remova os pacotes do adutil mais antigos.

    ```bash
    sudo zypper remove adutil
    ```

1. Execute o comando a seguir para instalar o adutil-preview. `ACCEPT_EULA=Y` aceita o EULA da versão prévia do adutil. O EULA é colocado no caminho `/usr/share/adutil/`.

    ```bash
    sudo ACCEPT_EULA=Y zypper install -y adutil-preview
    ```

## <a name="creating-the-ad-user-spns-and-sql-server-service-keytab"></a>Criando o usuário do AD, os SPNs e o keytab do serviço SQL Server

Se você não quiser que o host do contêiner do SQL Server em Linux faça parte do domínio e não tiver seguido as etapas para ingressar o computador no domínio, em outro computador Linux que já faz parte do domínio do AD, siga as etapas abaixo:

 1. Criar um usuário do AD para o SQL Server e definir o SPN usando a ferramenta adutil.

 2. Criar e configurar o arquivo keytab do serviço SQL Server.

Copie o arquivo mssql.keytab que foi criado para o computador host que executará o contêiner do SQL Server e configure o contêiner para usar o mssql.keytab copiado. Opcionalmente, você também pode ingressar o host Linux que executará o contêiner do SQL Server no domínio do AD e seguir as etapas abaixo no mesmo computador.

### <a name="create-an-ad-user-for-sql-server-and-set-the-serviceprincipalname-using-the-adutil-tool"></a>Criar um usuário do AD para o SQL Server e definir o ServicePrincipalName usando a ferramenta adutil

Habilitar a autenticação do AD em contêineres do SQL Server em Linux requer que as etapas 1 a 3 mencionadas abaixo sejam executadas em um computador Linux que faz parte do domínio do AD.

1. Obtenha ou renove o TGT (tíquete de concessão de tíquete) do Kerberos usando o comando `kinit`. Use uma conta com privilégios para o comando `kinit`. A conta precisa ter permissão para se conectar ao domínio e também deve ser capaz de criar contas e SPNs no domínio.

    > [!IMPORTANT]
    > Antes de executar esse comando, o host já deve fazer parte do domínio, conforme mostrado na etapa anterior.

    ```bash
    kinit privilegeduser@DOMAIN.COM
    ```

    Exemplo: Para o ambiente descrito acima, minha conta com privilégios é `amvin@CONTOSO.COM`

    ```bash
    kinit amvin@CONTOSO.COM
    ```

2. Usando a ferramenta adutil, crie o usuário que será usado como a conta do AD com privilégios pelo SQL Server.

   ```bash
   adutil user create --name sqluser -distname CN=sqluser,CN=Users,DC=CONTOSO,DC=COM --password 'P@ssw0rd'
   ```

    > [!NOTE]
    > As senhas podem ser especificadas de qualquer uma destas três maneiras:
    >
    > - Sinalizador de senha: --password \<password\>
    > - Variáveis de ambiente – `ADUTIL_ACCOUNT_PWD`
    > - Entrada Interativa
    >
    > A precedência dos métodos de entrada de senha segue a ordem das opções listadas acima. As opções recomendadas são fornecer a senha usando variáveis de ambiente ou entrada interativa, pois elas são mais seguras em comparação com o sinalizador de senha.

    Você pode especificar o nome da conta usando o nome diferenciado (`-distname`), como mostrado acima, ou pode usar o nome da UO (unidade organizacional). O nome da UO (`--ou`) tem precedência sobre o nome diferenciado, caso você especifique ambos. Você pode executar o comando abaixo para obter mais detalhes:

    ```bash
    adutil user create --help
    ```

3. Registre os SPNs para o usuário criado acima. Você pode usar o nome do computador host em vez do nome do contêiner, se desejar, dependendo de como deseja que a conexão pareça externamente. Neste tutorial, a porta 5433 é usada em vez da 1433. Esse é o mapeamento de portas para o contêiner. Seu número da porta pode ser diferente.

    ```bash
    adutil spn addauto -n sqluser -s MSSQLSvc -H sql1.contoso.com -p 5433
    ```

    > [!NOTE]
    >
    > - `addauto` criará os SPNs automaticamente, desde que privilégios suficientes estejam presentes para a conta de kinit.
    > - `-n`: nome da conta à qual os SPNs serão atribuídos.
    > - `-s`: o nome do serviço a ser usado para gerar SPNs. Nesse caso, é para o serviço SQL Server e, portanto, o nome do serviço é MSSQLSvc.
    > - `-H`: o nome do host a ser usado para gerar SPNs. Se não for especificado, o FQDN do host local será usado. Forneça também o FQDN para o nome do contêiner. Nesse caso, o nome do contêiner é `sql1` e o FQDN é `sql1.contoso.com`.
    > - `-p`: a porta a ser usada para gerar SPNs. Se não for especificado, os SPNs serão gerados sem uma porta. As conexões do SQL só funcionarão nesse caso quando o SQL Server estiver escutando a porta padrão, 1433.

### <a name="create-the-sql-server-service-keytab-file"></a>Criar o arquivo keytab do serviço SQL Server

Crie o arquivo keytab que contém entradas para cada um dos 4 SPNs criados anteriormente, bem como um para o usuário. O arquivo keytab será montado no contêiner para que possa ser criado em qualquer local no host. Você pode alterar esse caminho com segurança, desde que o keytab resultante seja montado corretamente ao usar o docker/podman para implantar o contêiner.

Para criar o keytab para todos os SPNs, podemos usar a opção `createauto`:

```bash
adutil keytab createauto -k /container/sql1/secrets/mssql.keytab -p 5433 -H sql1.contoso.com --password 'P@ssw0rd' -s MSSQLSvc
```

> [!NOTE]
>
> - `-k`: caminho em que você deseja que o arquivo `mssql.keytab` seja criado. No exemplo acima, o diretório "/container/sql1/secrets" já deve existir no host.
> - `-p`: a porta a ser usada para gerar SPNs. Se não for especificado, os SPNs serão gerados sem uma porta.
> - `-H`: o nome do host a ser usado para gerar SPNs. Se não for especificado, o FQDN do host local será usado. Forneça também o FQDN para o nome do contêiner. Nesse caso, o nome do contêiner é `sql1` e o FQDN é `sql1.contoso.com`.
> - `-s`: o nome do serviço a ser usado para gerar SPNs. Nesse caso, é para o serviço SQL Server e, portanto, o nome do serviço é MSSQLSvc.
> - `--password`: essa é a senha da conta de usuário privilegiada do AD que foi criada anteriormente.
> - `-e` ou `--enctype`: Tipos de criptografia para a entrada de keytab. Use uma lista de valores separados por vírgulas. Se não for especificado, um prompt interativo será apresentado.

Quando for dada a opção de escolher os tipos de criptografia, você poderá escolher mais de um. Para este exemplo, escolhemos `aes256-cts-hmac-sha1-96` e `arcfour-hmac`. Certifique-se de escolher o tipo de criptografia que tem suporte do host e do domínio.

Se deseja escolher o tipo de criptografia de maneira não interativa, você pode especificar sua escolha de tipo de criptografia com o argumento -e no comando acima. Para obter ajuda adicional sobre os comandos de adutil, execute o comando a seguir.

```bash
adutil keytab createauto --help
```

> [!NOTE]
> `arcfour-hmac` é uma criptografia fraca e não é um tipo de criptografia recomendada a ser usada no ambiente de produção.

Para criar o keytab para o usuário, o comando é:

```bash
adutil keytab create -k /container/sql1/secrets/mssql.keytab -p sqluser --password 'P@ssw0rd!'
```

> [!NOTE]
>
> - `-k`: caminho em que você deseja que o arquivo `mssql.keytab` seja criado. No exemplo acima, o diretório "/container/sql1/secrets" já deve existir no host.
> - `-p`: entidade de segurança a ser adicionada ao keytab.

A criação automática/criação de keytab de adutil não substitui os arquivos anteriores, ela apenas acrescenta ao arquivo se ele já estiver presente.

Verifique se o keytab criado tem as permissões corretas definidas ao implantar o contêiner.

```bash
chmod 440 /container/sql1/secrets/mssql.keytab
```

> [!NOTE]
> Neste ponto, você pode copiar o mssql.keytab do host do Linux atual para o host do Linux em que você implantaria o contêiner do SQL Server e seguir o restante das etapas no host Linux que executarão o contêiner SQL Server. Se as etapas acima foram executadas no mesmo host do Linux em que os contêineres de SQL serão implantados, siga as próximas etapas, bem como no mesmo host.

## <a name="create-the-config-files-to-be-used-by-the-sql-server-container"></a>Criar os arquivos de configuração para serem usados pelo contêiner do SQL Server

1. Crie um arquivo de `mssql.conf` com as configurações do AD. Esse arquivo pode ser criado em qualquer lugar no host e precisa ser montado corretamente durante o comando docker run. Neste exemplo, colocamos esse arquivo `mssql.conf` em `/container/sql1 `, que é nosso diretório de contêiner. O conteúdo do `mssql.conf` é como mostrado abaixo:

    ```output
    [network]
    privilegedadaccount = sqluser
    kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
    ```

    > [!NOTE]
    >
    > - `privilagedadaccount`: Usuário privilegiado do AD a ser usado para autenticação do AD.
    > - `kerberoskeytabfile`: o caminho no contêiner em que o arquivo mssql.keytab será localizado.

1. Crie um arquivo krb5.conf. Um exemplo é mostrado abaixo. A capitalização é importante nesses arquivos.

    ```output
    [libdefaults]
    default_realm = DOMAIN.COM

    [realms]
     CONTOSO.COM = {
         kdc = adVM.contoso.com
         admin_server = adVM.contoso.com
         default_domain = CONTOSO.COM
     }

    [domain_realm]
     .contoso.com = CONTOSO.COM
     contoso.com = CONTOSO.COM


1. Copy all files, `mssql.conf`, `krb5.conf`, `mssql.keytab` to a location that will be mounted to the SQL Server container. In this example, these files are placed on the host at the following locations: `mssql.conf` and `krb5.conf` at `/container/sql1/`. `mssql.keytab` is placed at the location `/container/sql1/secrets/`.

1. Make sure there's enough permission on these folders for the user running the docker/podman command. When the container starts, the user needs access to the folder path created. In this example, we provided the below permissions given to the folder path:

    ```bash
    sudo chmod 755 /container/sql1/
    ```

## <a name="mount-the-config-files-and-deploy-the-sql-server-container"></a>Montar os arquivos de configuração e implantar o contêiner de SQL Server

Execute o contêiner do SQL Server e monte os arquivos de configuração do AD corretos criados anteriormente, conforme mostrado abaixo:

```bash
sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=\<YourStrong@Passw0rd\>" \
-p 5433:1433 --name sql1 \
-v /container/sql1:/var/opt/mssql \
-v /container/sql1/krb5.conf:/etc/krb5.conf \
-d mcr.microsoft.com/mssql/server:2019-latest
```

> [!NOTE]
> Ao executar o contêiner no LSM (Módulo de Segurança do Linux) como hosts habilitados para SELinux, você precisa montar os volumes usando a opção `Z`, que instrui o Docker a rotular o conteúdo com um rótulo não compartilhado privado. Para obter mais informações, confira [Configurar o rótulo do SE Linux](https://docs.docker.com/storage/bind-mounts/#configure-the-selinux-label).

Nosso exemplo conteria estes comandos:

```bash
sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=P@ssw0rd" -p 5433:1433 --name sql1 \
-v /container/sql1:/var/opt/mssql/ \
-v /container/sql1/krb5.conf:/etc/krb5.conf \
--dns-search contoso.com \
--dns 10.0.0.4 \
--add-host adVM.contoso.com:10.0.0.4 \
--add-host contoso.com:10.0.0.4 \
--add-host contoso:10.0.0.4 \
-d mcr.microsoft.com/mssql/server:2019-latest
```

> [!NOTE]
>
> - Os arquivos `mssql.conf` e `krb5.conf` ficam localizados no caminho do arquivo de host `/container/sql1`.
> - O `mssql.keytab` que foi criado fica localizado no caminho do arquivo de host `/container/sql1/secrets`.
> - Como nosso computador host está no Azure, os detalhes do AD na mesma ordem precisam ser acrescentados ao comando docker run. Em nosso exemplo, o controlador de domínio `adVM` está no domínio `contoso.com`, com um endereço IP `10.0.0.4`. O controlador de domínio executa DNS e KDC.

## <a name="create-ad-based-sql-server-logins-in-transact-sql"></a>Criar logons do SQL Server baseados em AD no Transact-SQL

Conecte-se ao contêiner do SQL e execute os comandos a seguir para criar o logon e confirme se ele está listado. Execute esse comando em um computador cliente (Windows ou Linux) executando o SSMS, o ADS (Azure Data Studio) ou qualquer outra ferramenta de CLI (interface de linha de comando).

```sql
create login [contoso\amvin] From Windows
SELECT name FROM sys.server_principals;
```

## <a name="connect-to-sql-server-using-ad-authentication"></a>Conectar-se ao SQL Server usando a autenticação do AD.

Para se conectar usando o [SSMS](../ssms/download-sql-server-management-studio-ssms.md) ou o [ADS](../azure-data-studio/download-azure-data-studio.md), faça logon no SQL Server com as credenciais do Windows usando o nome do SQL Server e o número da porta (o nome pode ser o nome do contêiner ou o nome do host). Em nosso exemplo, o nome do servidor seria `sql1.contoso.com, 5433`.

Você também pode usar uma ferramenta como [sqlcmd](../tools/sqlcmd-utility.md) para se conectar ao SQL Server em seu contêiner.

```bash
sqlcmd -E -S 'sql1.contoso.com, 5433'
```

## <a name="next-steps"></a>Próximas etapas

- [Início Rápido: Executar imagens de contêiner do SQL Server com o Docker](quickstart-install-connect-docker.md)
- [Ingressar o SQL Server em um host Linux em um domínio do Active Directory](sql-server-linux-active-directory-auth-overview.md)
