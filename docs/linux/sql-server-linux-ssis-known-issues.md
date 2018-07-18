---
title: Limitações e problemas conhecidos do SSIS no Linux | Microsoft Docs
description: Este artigo descreve as limitações e problemas conhecidos para o SQL Server Integration Services (SSIS) em computadores Linux
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 06/06/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 33f798fd3b7816cae61137292392cb9cca729ec7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020595"
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Limitações e problemas conhecidos do SSIS no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve as limitações e problemas conhecidos para o SQL Server Integration Services (SSIS) no Linux.

## <a name="general-limitations-and-known-issues"></a>Problemas conhecidos e limitações gerais

Os recursos a seguir não têm suporte nesta versão do SSIS no Linux:
  - Banco de dados de catálogo do SSIS
  - Execução de pacotes agendados pelo SQL Agent
  - Autenticação do Windows
  - Componentes de terceiros
  - Change Data Capture (CDC)
  - SSIS Scale Out
  - Azure Feature Pack para SSIS
  - Suporte de Hadoop e HDFS
  - Microsoft Connector for SAP BW

Para outras limitações e problemas conhecidos com o SSIS no Linux, consulte o [notas de versão](sql-server-linux-release-notes.md#ssis).

## <a name="components"></a> Componentes compatíveis e sem suportados

Os seguintes componentes internos do Integration Services têm suporte no Linux. Alguns deles têm limitações na plataforma Linux. Componentes internos que não estão listados aqui não têm suporte no Linux.

## <a name="supported-control-flow-tasks"></a>Suporte para tarefas de fluxo de controle
- Tarefa Inserção em Massa
- Tarefa de Fluxo de Dados
- Tarefa Criação de Perfil de Dados
- Tarefa Executar SQL
- Tarefa Executar Instrução T-SQL
- Tarefa de Expressão
- Tarefa FTP
- Tarefa Serviços Web
- XML Task

## <a name="control-flow-tasks-supported-with-limitations"></a>Tarefas de fluxo de controle compatíveis com limitações

| Tarefa | Limitações |
|------------|---|
| Tarefa executar processo | Só dá suporte ao modo em processo. |
| Tarefa sistema de arquivos | O *diretório de movimentação* e *definir atributos de arquivo* ações não têm suporte. |
| tarefa Script | Só dá suporte a APIs padrão do .NET Framework. |
| Tarefa Enviar Email | Só dá suporte ao modo de usuário anônimo. |
| Tarefa de transferência de banco de dados | Não há suporte para caminhos UNC. |
| | |

## <a name="supported-and-unsupported-maintenance-plan-tasks"></a>Tarefas do plano de manutenção com e sem suporte

Em um plano de manutenção do SQL Server, normalmente você pode usar uma variedade de tarefas do SSIS.

Não há suporte para as seguintes tarefas de plano de manutenção no Linux:
- Notificar operador
- Executar trabalho do SQL Server Agent

As seguintes tarefas de plano de manutenção têm suporte no Linux:
- Verificar integridade do banco de dados
- Reduzir banco de dados
- Reorganizar Índice
- Recriar índice
- Atualização de Estatísticas
- Limpar histórico
- Fazer backup de banco de dados
- Instrução T-SQL

## <a name="supported-control-flow-containers"></a>Suporte para contêineres de fluxo de controle
- Contêiner de sequência
- Contêiner Loop For
- Contêiner Loop Foreach

## <a name="supported-data-flow-sources-and-destinations"></a>Fontes de fluxo de dados com suporte e destinos
- Destino e origem do arquivo bruto
- Origem XML

## <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>Fontes de fluxo de dados e destinos com suporte com limitações

| Componente | Limitações |
|------------|---|
| Destino e origem do ADO.NET | Só há suporte para o provedor de dados SQLClient. |
| Fonte de arquivo simples e de destino | Suportam apenas caminhos de arquivo de estilo do Windows, ao qual a regra de mapeamento de caminho padrão é aplicada. Por exemplo `D:\home\ssis\travel.csv` torna-se `/home/ssis/travel.csv`. |
| Origem do OData | Só dá suporte à autenticação básica. |
| Origem e destino ODBC | Dá suporte a drivers de ODBC Unicode de 64 bits no Linux. Depende do Gerenciador de driver UnixODBC no Linux. |
| Destino e origem de OLE DB | Apenas suporte do SQL Server Native Client 11.0 e o Microsoft OLE DB Provider para SQL Server. |
| | |

## <a name="supported-data-flow-transformations"></a>Transformações de fluxo de dados com suporte
- Agregado
- Auditar o
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

## <a name="data-flow-transformations-supported-with-limitations"></a>Transformações de fluxo de dados compatíveis com limitações

| Componente | Limitações |
|------------|---|
| transformação Comando OLE DB | Mesmas limitações que a origem de OLE DB e o destino. |
| componente Script | Só dá suporte a APIs padrão do .NET Framework. |
| | |

## <a name="supported-and-unsupported-log-providers"></a>Provedores de log com e sem suporte
Todos os provedores de log SSIS internos têm suporte no Linux, exceto o provedor de Log de eventos do Windows.

O provedor de log do SQL Server oferece suporte somente a autenticação do SQL; ele não oferece suporte a autenticação do Windows.

Os provedores de log do SSIS para arquivos de texto, arquivos XML e SQL Server Profiler gravam sua saída para um arquivo que você especifica. As seguintes considerações se aplicam ao caminho do arquivo:
-   Se você não fornecer um caminho, o provedor de log gravará no diretório atual do host. Se o usuário atual não tem permissão para gravar no diretório atual do host, o provedor de log gera um erro.
-   Você não pode usar uma variável de ambiente em um caminho de arquivo. Se você especificar uma variável de ambiente, o texto literal que você especifica será exibida no caminho do arquivo. Por exemplo, se você especificar `%TMP%/log.txt`, o provedor de log acrescenta o texto literal `/%TMP%/log.txt` para o diretório do host atual.

## <a name="related-content-about-ssis-on-linux"></a>Conteúdo relacionado sobre SSIS no Linux
-   [Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)
-   [Instalar o SQL Server Integration Services (SSIS) no Linux](sql-server-linux-setup-ssis.md)
-   [Configurar o SQL Server Integration Services no Linux com o ssis-conf](sql-server-linux-configure-ssis.md)
-   [SQL Server Integration Services de agenda a execução no Linux com cron do pacote](sql-server-linux-schedule-ssis-packages.md)
