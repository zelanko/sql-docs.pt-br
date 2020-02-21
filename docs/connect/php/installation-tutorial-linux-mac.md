---
title: Tutorial de instalação de Linux e macOS para Drivers da Microsoft para PHP para SQL Server | Microsoft Docs | Microsoft Docs
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: aca4ce5392b9cbac7903666b13e7a9cf544f1004
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76918375"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Tutorial de instalação de Linux e macOS para Drivers da Microsoft para PHP para SQL Server
As instruções a seguir consideram um ambiente limpo e mostram como instalar o PHP 7.x, o driver do Microsoft ODBC, o servidor Web do Apache e os Drivers da Microsoft para PHP e para SQL Server no Ubuntu 16.04, 18.04 e 19.10, no RedHat 7 e 8, no Debian 8, 9 e 10, no Suse 12 e 15, no Alpine 3.11 (experimental) e no macOS 10.13, 10.14 e 10.15. Essas instruções aconselham a instalar os drivers usando PECL, mas também é possível baixar os binários predefinidos na página de projetos do GitHub [Drivers da Microsoft para PHP e para SQL Server](https://github.com/Microsoft/msphpsql/releases) e instalá-los seguindo as instruções em [Como carregar os Drivers da Microsoft para PHP e para SQL Server](../../connect/php/loading-the-php-sql-driver.md). Para obter uma explicação do carregamento da extensão e por que não adicionamos as extensões ao php.ini, confira a seção sobre [carregar os drivers](../../connect/php/loading-the-php-sql-driver.md#loading-the-driver-at-php-startup).

Essas instruções instalam o PHP 7.4 por padrão. Observe que algumas distribuições compatíveis com Linux têm como padrão o PHP 7.1 ou anterior que não é compatível com a versão mais recente dos drivers PHP para SQL Server. Confira as observações no início de cada seção para instalar o PHP 7.2 ou 7.3.

As instruções para instalar o Gerenciador de Processos do PHP FastCGI e o PHP-FPM no Ubuntu também estão incluídas. Isso será necessário caso esteja usando o servidor Web nginx em vez do Apache.

## <a name="contents-of-this-page"></a>Conteúdo desta página:

- [Como instalar os drivers no Ubuntu 16.04, 18.04 e 19.10](#installing-the-drivers-on-ubuntu-1604-1804-and-1910)
- [Como instalar os drivers com PHP-FPM no Ubuntu](#installing-the-drivers-with-php-fpm-on-ubuntu)
- [Como instalar os drivers no Red Hat 7 e 8](#installing-the-drivers-on-red-hat-7-and-8)
- [Como instalar os drivers no Debian 8, 9 e 10](#installing-the-drivers-on-debian-8-9-and-10)
- [Instalar os drivers no Suse 12 e 15](#installing-the-drivers-on-suse-12-and-15)
- [Como instalar os drivers no Alpine 3.11](#installing-the-drivers-on-alpine-311)
- [Como instalar os drivers no macOS High Sierra, no Mojave e no Catalina](#installing-the-drivers-on-macos-high-sierra-mojave-and-catalina)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-1910"></a>Como instalar os drivers no Ubuntu 16.04, 18.04 e 19.10

> [!NOTE]
> Para instalar o PHP 7.2 ou 7.3, substitua o 7.4 por 7.2 ou por 7.3 nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
```bash
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.4 php7.4-dev php7.4-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instalar pré-requisitos
Instale o driver ODBC para Ubuntu seguindo as instruções na [página de instalação de Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instalar os drivers PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```

Caso haja somente uma versão do PHP no sistema, a última etapa poderá ser simplificada para `phpenmod sqlsrv pdo_sqlsrv`.

### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
sudo su
apt-get install libapache2-mod-php7.4 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.4
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reiniciar o Apache e testar o script de amostra
```
sudo service apache2 restart
```
Para testar sua instalação, confira [Testar a instalação](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-with-php-fpm-on-ubuntu"></a>Como instalar os drivers com PHP-FPM no Ubuntu

> [!NOTE]
> Para instalar o PHP 7.2 ou 7.3, substitua o 7.4 por 7.2 ou por 7.3 nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
```bash
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.4 php7.4-dev php7.4-xml php7.4-fpm -y --allow-unauthenticated
```
Verifique o status de serviço do PHP-FPM ao executar
```
systemctl status php7.4-fpm
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instalar pré-requisitos
Instale o driver ODBC para Ubuntu seguindo as instruções na [página de instalação de Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instalar os drivers PHP para Microsoft SQL Server
```
sudo pecl config-set php_ini /etc/php/7.3/fpm/php.ini
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```
Caso haja somente uma versão do PHP no sistema, a última etapa poderá ser simplificada para `phpenmod sqlsrv pdo_sqlsrv`.

Verifique se `sqlsrv.ini` e `pdo_sqlsrv.ini` estão localizados em `/etc/php/7.4/fpm/conf.d/`:
```
ls /etc/php/7.4/fpm/conf.d/*sqlsrv.ini
```
Reinicie o serviço do PHP-FPM:
```
sudo systemctl restart php7.4-fpm
```

### <a name="step-4-install-and-configure-nginx"></a>Etapa 4. Instalar e configurar o nginx
```
sudo apt-get update
sudo apt-get install nginx
sudo systemctl status nginx
```
Para configurar o nginx será necessário editar o arquivo `/etc/nginx/sites-available/default`. Adicione `index.php` à lista abaixo da seção com o texto `# Add index.php to the list if you are using PHP`:
```
# Add index.php to the list if you are using PHP
index index.html index.htm index.nginx-debian.html index.php;
```
Em seguida, modifique a seguinte seção `# pass PHP scripts to FastCGI server` da seguinte maneira:
```
# pass PHP scripts to FastCGI server
#
location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;
}
```
### <a name="step-5-restart-nginx-and-test-the-sample-script"></a>Etapa 5. Reiniciar o nginx e testar o script de exemplo
```
sudo systemctl restart nginx.service
```
Para testar sua instalação, confira [Testar a instalação](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-on-red-hat-7-and-8"></a>Como instalar os drivers no Red Hat 7 e 8

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP

Para instalar o PHP no Red Hat 7, execute o seguinte:
> [!NOTE]
> Para instalar o PHP 7.2 ou 7.3, substitua remi-php74 por remi-php72 ou por remi-php73, respectivamente, nos comandos a seguir.
```
sudo su
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php74
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```

Para instalar o PHP no Red Hat 8, execute o seguinte:
> [!NOTE]
> Para instalar o PHP 7.2 ou 7.3, substitua remi-7.4 por remi-7.2 ou por remi-7.3, respectivamente, nos comandos a seguir.
```
sudo su
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
dnf install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
dnf install yum-utils
dnf module reset php
dnf module install php:remi-7.4
subscription-manager repos --enable codeready-builder-for-rhel-8-x86_64-rpms
dnf update
dnf install php-pdo php-pear php-devel
```

### <a name="step-2-install-prerequisites"></a>Etapa 2. Instalar pré-requisitos
Instale o driver ODBC para Red Hat 7 ou 8 seguindo as instruções na [Página de instalação do Linux e do macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instalar os drivers PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```

Como alternativa é possível instalar usando o repositório Remi:
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

## <a name="installing-the-drivers-on-debian-8-9-and-10"></a>Como instalar os drivers no Debian 8, 9 e 10

> [!NOTE]
> Para instalar o PHP 7.2 ou 7.3, substitua 7.4 por 7.2 ou por 7.3 nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.4 php7.4-dev php7.4-xml php7.4-intl
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instalar pré-requisitos
Instale o driver ODBC para Debian seguindo as instruções na [página de instalação de Linux e macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Você também precisa gerar a localidade correta para que uma saída PHP seja exibida corretamente em um navegador. Por exemplo, para a localidade en_US UTF-8, execute os seguintes comandos:
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```
Talvez seja necessário adicionar `/usr/sbin` ao seu `$PATH`, já que o `locale-gen` executável está localizado lá.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instalar os drivers PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```

Caso haja somente uma versão do PHP no sistema, a última etapa poderá ser simplificada para `phpenmod sqlsrv pdo_sqlsrv`. Assim como `locale-gen`, `phpenmod` está localizado em `/usr/sbin`, por isso, talvez seja necessário adicionar esse diretório ao seu `$PATH`.

### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
sudo su
apt-get install libapache2-mod-php7.4 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.4
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reiniciar o Apache e testar o script de amostra
```
sudo service apache2 restart
```
Para testar sua instalação, confira [Testar a instalação](#testing-your-installation) no final deste documento.

## <a name="installing-the-drivers-on-suse-12-and-15"></a>Instalar os drivers no Suse 12 e 15

> [!NOTE]
> Nas instruções a seguir, substitua `<SuseVersion>` por sua versão do Suse: se você estiver usando o Suse Enterprise Linux 15, ela será SLE_15 ou SLE_15_SP1. Para o Suse 12, use SLE_12_SP4 (ou acima, se aplicável). Nem todas as versões do PHP estão disponíveis para todas as versões do Suse Linux. Confira `http://download.opensuse.org/repositories/devel:/languages:/php` para ver quais versões do Suse têm a versão padrão do PHP disponível, ou `http://download.opensuse.org/repositories/devel:/languages:/php:/` para ver quais versões do PHP estão disponíveis relativamente às versões do Suse.

> [!NOTE]
> Pacotes para PHP 7.4 não estão disponíveis para o Suse 12. Para instalar o PHP 7.2, substitua a URL do repositório abaixo pela seguinte URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo`.
> Para instalar o PHP 7.3, substitua a URL do repositório abaixo pela seguinte URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php73/<SuseVersion>/devel:languages:php:php73.repo`.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-devel php7-openssl
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

## <a name="installing-the-drivers-on-alpine-311"></a>Como instalar os drivers no Alpine 3.11

> [!NOTE]
> O suporte para Alpine é experimental.

> [!NOTE]
> A versão padrão do PHP é 7.3. Versões alternativas do PHP não estão disponíveis em outros repositórios para o Alpine 3.11. Em vez disso é possível compilar o PHP da origem.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP
Os pacotes PHP para Alpine são encontrados no repositório `edge/community`. Adicione a seguinte linha em `/etc/apt/repositories`, substituindo `<mirror>` pela URL de um espelho do repositório Alpine:
```
http://<mirror>/alpine/edge/community
```
Em seguida, execute:
```
sudo su
apk update
apk add php7 php7-dev php7-pear php7-pdo php7-openssl autoconf make g++
```
### <a name="step-2-install-prerequisites"></a>Etapa 2. Instalar pré-requisitos
Instale o driver ODBC para Alpine seguindo as instruções na [Página de instalação do Linux e do macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Etapa 3. Instalar os drivers PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/10_pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/00_sqlsrv.ini
```
Talvez seja necessário definir uma localidade:
```
export LC_ALL=C
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Etapa 4. Instalar o Apache e configurar o carregamento do driver
```
sudo apk add php7-apache2 apache2
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reiniciar o Apache e testar o script de amostra
```
sudo rc-service apache2 restart
```
Para testar sua instalação, confira [Testar a instalação](#testing-your-installation) no final deste documento.


## <a name="installing-the-drivers-on-macos-high-sierra-mojave-and-catalina"></a>Como instalar os drivers no macOS High Sierra, no Mojave e no Catalina

Se você ainda não fez isso, instale o brew da seguinte maneira:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> Para instalar o PHP 7.2 ou 7.3, substitua php@7.4 por php@7.2 ou por php@7.3, respectivamente, nos comandos a seguir.

### <a name="step-1-install-php"></a>Etapa 1. Instalar o PHP

```
brew tap
brew tap homebrew/core
brew install php@7.4
```
O PHP já deve estar no seu caminho: execute `php -v` para verificar se você está executando a versão correta do PHP. Se o PHP não está no seu caminho ou não tem a versão correta, execute o seguinte:
```
brew link --force --overwrite php@7.4
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
Para localizar o arquivo de configuração `httpd.conf` para a instalação do Apache, execute 
```
/usr/local/bin/apachectl -V | grep SERVER_CONFIG_FILE
``` 
Os comandos a seguir acrescentam a configuração necessária para `httpd.conf`. Certifique-se de substituir o caminho retornado pelo comando anterior no lugar de `/usr/local/etc/httpd/httpd.conf`:
```
echo "LoadModule php7_module /usr/local/opt/php@7.4/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Etapa 5. Reiniciar o Apache e testar o script de amostra
```
sudo apachectl restart
```
Para testar sua instalação, confira [Testar a instalação](#testing-your-installation) no final deste documento.

## <a name="testing-your-installation"></a>Testar a instalação

Para testar esta amostra de script, crie um arquivo chamado testsql.php na raiz do documento do seu sistema. Ou seja, `/var/www/html/` no Ubuntu, no Debian e no RedHat, `/srv/www/htdocs` no SUSE, `/var/www/localhost/htdocs` no Alpine ou `/usr/local/var/www` no macOS. Copie o script a seguir para esse arquivo, substituindo o servidor, o banco de dados, o nome de usuário e a senha, conforme apropriado. No Alpine 3.11, talvez seja necessário especificar também **CharacterSet** como "UTF-8" na matriz de `$connectionOptions`.
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
