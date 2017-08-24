---
title: Extrair, transformar e carregar dados em Linux com o SSIS | Microsoft Docs
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d7317cad5aa1e77653431c128ce1549bc4349e18
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>Extrair, transformar e carregar dados em Linux com o SSIS

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

Este tópico descreve como executar pacotes do SQL Server Integration Services (SSIS) no Linux. SSIS resolve problemas de integração de dados complexos, carregar dados de várias fontes e formatos, transformar e limpar os dados e atualizando vários destinos. 

Pacotes do SSIS em execução no Linux podem se conectar ao Microsoft SQL Server em execução no Windows local ou na nuvem, no Linux ou no Docker. Eles também possam se conectar ao banco de dados do SQL Azure, Azure SQL Data Warehouse e fontes de dados ODBC.

Você pode usar o SSIS para executar pacotes no Linux, quando você também tem um computador com Windows para criar e manter pacotes. As ferramentas de design e gerenciamento do SSIS são aplicativos do Windows. 

## <a name="prerequisites"></a>Pré-requisitos

Para executar pacotes SSIS em um computador Linux, primeiro você precisa instalar o SQL Server Integration Services. Para obter instruções de instalação, consulte [instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md).

## <a name="run-an-ssis-package"></a>Executar um pacote do SSIS

Para executar um pacote do SSIS em um computador Linux, faça o seguinte:

1.  Copie o pacote do SSIS para o computador Linux.
2.  Execute o seguinte comando:
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="more-about-ssis-on-linux"></a>Mais sobre o SSIS no Linux

**Conexões ODBC**. Com o SSIS, sobre a atualização do Linux CTP 2.1 e posterior, os pacotes do SSIS podem usar conexões ODBC no Linux. Essa funcionalidade foi testada com o SQL Server e os drivers ODBC MySQL, mas também é esperada para funcionar com qualquer driver de ODBC Unicode que observa a especificação de ODBC. Em tempo de design, você pode fornecer um DSN ou uma cadeia de caracteres de conexão para conectar-se aos dados de ODBC; Você também pode usar a autenticação do Windows. Para obter mais informações, consulte o [postagem do blog anunciar suporte a ODBC no Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

**Caminhos**. SSIS no Linux não oferece suporte a caminhos de estilo do Linux, mas mapeia caminhos no estilo do Windows para caminhos no estilo do Linux em tempo de execução. Fornece caminhos de estilo do Windows em seus pacotes SSIS. Em seguida, por exemplo, o SSIS no Linux mapeia o caminho de estilo do Windows `C:\test` para o caminho de estilo de Linux `/test`.

**Implantando pacotes**. Você só pode armazenar pacotes no sistema de arquivos Linux nesta versão. O banco de dados de catálogo do SSIS e o serviço SSIS herdado não estão disponíveis no Linux para o armazenamento e a implantação do pacote.

**Agendando pacotes**. Você não pode usar o SQL Agent no Linux para agendar a execução de pacote nesta versão.

**Outras limitações e problemas conhecidos**. Os recursos a seguir não têm suporte nesta versão, quando você executar pacotes SSIS no Linux:
  - Banco de dados de catálogo do SSIS
  - Execução de pacotes agendados pelo SQL Agent
  - Autenticação do Windows
  - Componentes de terceiros
  - Change Data Capture (CDC)
  - Expansão do SSIS
  - Azure Feature Pack para SSIS
  - Suporte de Hadoop e HDFS
  - Microsoft Connector for SAP BW

Para outras limitações e problemas conhecidos com o SSIS no Linux, consulte o [notas de versão](sql-server-linux-release-notes.md#ssis).

Para obter mais informações sobre o SSIS no Linux, consulte as postagens de blog a seguir:

-   [SSIS no Linux está disponível no SQL Server de 2017 CTP 2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [Há suporte para o ODBC no SSIS no Linux (atualização do SQL Server de 2017 CTP 2.1)](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-about-ssis"></a>Mais sobre o SSIS

Microsoft SQL Server Integration Services (SSIS) é uma plataforma para criar soluções de integração de dados de alto desempenho, incluindo a extração, transformação e carregamento (ETL) pacotes para data warehouse. Para obter mais informações sobre SSIS, consulte [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md).

SSIS inclui os seguintes recursos:
- ferramentas gráficas e assistentes para compilar e depurar pacotes no Windows
- uma variedade de tarefas para executar funções de fluxo de trabalho, como operações de FTP, execução de instruções SQL e enviar mensagens de email
- uma variedade de fontes de dados e destinos para extração e carregamento de dados
- uma variedade de transformações para limpeza, agregação, mesclagem e copiando dados
- interfaces de programação de aplicativo (APIs) para estender o SSIS com seus próprios scripts personalizados e componentes

Para começar a usar o SSIS, baixe a versão mais recente do [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md). Em seguida, siga o tutorial [como SSIS para criar um pacote de ETL](https://msdn.microsoft.com/en-us/library/ms169917.aspx).

## <a name="see-also"></a>Consulte também
- [Saiba mais sobre o SQL Server Integration Services](https://msdn.microsoft.com/en-us/library/ms141026.aspx)
- [Ferramentas de gerenciamento e desenvolvimento do SQL Server Integration Services (SSIS)](https://msdn.microsoft.com/en-us/library/ms140028.aspx)
- [Tutoriais do SQL Server Integration Services](https://msdn.microsoft.com/en-us/library/jj720568.aspx)

