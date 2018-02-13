---
title: Extrair, transformar e carregar dados em Linux com o SSIS | Microsoft Docs
description: Este artigo descreve o SQL Server Integration Services (SSIS) para computadores Linux
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 01/09/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 40699608d068895cdcee736c87aa4c2bd405b807
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2018
---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>Extrair, transformar e carregar dados em Linux com o SSIS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve como executar pacotes do SQL Server Integration Services (SSIS) no Linux. SSIS soluciona problemas de integração de dados complexos, extrair dados de várias fontes e formatos, transformar e limpar os dados e carregar os dados em vários destinos. 

Pacotes do SSIS em execução no Linux podem se conectar ao Microsoft SQL Server em execução no Windows local ou na nuvem, no Linux ou no Docker. Eles também possam se conectar ao banco de dados do SQL Azure, Azure SQL Data Warehouse, fontes de dados ODBC, arquivos simples e outras fontes de dados, incluindo fontes do ADO.NET, arquivos XML e serviços OData.

Para obter mais informações sobre os recursos do SSIS, consulte [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).

## <a name="prerequisites"></a>Prerequisites

Para executar pacotes SSIS em um computador Linux, primeiro você precisa instalar o SQL Server Integration Services. O SSIS não está incluído na instalação do SQL Server para computadores Linux. Para obter instruções de instalação, consulte [instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md).

Você também precisa ter um computador com Windows para criar e manter pacotes. As ferramentas de design e gerenciamento do SSIS são aplicativos do Windows que não estão atualmente disponíveis para computadores Linux. 

## <a name="run-an-ssis-package"></a>Executar um pacote do SSIS

Para executar um pacote do SSIS em um computador Linux, faça o seguinte:

1.  Copie o pacote do SSIS para o computador Linux.
2.  Execute o seguinte comando:
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="run-an-encrypted-password-protected-package"></a>Executar um pacote criptografado (protegido por senha)
Há três maneiras de executar um pacote do SSIS é criptografado com uma senha:

1.  Defina o valor da variável de ambiente `SSIS_PACKAGE_DECRYPT`, conforme mostrado no exemplo a seguir:

    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  Especifique o `/de[crypt]` opção para digitar a senha interativamente, conforme mostrado no exemplo a seguir:

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de
    
    Enter decryption password:
    ```

3.  Especifique o `/de` opção para fornecer a senha na linha de comando, conforme mostrado no exemplo a seguir. Esse método não é recomendado porque ele armazena a senha de descriptografia com o comando no histórico de comandos.

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test
    
    Warning: Using /De[crypt] <password> may store decryption password in command history.
    
    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

## <a name="design-packages"></a>Criar pacotes

**Conecte-se a fontes de dados ODBC**. Com o SSIS, sobre a atualização do Linux CTP 2.1 e posterior, os pacotes do SSIS podem usar conexões ODBC no Linux. Essa funcionalidade foi testada com o SQL Server e os drivers ODBC MySQL, mas também é esperada para funcionar com qualquer driver de ODBC Unicode que observa a especificação de ODBC. Em tempo de design, você pode fornecer um DSN ou uma cadeia de caracteres de conexão para conectar-se aos dados de ODBC; Você também pode usar a autenticação do Windows. Para obter mais informações, consulte o [postagem do blog anunciar suporte a ODBC no Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

**Caminhos**. Fornece caminhos de estilo do Windows em seus pacotes SSIS. SSIS no Linux não oferece suporte a caminhos de estilo do Linux, mas mapeia caminhos no estilo do Windows para caminhos no estilo do Linux em tempo de execução. Em seguida, por exemplo, o SSIS no Linux mapeia o caminho de estilo do Windows `C:\test` para o caminho de estilo de Linux `/test`.

## <a name="deploy-packages"></a>Implantar pacotes
Você só pode armazenar pacotes no sistema de arquivos Linux nesta versão. O banco de dados de catálogo do SSIS e o serviço SSIS herdado não estão disponíveis no Linux para o armazenamento e a implantação do pacote.

## <a name="schedule-packages"></a>Agendar pacotes
Você pode usar o sistema do Linux, como ferramentas de agendamento `cron` para agendar pacotes. Você não pode usar o SQL Agent no Linux para agendar a execução de pacote nesta versão. Para obter mais informações, consulte [pacotes do SSIS de agenda em Linux com cron](sql-server-linux-schedule-ssis-packages.md).

## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

Para obter informações detalhadas sobre as limitações e problemas conhecidos do SSIS no Linux, consulte [limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md).

## <a name="more-info-about-ssis-on-linux"></a>Para obter mais informações sobre o SSIS no Linux

Para obter mais informações sobre o SSIS no Linux, consulte as postagens de blog a seguir:

-   [SSIS no Linux está disponível no SQL Server de 2017 CTP 2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [Há suporte para o ODBC no SSIS no Linux (atualização do SQL Server de 2017 CTP 2.1)](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>Para obter mais informações sobre o SSIS

Microsoft SQL Server Integration Services (SSIS) é uma plataforma para criar soluções de integração de dados de alto desempenho, incluindo a extração, transformação e carregamento (ETL) pacotes para data warehouse. Para obter mais informações sobre SSIS, consulte [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services).

SSIS inclui os seguintes recursos:
- ferramentas gráficas e assistentes para compilar e depurar pacotes no Windows
- uma variedade de tarefas para executar funções de fluxo de trabalho, como operações de FTP, execução de instruções SQL e enviar mensagens de email
- uma variedade de fontes de dados e destinos para extração e carregamento de dados
- uma variedade de transformações para limpeza, agregação, mesclagem e copiando dados
- interfaces de programação de aplicativo (APIs) para estender o SSIS com seus próprios scripts personalizados e componentes

Para começar a usar o SSIS, baixe a versão mais recente do [SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md).

## <a name="see-also"></a>Consulte também
- [Saiba mais sobre o SQL Server Integration Services](../integration-services/sql-server-integration-services.md)
- [Ferramentas de gerenciamento e desenvolvimento do SQL Server Integration Services (SSIS)](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [Tutoriais do SQL Server Integration Services](../integration-services/integration-services-tutorials.md)
