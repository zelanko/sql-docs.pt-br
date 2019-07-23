---
title: Tutorial de instalação de Linux e macOS para Drivers da Microsoft para PHP para SQL Server | Microsoft Docs | Microsoft Docs
ms.date: 06/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: 7a2312a4ff6af5a11825274e3e010873ef2d3bd9
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68256699"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Tutorial de instalação de Linux e macOS para Drivers da Microsoft para PHP para SQL Server
As instruções a seguir consideram um ambiente limpo e mostram como instalar o PHP 7.x, o driver ODBC da Microsoft, o Apache e os Drivers da Microsoft para PHP para SQL Server no Ubuntu 16.04, 18.04 e 18.10, RedHat 7, Debian 8 e 9, Suse 12 e 15 e macOS 10.12, 10.13 e 10.14. Estas instruções aconselham instalar os drivers usando PECL, mas você também pode baixar os binários pré-criados na página do projeto no Github [Drivers da Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) e instalá-los seguindo as instruções em [Carregando os Drivers Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md). Para obter uma explicação do carregamento da extensão e por que não adicionamos as extensões ao php.ini, confira a seção sobre [carregar os drivers](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup).

Essas instruções instalam o PHP 7.3 por padrão. Observe que algumas distribuições compatíveis do Linux têm como padrão o PHP 7.0 ou anterior, que não é compatível com os drivers PHP para SQL Server. Confira as observações no início de cada seção para instalar o PHP 7.1 ou 7.2.

## <a name="contents-of-this-page"></a>Conteúdo desta página:

- [Instalar os drivers no Ubuntu 16.04, 18.04 e 18.10](#installing-the-drivers-on-ubuntu-1604-1804-and-1810)
- [Instalar os drivers no Red Hat 7](#installing-the-drivers-on-red-hat-7)
- [Instalar os drivers no Debian 8 e 9](#installing-the-drivers-on-debian-8-and-9)
- [Instalar os drivers no Suse 12 e 15](#installing-the-drivers-on-suse-12-and-15)
- [Instalar os drivers no macOS Sierra, High Sierra e Mojave](#installing-the-drivers-on-macos-sierra-high-sierra-and-mojave)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-1810"></a>Instalar os drivers no Ubuntu 16.04, 18.04 e 18.10

> [!NOTE]
> Para instalar o PHP 7.1 ou 7.2, substitua 7.3 por 7.1 ou 7.2 nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.3 php7.3-dev php7.3-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instalar pré-requisitos
Instale o driver ODBC para Ubuntu seguindo as instruções na [página de instalação de Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instalar os drivers PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.3/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.3/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.3 sqlsrv pdo_sqlsrv
```

Se houver apenas uma versão do PHP no sistema, a última etapa poderá ser simplificada para `phpenmod sqlsrv pdo_sqlsrv`.

### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
sudo su
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reiniciar o Apache e testar o script de amostra
```
sudo service apache2 restart
```
Para testar sua instalação, confira [Testar a instalação](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-on-red-hat-7"></a>Instalar os drivers no Red Hat 7

> [!NOTE]
> Para instalar o PHP 7.1 ou 7.2, substitua remi-php73 por remi-php71 ou remi-php72, respectivamente, nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php73
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instalar pré-requisitos
Instale o driver ODBC para Red Hat 7 seguindo as instruções na [página de instalação de Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instalar os drivers PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```

Como alternativa, você pode baixar os binários pré-criados na [página do projeto no Github](https://github.com/Microsoft/msphpsql/releases) ou instalar a partir do repositório do Remi:
```
sudo yum install php-sqlsrv
```
### <a name="step-4-install-apache"></a>Etapa 4. Instalar o Apache
```
sudo yum install httpd
```
O SELinux é instalado por padrão e é executado no modo de imposição. Para permitir que o Apache se conecte aos bancos de dados por meio do SELinux, execute o seguinte comando:
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reiniciar o Apache e testar o script de amostra
```
sudo apachectl restart
```
Para testar sua instalação, confira [Testar a instalação](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-on-debian-8-and-9"></a>Instalar os drivers no Debian 8 e 9

> [!NOTE]
> Para instalar o PHP 7.1 ou 7.2, substitua 7.3 por 7.1 ou 7.2 nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.3 php7.3-dev php7.3-xml
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instalar pré-requisitos
Instale o driver ODBC para Debian seguindo as instruções na [página de instalação de Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Você também precisa gerar a localidade correta para que uma saída PHP seja exibida corretamente em um navegador. Por exemplo, para a localidade en_US UTF-8, execute os seguintes comandos:
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instalar os drivers PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.3/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.3/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.3 sqlsrv pdo_sqlsrv
```

Se houver apenas uma versão do PHP no sistema, a última etapa poderá ser simplificada para `phpenmod sqlsrv pdo_sqlsrv`.

### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
sudo su
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reiniciar o Apache e testar o script de amostra
```
sudo service apache2 restart
```
Para testar sua instalação, confira [Testar a instalação](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-on-suse-12-and-15"></a>Instalar os drivers no Suse 12 e 15

> [!NOTE]
> Nas instruções a seguir, substitua <SuseVersion> por sua versão do Suse: se você estiver usando o Suse Enterprise Linux 15, ela será SLE_15 ou SLE_15_SP1, e de forma similar para outras versões. Nem todas as versões do PHP estão disponíveis para todas as versões do Suse Linux. Confira `http://download.opensuse.org/repositories/devel:/languages:/php` para ver quais versões do Suse têm a versão padrão do PHP disponível, ou `http://download.opensuse.org/repositories/devel:/languages:/php:/` para ver quais versões do PHP estão disponíveis relativamente às versões do Suse.

> [!NOTE]
> Pacotes para PHP 7.3 não estão disponíveis para o Suse 12. Para instalar o PHP 7.1, substitua a URL do repositório abaixo pela seguinte URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php71/<SuseVersion>/devel:languages:php:php71.repo`.
> Para instalar o PHP 7.2, substitua a URL do repositório abaixo pela seguinte URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo`.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel php7-openssl
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instalar pré-requisitos
Instale o driver ODBC para Suse seguindo as instruções na [página de instalação de Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instalar os drivers PHP para Microsoft SQL Server
> [!NOTE]
> Se você vir uma mensagem de erro dizendo `Connection to 'pecl.php.net:443' failed: Unable to find the socket transport "ssl"`, edite o script pecl em /usr/bin/pecl e remova o comutador `-n` na última linha. Esse comutador impede o PECL de carregar arquivos ini quando o PHP é chamado, o que impede o carregamento da extensão OpenSSL.

```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reiniciar o Apache e testar o script de amostra
```
sudo systemctl restart apache2
```
Para testar sua instalação, confira [Testar a instalação](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-on-macos-sierra-high-sierra-and-mojave"></a>Instalar os drivers no macOS Sierra, High Sierra e Mojave

Se você ainda não fez isso, instale o brew da seguinte maneira:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> Para instalar o PHP 7.1 ou 7.2, substitua php@7.3 por php@7.1 ou php@7.2, respectivamente, nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP

```
brew tap
brew tap homebrew/core
brew install php@7.3
```
O PHP já deve estar no seu caminho: execute `php -v` para verificar se você está executando a versão correta do PHP. Se o PHP não está no seu caminho ou não tem a versão correta, execute o seguinte:
```
brew link --force --overwrite php@7.3
```

### <a name="step-2-install-prerequisites"></a>Etapa 2. Instalar pré-requisitos
Instale o driver ODBC para macOS seguindo as instruções na [página de instalação de Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Além disso, você precisa instalar as ferramentas de criação do GNU:
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instalar os drivers PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
brew install apache2
```
Para localizar o arquivo de configuração do Apache para a instalação do Apache, execute 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
e substitua o caminho por `httpd.conf` nos comandos a seguir:
```
echo "LoadModule php7_module /usr/local/opt/php@7.3/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reiniciar o Apache e testar o script de amostra
```
sudo apachectl restart
```
Para testar sua instalação, confira [Testar a instalação](#testing-your-installation) no final deste documento.

## <a name="testing-your-installation"></a>Testar a instalação

Para testar esta amostra de script, crie um arquivo chamado testsql.php na raiz do documento do seu sistema. No Ubuntu, Debian e Redhat é `/var/www/html/`, no SUSE é `/srv/www/htdocs` e no macOS é `/usr/local/var/www`. Copie o script a seguir para esse arquivo, substituindo o servidor, o banco de dados, o nome de usuário e a senha, conforme apropriado.
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "database" => "yourDatabase",
    "uid" => "yourUsername",
    "pwd" => "yourPassword"
);

// Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if ($conn === false) {
    die(formatErrors(sqlsrv_errors()));
}

// Select Query
$tsql = "SELECT @@Version AS SQL_VERSION";

// Executes the query
$stmt = sqlsrv_query($conn, $tsql);

// Error handling
if ($stmt === false) {
    die(formatErrors(sqlsrv_errors()));
}
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['SQL_VERSION'] . PHP_EOL;
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

function formatErrors($errors)
{
    // Display errors
    echo "Error information: <br/>";
    foreach ($errors as $error) {
        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
        echo "Code: ". $error['code'] . "<br/>";
        echo "Message: ". $error['message'] . "<br/>";
    }
}
?>
```
Aponte seu navegador para https://localhost/testsql.php (https://localhost:8080/testsql.php no macOS). Agora, você pode se conectar ao banco de dados do SQL Server/SQL do Azure.

## <a name="see-also"></a>Consulte Também  
[Introdução aos Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Carregando os Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Requisitos do sistema para os Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
