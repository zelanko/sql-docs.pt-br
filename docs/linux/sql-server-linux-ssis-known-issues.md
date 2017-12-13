---
title: "Limitações e problemas conhecidos do SSIS no Linux | Microsoft Docs"
description: "Este artigo descreve as limitações e problemas conhecidos para o SQL Server Integration Services (SSIS) em computadores Linux"
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: edff09c1c66a1b3c97a80d42d5a1d9702dca3e0c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Limitações e problemas conhecidos do SSIS no Linux

Este artigo descreve as limitações atuais e problemas conhecidos para o SQL Server Integration Services (SSIS) no Linux.

## <a name="general-limitations-and-known-issues"></a>Problemas conhecidos e limitações gerais

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

## <a name="components"></a>Componentes compatíveis e sem suportados

Os seguintes componentes internos do Integration Services têm suporte no Linux. Algumas delas têm limitações na plataforma Linux, conforme descrito nas tabelas a seguir.

Componentes internos que não estão listados aqui não têm suporte no Linux.

### <a name="supported-control-flow-tasks"></a>Suporte para tarefas de fluxo de controle
- Tarefa Inserção em Massa
- Tarefa de Fluxo de Dados
- Tarefa Criação de Perfil de Dados
- Tarefa Executar SQL
- Tarefa Executar Instrução T-SQL
- Tarefa de Expressão
- Tarefa FTP
- Tarefa Serviços Web
- XML Task

### <a name="control-flow-tasks-supported-with-limitations"></a>Tarefas de fluxo de controle compatíveis com limitações

| Tarefa | Limitações |
|------------|---|
| Tarefa executar processo | Só dá suporte ao modo em processo. |
| Tarefa sistema de arquivos | O *mover diretório* e *definir atributos de arquivo* ações não têm suporte. |
| tarefa Script | Só oferece suporte a APIs padrão do .NET Framework. |
| Tarefa Enviar Email | Só dá suporte ao modo de usuário anônimo. |
| Tarefa de transferência de banco de dados | Não há suporte para caminhos UNC. |
| | |

### <a name="supported-control-flow-containers"></a>Suporte para contêineres de fluxo de controle
- Contêiner de sequência
- Contêiner Loop For
- Contêiner Loop Foreach

### <a name="supported-data-flow-sources-and-destinations"></a>Fontes de fluxo de dados com suporte e destinos
- Destino e origem arquivo bruto
- Origem XML

### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>Fluxo de dados origens e destinos compatíveis com limitações

| Componente | Limitações |
|------------|---|
| Destino e origem do ADO.NET | Suportam apenas o provedor de dados SQLClient. |
| Fonte de arquivo simples e de destino | Somente dão suporte a caminhos de arquivo de estilo do Windows, aos quais a regra de mapeamento de caminho padrão é aplicada. Por exemplo `D:\home\ssis\travel.csv` torna-se `/home/ssis/travel.csv`. |
| Fonte OData | Suporta apenas a autenticação básica. |
| Origem ODBC e destino | Dá suporte a drivers de ODBC Unicode de 64 bits no Linux. Depende do Gerenciador de driver UnixODBC no Linux. |
| Origem de OLE DB e de destino | Apenas suporte do SQL Server Native Client 11.0 e o Microsoft OLE DB Provider para SQL Server. |
| | |

### <a name="supported-data-flow-transformations"></a>Suporte para transformações de fluxo de dados
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

### <a name="data-flow-transformations-supported-with-limitations"></a>Transformações de fluxo de dados compatíveis com limitações

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

