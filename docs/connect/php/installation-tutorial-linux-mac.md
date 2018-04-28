---
title: Linux e macOS Tutorial de instalação para os Drivers da Microsoft para PHP para SQL Server | Microsoft Docs
ms.date: 04/11/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: article
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.workload: Inactive
ms.openlocfilehash: 4ab3f815063a537b25b776b6b98fd26e74b7d2c4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux e macOS Tutorial de instalação para os Drivers da Microsoft para PHP para SQL Server
As instruções a seguir pressupõem a um ambiente limpo e mostram como instalar o PHP 7. x, o driver ODBC da Microsoft, Apache e os Drivers da Microsoft para PHP para SQL Server no Ubuntu 16.04 e 17.10, RedHat 7, Debian 8 e 9, Suse 12 e macOS X 10.11 e 10.12. Essas instruções aconselhar instalar os drivers usando PECL, mas você também pode baixar os binários pré-compilada do [Drivers da Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) Github página do projeto e instalá-lo seguindo as instruções em [ Carregando os Drivers da Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md). Para obter uma explicação de carregamento de extensão e por que não adicionamos as extensões ao php.ini, consulte a seção sobre [carregando os drivers](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup).

Esses instalação instrução 7.2 PHP por padrão — consulte as notas no início de cada seção para instalar o PHP 7.0 ou 7.1.

## <a name="contents-of-this-page"></a>Conteúdo desta página:

- [Instalar os drivers no Ubuntu 16.04 e 17.10](#installing-the-drivers-on-ubuntu-1604-and-1710)
- [Instalando os drivers em Red Hat 7](#installing-the-drivers-on-red-hat-7)
- [Instalar os drivers no Debian 8 e 9](#installing-the-drivers-on-debian-8-and-9)
- [Instalando os drivers em 12 Suse](#installing-the-drivers-on-suse-12)
- [Instalando os drivers em macOS El Capitan e Serra](#installing-the-drivers-on-macos-el-capitan-and-sierra)

## <a name="installing-the-drivers-on-ubuntu-1604-and-1710"></a>Instalar os drivers no Ubuntu 16.04 e 17.10

> [!NOTE]
> Para instalar o PHP 7.0 ou 7.1, substitua 7.2 7.0 ou 7.1 nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.2 php7.2-dev php7.2-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instale os pré-requisitos
Instalar o driver ODBC para Ubuntu seguindo as instruções [página de instalação do Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instale os drivers PHP para Microsoft SQL Server
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reinicie o Apache e testar o script de exemplo
```
sudo service apache2 restart
```
Para testar a instalação, consulte [testar a instalação do](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-on-red-hat-7"></a>Instalando os drivers em Red Hat 7

> [!NOTE]
> Para instalar o PHP 7.0 ou 7.1, substitua remi php72 remi php70 ou remi-php71 respectivamente nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum-config-manager --enable remi-php72
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instale os pré-requisitos
Instalar o driver ODBC para Red Hat 7 seguindo as instruções [página de instalação do Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

Compilar os drivers PHP com PECL com PHP 7.2 requer um GCC mais recente do padrão:
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instale os drivers PHP para Microsoft SQL Server
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
Um problema no PECL pode impedir a instalação correta da última versão dos drivers mesmo se você tiver atualizado GCC. Para instalar, baixe os pacotes e compilar manualmente:
```
pecl download sqlsrv
tar xvzf sqlsrv-5.2.0.tgz
cd sqlsrv-5.2.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
Como alternativa, você pode baixar os binários pré-compilada do [página de projeto do Github](https://github.com/Microsoft/msphpsql/releases), ou instalar a partir do repositório de Remi:
```
sudo yum install php-sqlsrv php-pdo_sqlsrv
```
### <a name="step-4-install-apache"></a>Etapa 4. Instalar o Apache
```
sudo yum install httpd
```
SELinux é instalado por padrão e é executado no modo de aplicar. Para permitir o Apache para se conectar aos bancos de dados por meio de SELinux, execute o seguinte comando:
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reinicie o Apache e testar o script de exemplo
```
sudo apachectl restart
```
Para testar a instalação, consulte [testar a instalação do](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-on-debian-8-and-9"></a>Instalar os drivers no Debian 8 e 9

> [!NOTE]
> Para instalar o PHP 7.0 ou 7.1, substitua 7.2 nos comandos a seguir 7.0 ou 7.1.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install –y php7.2 php7.2-dev php7.2-xml
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instale os pré-requisitos
Instalar o driver ODBC para Debian seguindo as instruções [página de instalação do Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Você também precisará gerar a localidade correta para obter uma saída PHP para exibir corretamente em um navegador. Por exemplo, para a localidade de UTF-8 en_US, execute os seguintes comandos:
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instale os drivers PHP para Microsoft SQL Server
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reinicie o Apache e testar o script de exemplo
```
sudo service apache2 restart
```
Para testar a instalação, consulte [testar a instalação do](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-on-suse-12"></a>Instalando os drivers em 12 Suse

> [!NOTE]
> Para instalar o PHP 7.0, ignorar o comando a seguir adicionando o repositório - 7.0 é o padrão PHP no suse 12.
> Para instalar o PHP 7.1, substitua a URL do repositório abaixo com a seguinte URL: `http://download.opensuse.org/repositories/devel:/languages:/php:/php71/SLE_12/devel:languages:php:php71.repo`

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
```
sudo su
zypper -n ar -f http://download.opensuse.org/repositories/devel:languages:php/SLE_12/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instale os pré-requisitos
Instalar o driver ODBC para Suse 12 seguindo as instruções [página de instalação do Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instale os drivers PHP para Microsoft SQL Server
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reinicie o Apache e testar o script de exemplo
```
sudo systemctl restart apache2
```
Para testar a instalação, consulte [testar a instalação do](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-on-macos-el-capitan-and-sierra"></a>Instalando os drivers em macOS El Capitan e Serra

Se você ainda não tivê-lo, instale o brew da seguinte maneira:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> Para instalar o PHP 7.0 ou 7.1, substitua php@7.2 com php@7.0 ou php@7.1 respectivamente nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP

```
brew tap
brew tap homebrew/core
brew install php@7.2
```
PHP agora deve estar no seu caminho--executar `php -v` para verificar se estão executando a versão correta do PHP. Se o PHP não está no caminho ou não é a versão correta, execute o seguinte:
```
brew link --force --overwrite php@7.2
```

### <a name="step-2-install-prerequisites"></a>Etapa 2. Instale os pré-requisitos
Instalar o driver ODBC macOS, seguindo as instruções [página de instalação do Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Além disso, talvez seja necessário instalar as ferramentas do GNU verifique:
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instale os drivers PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
brew install apache2
```
Para localizar o Apache arquivo de configuração para a instalação do Apache, execute 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
e substitua o caminho para `httpd.conf` nos comandos a seguir:
```
echo "LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reinicie o Apache e testar o script de exemplo
```
sudo apachectl restart
```
Para testar a instalação, consulte [testar a instalação do](#testing-your-installation) no final deste documento.

## <a name="testing-your-installation"></a>Testar a instalação

Para testar esse exemplo de script, crie um arquivo chamado testsql.php na raiz do documento do seu sistema. Isso é `/var/www/html/` no Debian, Ubuntu e Redhat, `/srv/www/htdocs` no SUSE, ou `/usr/local/var/www` em macOS. Copie o script a seguir, substituindo o servidor, banco de dados, nome de usuário e senha conforme apropriado.
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "Database" => "yourDatabase",
    "Uid" => "yourUsername",
    "PWD" => "yourPassword"
);

//Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if( $conn === false ) {
    die( FormatErrors( sqlsrv_errors()));
}

//Select Query
$tsql= "SELECT @@Version as SQL_VERSION";

//Executes the query
$getResults= sqlsrv_query($conn, $tsql);

//Error handling
if ($getResults == FALSE)
    die(FormatErrors(sqlsrv_errors()));
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['SQL_VERSION']);
    echo ("<br/>");
}

sqlsrv_free_stmt($getResults);

function FormatErrors( $errors )
{
    /* Display errors. */
    echo "Error information: <br/>";
    foreach ( $errors as $error )
    {
        echo "SQLSTATE: ".$error['SQLSTATE']."<br/>";
        echo "Code: ".$error['code']."<br/>";
        echo "Message: ".$error['message']."<br/>";
    }
}
?>
```
Aponte seu navegador para http://localhost/testsql.php (http://localhost:8080/testsql.php em macOS). Agora você deve ser capaz de se conectar ao banco de dados SQL Server/Azure SQL.

## <a name="see-also"></a>Consulte também  
[Guia de Introdução com os Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Carregando os Drivers da Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Requisitos de sistema para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
