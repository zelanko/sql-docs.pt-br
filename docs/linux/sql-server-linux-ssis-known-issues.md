---
title: Limitações e problemas conhecidos do SSIS no Linux
description: Este artigo descreve as limitações e os problemas conhecidos do SSIS (SQL Server Integration Services) em computadores Linux
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 06/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 45e5d9b36b6fd75db7bbc3c5ea397ee9226e2771
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78339335"
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Limitações e problemas conhecidos do SSIS no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve as limitações e os problemas conhecidos do SSIS (SQL Server Integration Services) no Linux.

## <a name="general-limitations-and-known-issues"></a>Limitações e problemas conhecidos

Não há suporte para os seguintes recursos nesta versão do SSIS no Linux:
  - Banco de dados do Catálogo do SSIS
  - Execução de pacotes agendada pelo SQL Agent
  - Autenticação do Windows
  - Componentes de terceiros
  - Change Data Capture (CDC)
  - SSIS Scale Out
  - Feature Pack do Azure para SSIS
  - Suporte para Hadoop e HDFS
  - Microsoft Connector for SAP BW

Para conhecer outras limitações e outros problemas conhecidos com o SSIS no Linux, confira as [Notas sobre a versão](sql-server-linux-release-notes.md#ssis).

## <a name="components"></a> Componentes com e sem suporte

Há suporte para os componentes internos do Integration Services a seguir no Linux. Alguns deles têm limitações na plataforma Linux. Os componentes internos que não estão listados aqui não são compatíveis com o Linux.

## <a name="supported-control-flow-tasks"></a>Tarefas de fluxo de controle compatíveis
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
| Tarefa Executar Processo | Só dá suporte ao modo em processo. |
| Tarefa Sistema de Arquivos | Não há suporte para as ações *Mover diretório* e *Definir atributos de arquivo*. |
| tarefa Script | Só dá suporte às APIs padrão do .NET Framework. |
| Tarefa Enviar Email | Só dá suporte ao modo de usuário anônimo. |
| Tarefa Transferir Banco de Dados | Não há suporte para caminhos UNC. |
| | |

## <a name="supported-and-unsupported-maintenance-plan-tasks"></a>Tarefas de plano de manutenção com e sem suporte

Em um plano de manutenção do SQL Server, normalmente, é possível usar uma variedade de tarefas do SSIS.

Não há suporte para as seguintes tarefas de plano de manutenção no Linux:
- Notificar Operador
- Executar Trabalho do SQL Server Agent

Há suporte para as seguintes tarefas de plano de manutenção no Linux:
- Verificar Integridade do Banco de Dados
- Reduzir Banco de Dados
- Reorganizar Índice
- Recompilar Índice
- Atualização de Estatísticas
- Limpar Histórico
- Fazer Backup do Banco de Dados
- Instrução T-SQL

## <a name="supported-control-flow-containers"></a>Contêineres de fluxo de controle compatíveis
- Contêiner de sequência
- Contêiner Loop For
- Contêiner Loop Foreach

## <a name="supported-data-flow-sources-and-destinations"></a>Origens e destinos de fluxo de dados compatíveis
- Fonte Arquivo Bruto e destino
- Origem XML

## <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>Origens e destinos de fluxo de dados compatíveis com limitações

| Componente | Limitações |
|------------|---|
| Origem e destino ADO.NET | Só dá suporte ao provedor de dados SQLClient. |
| Origem e destino Arquivo Simples | Só dá suporte a caminhos de arquivo no estilo Windows, aos quais a regra de mapeamento de caminho padrão é aplicada. Por exemplo, `D:\home\ssis\travel.csv` torna-se `/home/ssis/travel.csv`. |
| Origem OData | Só dá suporte à autenticação Básica. |
| Origem e destino ODBC | Dá suporte a drivers ODBC Unicode de 64 bits no Linux. Depende do gerenciador de driver UnixODBC no Linux. |
| Origem e destino OLE DB | Só dá suporte ao SQL Server Native Client 11.0 e ao Provedor Microsoft OLE DB para SQL Server. |
| | |

## <a name="supported-data-flow-transformations"></a>Transformações de fluxo de dados compatíveis
- Agregado
- Audit
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
- Pesquisa
- Mesclar
- Junção de Mesclagem
- Multicast
- Dinâmico
- Contagem de Linhas
- Dimensão de Alteração Lenta
- Classificar
- Pesquisa de Termos
- Unir Tudo
- Não Dinâmico

## <a name="data-flow-transformations-supported-with-limitations"></a>Transformações de fluxo de dados compatíveis com limitações

| Componente | Limitações |
|------------|---|
| transformação Comando OLE DB | As mesmas limitações da origem e do destino OLE DB. |
| componente Script | Só dá suporte às APIs padrão do .NET Framework. |
| | |

## <a name="supported-and-unsupported-log-providers"></a>Provedores de logs com e sem suporte
Há suporte para todos os provedores de logs internos do SSIS no Linux, exceto no provedor de Logs de Eventos do Windows.

O provedor de logs do SQL Server só dá suporte à Autenticação SQL; ele não dá suporte à Autenticação do Windows.

Os provedores de logs do SSIS para arquivos de texto, para arquivos XML e para o SQL Server Profiler gravam a saída em um arquivo especificado. As seguintes considerações se aplicam ao caminho do arquivo:
-   Se você não fornecer um caminho, o provedor de logs fará a gravação no diretório atual do host. Se o usuário atual não tiver permissão para fazer a gravação no diretório atual do host, o provedor de logs gerará um erro.
-   Não é possível usar uma variável de ambiente em um caminho de arquivo. Se você especificar uma variável de ambiente, o texto literal especificado será exibido no caminho do arquivo. Por exemplo, se você especificar `%TMP%/log.txt`, o provedor de logs acrescentará o texto literal `/%TMP%/log.txt` ao diretório de host atual.

## <a name="related-content-about-ssis-on-linux"></a>Conteúdo relacionado sobre o SSIS no Linux
-   [Extrair, transformar e carregar dados no Linux com o SSIS](sql-server-linux-migrate-ssis.md)
-   [Instalar o SSIS (SQL Server Integration Services) no Linux](sql-server-linux-setup-ssis.md)
-   [Configurar o SQL Server Integration Services no Linux com ssis-conf](sql-server-linux-configure-ssis.md)
-   [Agendar a execução de pacotes do SQL Server Integration Services no Linux com cron](sql-server-linux-schedule-ssis-packages.md)
