---
title: Configurar a autenticação do Active Directory com o SQL Server em Linux usando o adutil
description: Passo a passo sobre como configurar a autenticação do Active Directory com o SQL Server em Linux usando adutil
author: amvin87
ms.author: amitkh
ms.reviewer: vanto
ms.date: 12/10/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 462c48c7d0ade07c62a154927c352962f454cc46
ms.sourcegitcommit: 18e2f0706e03d0b2b6324845244fbafaa077a8dd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97103270"
---
# <a name="tutorial-configure-active-directory-authentication-with-sql-server-on-linux-using-adutil"></a>Tutorial: Configurar a autenticação do Active Directory com o SQL Server em Linux usando o adutil

> [!NOTE]
> O **adutil** está em **versão prévia pública**

Este tutorial explica como configurar a autenticação do AD (Active Directory) com o SQL Server em Linux usando adutil. Para conhecer outro método de configuração da autenticação do AD usando o ktpass, confira o [Tutorial: Use a autenticação do Active Directory com o SQL Server em Linux](sql-server-linux-active-directory-authentication.md).

Este tutorial é composto pelas seguintes etapas:

> [!div class="checklist"]
> - Instalar o adutil-preview
> - Ingressar o computador Linux em seu domínio do AD
> - Criar um usuário do AD para o SQL Server e definir SPN (ServicePrincipalName) usando a ferramenta adutil
> - Criar o arquivo keytab do serviço SQL Server
> - Configurar o SQL Server para usar o arquivo keytab
> - Criar logons do SQL Server baseados no AD usando Transact-SQL
> - Conectar-se ao SQL Server usando a autenticação do AD

## <a name="prerequisites"></a>Pré-requisitos

Os itens a seguir são necessários antes de configurar a autenticação do AD:

- Ter um controlador de domínio do AD (Windows) em sua rede.
- Instale a ferramenta adutil-preview em um computador host Linux. Siga a seção abaixo com base na distribuição do Linux que você está executando para instalar o adutil-preview.

## <a name="install-adutil-preview"></a>Instalar o adutil-preview

No computador host Linux, use os comandos a seguir para instalar o adutil-preview.

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

1. Execute os comandos a seguir para instalar o adutil-preview. `ACCEPT_EULA=Y` aceita o EULA da versão prévia do adutil. O EULA fica no caminho '/usr/share/adutil/'.

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

1. Execute o comando a seguir para instalar o adutil-preview. `ACCEPT_EULA=Y` aceita o EULA da versão prévia do adutil. O EULA fica no caminho '/usr/share/adutil/'.

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

1. Execute o comando a seguir para instalar o adutil-preview. `ACCEPT_EULA=Y` aceita o EULA da versão prévia do adutil. O EULA fica no caminho '/usr/share/adutil/'.

    ```bash
    sudo ACCEPT_EULA=Y zypper install -y adutil-preview
    ```

## <a name="domain-machine-preparation"></a>Preparação do computador de domínio

Verifique se há uma entrada de host de encaminhamento (A) adicionada no Active Directory para o endereço IP do host do Linux. Neste tutorial, o endereço IP do computador host `myubuntu` é `10.0.0.10`. Adicionamos a entrada do host de encaminhamento no Active Directory, conforme mostrado abaixo. A entrada garante que, quando os usuários se conectarem a myubuntu.contoso.com, o host correto será atingido.

:::image type="content" source="media/sql-server-linux-ad-auth-adutil-tutorial/host-a-record.png" alt-text="adicionar registro de host":::

Para este tutorial, estamos usando um ambiente no Azure com três VMs. Uma VM que atua como o DC (controlador de domínio) do Windows, com o nome de domínio `contoso.com`. O controlador de domínio se chama `adVM.contoso.com`. O segundo computador é um computador Windows chamado `winbox`, executando o Windows 10 desktop, que é usado como uma caixa cliente e tem o SSMS (SQL Server Management Studio) instalado. O terceiro computador é um computador Ubuntu 18.04 LTS chamado `myubuntu`, que hospeda o SQL Server.

## <a name="join-the-linux-host-machine-to-your-ad-domain"></a>Ingresse o computador host Linux em seu domínio do AD

Ingresse no host do SQL Server Linux com um controlador de domínio do Active Directory. Para saber mais sobre como ingressar um domínio do Active Directory, confira [Ingressar SQL Server em um host Linux em um domínio do Active Directory](sql-server-linux-active-directory-join-domain.md).

## <a name="create-an-ad-user-for-sql-server-and-set-the-serviceprincipalname-spn-using-the-adutil-tool"></a>Criar um usuário do AD para o SQL Server e definir SPN (ServicePrincipalName) usando a ferramenta adutil

1. Obtenha ou renove o TGT (tíquete de concessão de tíquete) do Kerberos usando o comando `kinit`. Use uma conta com privilégios para o comando `kinit`. A conta precisa ter permissão para se conectar ao domínio e também deve ser capaz de criar contas e SPNs no domínio.

    > [!IMPORTANT]
    > Antes de executar esse comando, o computador host já deve fazer parte do domínio, conforme mostrado na etapa anterior.

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

3. Registre os SPNs para a entidade de segurança criada acima. Use o FQDN do computador. Neste tutorial, estamos usando a porta padrão do SQL Server, 1433. Seu número da porta pode ser diferente.

    ```bash
    adutil spn addauto -n sqluser -s MSSQLSvc -H myubuntu.contoso.com -p 1433
    ```

    > [!NOTE]
    >
    > - `addauto` criará os SPNs automaticamente, desde que privilégios suficientes estejam presentes para a conta de kinit.
    > - `-n`: nome da conta à qual os SPNs serão atribuídos.
    > - `-s`: o nome do serviço a ser usado para gerar SPNs. Nesse caso, é para o serviço SQL Server e, portanto, o nome do serviço é `MSSQLSvc`.
    > - `-H`: o nome do host a ser usado para gerar SPNs. Se não for especificado, o FQDN do host local será usado. Nesse caso, o nome do host é `myubuntu` e o FQDN é `myubuntu.contoso.com`.
    > - `-p`: a porta a ser usada para gerar SPNs. Se não for especificado, os SPNs serão gerados sem uma porta. As conexões do SQL só funcionarão nesse caso quando o SQL Server estiver escutando a porta padrão, 1433.

## <a name="create-the-sql-server-service-keytab-file"></a>Criar o arquivo keytab do serviço SQL Server

Crie o arquivo keytab que contém entradas para cada um dos 4 SPNs criados anteriormente, bem como um para o usuário.

```bash
adutil keytab createauto -k /var/opt/mssql/secrets/mssql.keytab -p 1433 -H myubuntu.contoso.com --password 'P@ssw0rd' -s MSSQLSvc 
```

> [!NOTE]
>
> - `-k`: caminho em que você deseja que o arquivo `mssql.keytab` seja criado. No exemplo acima, o diretório `/var/opt/mssql/secrets/` já deve existir no host.
> - `-p`: a porta a ser usada para gerar SPNs. Se não for especificado, os SPNs serão gerados sem uma porta.
> - `-H`: o nome do host a ser usado para gerar SPNs. Se não for especificado, o FQDN do host local será usado. Nesse caso, o nome do host é `myubuntu` e o FQDN é `myubuntu.contoso.com`.
> - `-s`: o nome do serviço a ser usado para gerar SPNs. Nesse caso, é para o serviço SQL Server e, portanto, o nome do serviço é `MSSQLSvc`.
> - `--password`: essa é a senha da conta de usuário privilegiada do AD que foi criada anteriormente.
> - `-e` ou `--enctype`: Tipos de criptografia para a entrada de keytab. Use uma lista de valores separados por vírgulas. Se não for especificado, um prompt interativo será apresentado.

Quando for dada a opção de escolher os tipos de criptografia, você poderá escolher mais de um. Para este exemplo, escolhemos `aes256-cts-hmac-sha1-96` e `arcfour-hmac`. Certifique-se de escolher o tipo de criptografia que tem suporte do host e do domínio.

Se deseja escolher o tipo de criptografia de maneira não interativa, você pode especificar sua escolha de tipo de criptografia com o argumento -e no comando acima. Para obter ajuda adicional sobre os comandos de adutil, execute o comando a seguir.

```bash
adutil keytab createauto --help
```

> [!NOTE]
> `arcfour-hmac` é uma criptografia fraca e não é um tipo de criptografia recomendada a ser usada no ambiente de produção.

Adicione uma entrada no keytab para o nome da entidade de segurança e sua senha que serão usadas pelo SQL Server para se conectar ao AD:

```bash
adutil keytab create -k /var/opt/mssql/secrets/mssql.keytab -p sqluser --password 'P@ssw0rd!'
```

> [!NOTE]
>
> - `-k`: caminho em que você deseja que o arquivo `mssql.keytab` seja criado.
> - `-p`: entidade de segurança a ser adicionada ao keytab.

A criação automática/criação de keytab de adutil não substitui os arquivos anteriores, ela apenas acrescenta ao arquivo se ele já estiver presente.

Verifique se o keytab criado pertence ao usuário `mssql` e se somente o usuário `mssql` tem acesso de leitura/gravação ao arquivo. Você pode executar os comandos `chown` e `chmod`, conforme mostrado abaixo:

```bash
chown mssql. /var/opt/mssql/secrets/mssql.keytab
chmod 440 /var/opt/mssql/secrets/mssql.keytab
```

## <a name="configure-sql-server-to-use-the-keytab"></a>Configurar o SQL Server para usar o keytab

Execute os comandos abaixo para configurar o SQL Server para usar o keytab criado na etapa anterior e defina a conta do AD com privilégio como o usuário criado acima. Em nosso exemplo, o nome de usuário é `sqluser`.

```bash
/opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
/opt/mssql/bin/mssql-conf set network.privilegedadaccount sqluser
```

## <a name="restart-sql-server"></a>Reiniciar o SQL Server

Execute o comando abaixo para reiniciar o serviço SQL Server:

```bash
sudo systemctl restart mssql-server
```

## <a name="create-ad-based-sql-server-logins-in-transact-sql"></a>Criar logons do SQL Server baseados em AD no Transact-SQL

Conecte-se ao SQL Server e execute os comandos a seguir para criar o logon e confirme se ele está listado.

```sql
create login [contoso\amvin] From Windows
SELECT name FROM sys.server_principals;
```

## <a name="connect-to-sql-server-using-ad-authentication"></a>Conectar-se ao SQL Server usando a autenticação do AD.

Para se conectar usando o [SSMS](../ssms/download-sql-server-management-studio-ssms.md) ou o [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md), faça logon no SQL Server com suas credenciais do Windows.

Você também pode usar uma ferramenta como [sqlcmd](../tools/sqlcmd-utility.md) para se conectar ao SQL Server usando a Autenticação do Windows.

```bash
sqlcmd -E -S 'myubuntu.contoso.com'
```

## <a name="next-steps"></a>Próximas etapas

- [Ingressar o SQL Server em um host Linux em um domínio do Active Directory](sql-server-linux-active-directory-auth-overview.md)
- Se estiver interessado em como configurar a autenticação do AD com contêineres de SQL Server em Linux, confira [Configurar a autenticação do Active Directory com contêineres do SQL Server em Linux](sql-server-linux-containers-ad-auth-adutil-tutorial.md)
