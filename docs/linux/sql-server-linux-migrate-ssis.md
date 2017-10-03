---
title: Extrair, transformar e carregar dados em Linux com o SSIS | Microsoft Docs
description: 
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: aa4ac0cca739ea57a28beb399325d55b38502217
ms.contentlocale: pt-br
ms.lasthandoff: 10/02/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>Extrair, transformar e carregar dados em Linux com o SSIS

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este tópico descreve como executar pacotes do SQL Server Integration Services (SSIS) no Linux. SSIS soluciona problemas de integração de dados complexos, extrair dados de várias fontes e formatos, transformar e limpar os dados e carregar os dados em vários destinos. 

Pacotes do SSIS em execução no Linux podem se conectar ao Microsoft SQL Server em execução no Windows local ou na nuvem, no Linux ou no Docker. Eles também possam se conectar ao banco de dados do SQL Azure, Azure SQL Data Warehouse, fontes de dados ODBC, arquivos simples e outras fontes de dados, incluindo fontes do ADO.NET, arquivos XML e serviços OData.

Para obter mais informações sobre os recursos do SSIS, consulte [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).

## <a name="prerequisites"></a>Pré-requisitos

Para executar pacotes SSIS em um computador Linux, primeiro você precisa instalar o SQL Server Integration Services. O SSIS não está incluído na instalação do SQL Server para computadores Linux. Para obter instruções de instalação, consulte [instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md).

Você também precisa ter um computador com Windows para criar e manter pacotes. As ferramentas de design e gerenciamento do SSIS são aplicativos do Windows que não estão atualmente disponíveis para computadores Linux. 

## <a name="run-an-ssis-package"></a>Executar um pacote do SSIS

Para executar um pacote do SSIS em um computador Linux, faça o seguinte:

1.  Copie o pacote do SSIS para o computador Linux.
2.  Execute o seguinte comando:
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="other-common-ssis-tasks"></a>Outras tarefas comuns do SSIS

-   **Criar pacotes**.

    -   **Conecte-se a fontes de dados ODBC**. Com o SSIS, sobre a atualização do Linux CTP 2.1 e posterior, os pacotes do SSIS podem usar conexões ODBC no Linux. Essa funcionalidade foi testada com o SQL Server e os drivers ODBC MySQL, mas também é esperada para funcionar com qualquer driver de ODBC Unicode que observa a especificação de ODBC. Em tempo de design, você pode fornecer um DSN ou uma cadeia de caracteres de conexão para conectar-se aos dados de ODBC; Você também pode usar a autenticação do Windows. Para obter mais informações, consulte o [postagem do blog anunciar suporte a ODBC no Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

    -   **Caminhos**. Fornece caminhos de estilo do Windows em seus pacotes SSIS. SSIS no Linux não oferece suporte a caminhos de estilo do Linux, mas mapeia caminhos no estilo do Windows para caminhos no estilo do Linux em tempo de execução. Em seguida, por exemplo, o SSIS no Linux mapeia o caminho de estilo do Windows `C:\test` para o caminho de estilo de Linux `/test`.

-   **Implantar pacotes**. Você só pode armazenar pacotes no sistema de arquivos Linux nesta versão. O banco de dados de catálogo do SSIS e o serviço SSIS herdado não estão disponíveis no Linux para o armazenamento e a implantação do pacote.

-   **Agendar pacotes**. Você pode usar o sistema do Linux, como ferramentas de agendamento `cron` para agendar pacotes. Você não pode usar o SQL Agent no Linux para agendar a execução de pacote nesta versão. Para obter mais informações, consulte [pacotes do SSIS de agenda em Linux com cron](sql-server-linux-schedule-ssis-packages.md).

## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

### <a name="general-limitations-and-known-issues"></a>Problemas conhecidos e limitações gerais

Os recursos a seguir não têm suporte nesta versão do SSIS no Linux:
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

### <a name="components"></a>Componentes compatíveis e sem suportados

Os seguintes componentes internos do Integration Services têm suporte no Linux. Algumas delas têm limitações na plataforma Linux, conforme descrito nas tabelas a seguir.

Componentes internos que não estão listados aqui não têm suporte no Linux.

#### <a name="supported-control-flow-tasks"></a>Suporte para tarefas de fluxo de controle
- Tarefa Inserção em Massa
- Tarefa de Fluxo de Dados
- Tarefa Criação de Perfil de Dados
- Tarefa Executar SQL
- Tarefa Executar Instrução T-SQL
- Tarefa de Expressão
- Tarefa FTP
- Tarefa Serviços Web
- XML Task

#### <a name="control-flow-tasks-supported-with-limitations"></a>Tarefas de fluxo de controle compatíveis com limitações

| Tarefa | Limitações |
|------------|---|
| Tarefa executar processo | Só dá suporte ao modo em processo. |
| Tarefa sistema de arquivos | O *mover diretório* e *definir atributos de arquivo* ações não têm suporte. |
| tarefa Script | Só oferece suporte a APIs padrão do .NET Framework. |
| Tarefa Enviar Email | Só dá suporte ao modo de usuário anônimo. |
| Tarefa de transferência de banco de dados | Não há suporte para caminhos UNC. |
| | |

#### <a name="supported-control-flow-containers"></a>Suporte para contêineres de fluxo de controle
- Contêiner de sequência
- Contêiner Loop For
- Contêiner Loop Foreach

#### <a name="supported-data-flow-sources-and-destinations"></a>Fontes de fluxo de dados com suporte e destinos
- Destino e origem arquivo bruto
- Origem XML

#### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>Fluxo de dados origens e destinos compatíveis com limitações

| Componente | Limitações |
|------------|---|
| Destino e origem do ADO.NET | Suportam apenas o provedor de dados SQLClient. |
| Fonte de arquivo simples e de destino | Somente dão suporte a caminhos de arquivo de estilo do Windows, aos quais a regra de mapeamento de caminho padrão é aplicada. Por exemplo `D:\home\ssis\travel.csv` torna-se `/home/ssis/travel.csv`. |
| Fonte OData | Suporta apenas a autenticação básica. |
| Origem ODBC e destino | Dá suporte a drivers de ODBC Unicode de 64 bits no Linux. Depende do Gerenciador de driver UnixODBC no Linux. |
| Origem de OLE DB e de destino | Apenas suporte do SQL Server Native Client 11.0 e o Microsoft OLE DB Provider para SQL Server. |
| | |

#### <a name="supported-data-flow-transformations"></a>Suporte para transformações de fluxo de dados
- Agregado
- Auditoria
- Balanced Data Distributor
- Mapa de Caracteres
- Divisão Condicional
- Copiar Coluna
- Conversão de Dados
- Coluna Derivada
- Exportar Coluna
- Agrupamento Difuso
- Pesquisa Difusa
- Importar Coluna
- Pesquisar
- Mesclagem
- Junção de Mesclagem
- Multicast
- Dinâmico
- Contagem de Linhas
- Dimensão de Alteração Lenta
- Sort
- Pesquisa de Termos
- Union All
- Não Dinâmico

#### <a name="data-flow-transformations-supported-with-limitations"></a>Transformações de fluxo de dados compatíveis com limitações

| Componente | Limitações |
|------------|---|
| transformação Comando OLE DB | Mesmas limitações que a origem de OLE DB e o destino. |
| componente Script | Só oferece suporte a APIs padrão do .NET Framework. |
| | |

### <a name="supported-and-unsupported-log-providers"></a>Provedores de log com e sem suporte
Todos os provedores internos de log do SSIS têm suporte no Linux, exceto o provedor de Log de eventos do Windows.

O provedor de log do SQL Server oferece suporte somente a autenticação do SQL; ele não dá suporte a autenticação do Windows.

Os provedores de log do SSIS para arquivos de texto, arquivos XML e SQL Server Profiler gravar sua saída em um arquivo que você especificar. As seguintes considerações se aplicam ao caminho do arquivo:
-   Se você não fornecer um caminho, o provedor de log grava no diretório atual do host. Se o usuário atual não tem permissão para gravar no diretório atual do host, o provedor de log gera um erro.
-   Você não pode usar uma variável de ambiente em um caminho de arquivo. Se você especificar uma variável de ambiente, o texto literal que você especificar será exibida no caminho do arquivo. Por exemplo, se você especificar `%TMP%/log.txt`, o provedor de log anexa o texto literal `/%TMP%/log.txt` para o diretório de host atual.

## <a name="more-info-about-ssis-on-linux"></a>Para obter mais informações sobre o SSIS no Linux

Para obter mais informações sobre o SSIS no Linux, consulte as postagens de blog a seguir:

-   [SSIS no Linux está disponível no SQL Server de 2017 CTP 2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [Há suporte para o ODBC no SSIS no Linux (atualização do SQL Server de 2017 CTP 2.1)](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>Para obter mais informações sobre o SSIS

Microsoft SQL Server Integration Services (SSIS) é uma plataforma para criar soluções de integração de dados de alto desempenho, incluindo a extração, transformação e carregamento (ETL) pacotes para data warehouse. Para obter mais informações sobre SSIS, consulte [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md).

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

