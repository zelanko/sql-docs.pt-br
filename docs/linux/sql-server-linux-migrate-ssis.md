---
title: Extrair, transformar e carregar dados no Linux com o SSIS
description: Este artigo descreve o SSIS (SQL Server Integration Services) para computadores Linux
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e6230ee4efebc4b1af873a61e9f2ebfc191df171
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67943814"
---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>Extrair, transformar e carregar dados no Linux com o SSIS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve como executar pacotes SSIS (SQL Server Integration Services) no Linux. O SSIS resolve problemas complexos de integração de dados extraindo dados de várias fontes e formatos, transformando-s e limpando-os e carregando-os dados em vários destinos. 

Os pacotes SSIS em execução no Linux podem conectar-se ao Microsoft SQL Server em execução no Windows local ou na nuvem ou no Linux ou no Docker. Eles também podem se conectar ao Banco de Dados SQL do Azure, ao SQL Data Warehouse do Azure, a fontes de dados ODBC, a arquivos simples e a outras fontes, incluindo fontes do ADO.NET, arquivos XML e serviços OData.

Para obter mais informações sobre as funcionalidades do SSIS, confira o [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).

## <a name="prerequisites"></a>Prerequisites

Para executar pacotes SSIS em um computador Linux, primeiro é necessário instalar o SQL Server Integration Services. O SSIS não está incluído na instalação do SQL Server para computadores Linux. Para obter instruções sobre a instalação, confira [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md).

Você também precisar ter um computador Windows para criar e manter pacotes. As ferramentas de design e de gerenciamento do SSIS são aplicativos Windows que não estão disponíveis para computadores Linux no momento. 

## <a name="run-an-ssis-package"></a>Executar um pacote SSIS

Para executar um pacote SSIS em um computador Linux, faça o seguinte:

1.  Copie o pacote SSIS para o computador Linux.
2.  Execute o comando a seguir:
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="run-an-encrypted-password-protected-package"></a>Executar um pacote criptografado (protegido por senha)
Há três maneiras de executar um pacote SSIS criptografado com uma senha:

1.  Defina o valor da variável de ambiente `SSIS_PACKAGE_DECRYPT`, conforme mostrado no exemplo a seguir:

    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  Especifique a opção `/de[crypt]` para inserir a senha interativamente, conforme mostrado no exemplo a seguir:

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de
    
    Enter decryption password:
    ```

3.  Especifique a opção `/de` para fornecer a senha na linha de comando, conforme mostrado no exemplo a seguir. Esse método não é recomendado, porque ele armazena a senha de descriptografia com o comando no histórico de comandos.

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test
    
    Warning: Using /De[crypt] <password> may store decryption password in command history.
    
    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

## <a name="design-packages"></a>Criar pacotes

**Conectar-se a fontes de dados ODBC**. Com o SSIS na Atualização CTP 2.1 do Linux e posterior, os pacotes SSIS podem usar conexões ODBC no Linux. Essa funcionalidade foi testada com o SQL Server e os drivers ODBC do MySQL, mas também espera-se que ela funcione com qualquer driver ODBC Unicode que observa a especificação ODBC. Em tempo de design, é possível fornecer um DSN ou uma cadeia de conexão para conectar-se aos dados ODBC; também é possível usar a autenticação do Windows. Para saber mais, confira a [postagem no blog que anunciou o suporte do ODBC para Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

**Caminhos**. Forneça caminhos no estilo do Windows em seus pacotes SSIS. O SSIS no Linux não dá suporte a caminhos no estilo do Linux, mas mapeia os caminhos no estilo do Windows para caminhos no estilo do Linux em tempo de execução. Em seguida, por exemplo, o SSIS no Linux mapeia o caminho `C:\test` no estilo do Windows para o caminho `/test` no estilo do Linux.

## <a name="deploy-packages"></a>Implantar pacotes
Só é possível armazenar pacotes no sistema de arquivos no Linux nesta versão. O banco de dados do Catálogo do SSIS e o serviço SSIS herdado não estão disponíveis no Linux para a implantação e o armazenamento de pacotes.

## <a name="schedule-packages"></a>Agendar pacotes
É possível usar as ferramentas de agendamento do sistema Linux, como `cron`, para agendar pacotes. Não é possível usar o SQL Agent no Linux para agendar a execução de pacotes nesta versão. Para obter mais informações, confira [Agendar pacotes SSIS no Linux com cron](sql-server-linux-schedule-ssis-packages.md).

## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

Para obter informações detalhadas sobre as limitações e problemas conhecidos do SSIS no Linux, confira [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md).

## <a name="more-info-about-ssis-on-linux"></a>Mais informações sobre o SSIS no Linux

Para obter mais informações sobre o SSIS no Linux, confira as seguintes postagens no blog:

-   [Os SSIS no Linux está disponível no SQL Server CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [O ODBC é compatível com o SSIS no Linux (SQL Server atualização CTP 2.1)](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>Mais informações sobre o SSIS

O Microsoft SSIS (SQL Server Integration Services) é uma plataforma para a criação de soluções de integração de dados de alto desempenho, incluindo os pacotes ETL (extração, transformação e carregamento) para armazenamento de dados. Para obter mais informações sobre SSIS, consulte [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services).

O SSIS inclui os seguintes recursos:
- Ferramentas gráficas e assistentes para criar e depurar pacotes no Windows
- Uma variedade de tarefas para realizar funções de fluxo de trabalho, como operações FTP, executar instruções SQL e enviar mensagens de email
- Uma variedade de fontes de dados e destinos para extrair e carregar dados
- Uma variedade de transformações para limpeza, agregação, mesclagem e cópia de dados
- APIs (interfaces de programação de aplicativo) para estender o SSIS com seus próprios componentes e scripts personalizados

Para começar a usar o SSIS, baixe a versão mais recente do [SSDT (SQL Server Data Tools)](../integration-services/ssis-how-to-create-an-etl-package.md).

Para saber mais sobre o SSIS, confira os seguintes artigos:
- [Saiba mais sobre o SQL Server Integration Services](../integration-services/sql-server-integration-services.md)
- [Ferramentas de Desenvolvimento e de Gerenciamento do SSIS (SQL Server Integration Services)](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [Tutoriais do SQL Server Integration Services](../integration-services/integration-services-tutorials.md)

## <a name="related-content-about-ssis-on-linux"></a>Conteúdo relacionado sobre o SSIS no Linux
-   [Instalar o SSIS (SQL Server Integration Services) no Linux](sql-server-linux-setup-ssis.md)
-   [Configurar o SQL Server Integration Services no Linux com ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md)
-   [Agendar a execução de pacotes do SQL Server Integration Services no Linux com cron](sql-server-linux-schedule-ssis-packages.md)
