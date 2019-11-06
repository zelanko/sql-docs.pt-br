---
title: Notas sobre a versão do DacFx e SqlPackage | Microsoft Docs
description: Notas sobre a versão do Microsoft sqlpackage.
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: 11e10f4a29b15efbd2b0ee513080a2000ae7e2f1
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73033047"
---
# <a name="release-notes-for-sqlpackageexe"></a>Notas sobre a versão do SqlPackage.exe

**[Baixar a versão mais recente](sqlpackage-download.md)**

Este artigo lista os recursos e as correções liberadas por versões do SqlPackage.exe lançadas.

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="184-sqlpackage"></a>sqlpackage 18.4

|Plataforma|Download|Data de liberação|Versão|Compilação
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2108813)|29 de outubro de 2019|18.4|15.0.4573.2|
|macOS .NET Core |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2108815)|29 de outubro de 2019| 18.4|15.0.4573.2|
|Linux .NET Core |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2108814)|29 de outubro de 2019| 18.4|15.0.4573.2|
|Windows .NET Core |[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2109019)|29 de outubro de 2019| 18.4|15.0.4573.2|

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Implantação | Adicione suporte para implantar no Azure SQL Data Warehouse (GA). | 
| Plataforma | SqlPackage .NET Core GA para macOS, Linux e Windows. | 
| Segurança | Remova a assinatura de código SHA1. |
| Implantação | Adicionar suporte para novas edições de banco de dados do Azure: GeneralPurpose, BusinessCritical, hiperescala |
| Implantação | Adicione suporte de Instância Gerenciada para usuários e grupos do AAD. |
| Implantação | Suporte ao parâmetro/AccessToken para SqlPackage no .NET Core. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos 

| Recurso | Detalhes |
| :------ | :------ |
| ScriptDom |  Uma regressão de análise de ScriptDom foi introduzida em 18.3.1, onde ' RENAME ' é tratado incorretamente como um token de nível superior, fazendo com que a análise falhe. Isso será corrigido na próxima versão SqlPackage. | 
| &nbsp; | &nbsp; |

### <a name="known-issues-for-net-core"></a>Problemas conhecidos do .NET Core

| Recurso | Detalhes |
| :------ | :------ |
| Importar |  Para arquivos. bacpac com arquivos compactados acima de 4GB de tamanho, talvez seja necessário usar a versão do .NET Core do SqlPackage para executar a importação.  Esse comportamento se deve ao modo como o .NET Core gera cabeçalhos zip, que, embora sejam válidos, não são legíveis pela versão do .NET Full Framework do SqlPackage. | 
| Implantação | Não há suporte para o parâmetro/p: Storage = File. Somente a memória tem suporte no .NET Core. | 
| Always Encrypted | o SqlPackage .NET Core não oferece suporte a colunas Always Encrypted. | 
| Segurança | o SqlPackage .NET Core não dá suporte ao parâmetro/UA para autenticação multifator. | 
| Implantação | Não há suporte para arquivos V2 .dacpac e .bacpac antigos que usam a serialização de dados json. |
| &nbsp; | &nbsp; |

## <a name="1831-sqlpackage"></a>sqlpackage 18.3.1

|Plataforma|Download|Data de liberação|Versão|Compilação
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2102893)|13 de setembro de 2019|18.3.1|15.0.4538.1|
|.NET Core para macOS (versão prévia)|[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2102894)|13 de setembro de 2019| 18.3.1|15.0.4538.1|
|.NET Core para Linux (versão prévia)|[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2102978)|13 de setembro de 2019| 18.3.1|15.0.4538.1|
|Windows .NET Core (versão prévia)|[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2102979)|13 de setembro de 2019| 18.13.1|15.0.4538.1|

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Implantação | Adicione suporte para implantar no Azure SQL Data Warehouse (versão prévia). | 
| Implantação | Adicione o parâmetro/p: DatabaseLockTimeout = (INT32 ' 60 ') ao SqlPackage. | 
| Implantação | Adicione o parâmetro/p: LongRunningCommandTimeout = (INT32) ao SqlPackage. |
| Exportar/extrair | Adicione o parâmetro/p: TempDirectoryForTableData = (cadeia de caracteres) ao SqlPackage. |
| Implantação | Permitir que os colaboradores de implantação sejam carregados de locais adicionais. Os colaboradores de implantação serão carregados do mesmo diretório que o Target. dacpac que está sendo implantado, o diretório de extensões relativo ao binário SqlPackage. exe e o parâmetro/p: AdditionalDeploymentContributorPaths = (STRING) adicionado ao SqlPackage onde locais de diretório adicionais podem ser especificados. |
| Implantação | Adicione suporte para OPTIMIZE_FOR_SEQUENTIAL_KEY. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Implantação | Corrija para ignorar índices automáticos para que eles não sejam descartados na implantação. | 
| Always Encrypted | Correção para manipulação de Always Encrypted colunas varchar. | 
| Compilação/Implantação | Corrija para resolver o método Nodes () para conjuntos de colunas XML.| 
| ScriptDom | Corrigir casos adicionais em que a cadeia de caracteres ' URL ' foi interpretada como um token de nível superior. | 
| Gráfico | Corrigir o TSQL gerado para referências de pseudo coluna em restrições.  | 
| Exportar | Gerar senhas aleatórias que atendam aos requisitos de complexidade. | 
| Implantação | Correção para honrar os tempos limite de comando ao recuperar restrições. | 
| .NET Core (versão prévia) | Corrija o log de diagnóstico em um arquivo. | 
| .NET Core (versão prévia) | Use o streaming para exportar dados de tabela para dar suporte a tabelas grandes. | 
| &nbsp; | &nbsp; |

## <a name="182-sqlpackage"></a>sqlpackage 18.2

|Plataforma|Download|Data de liberação|Versão|Compilação
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2087429)|15 de abril de 2019|18.2|15.0.4384.2|
|.NET Core para macOS (versão prévia)|[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2087247)|15 de abril de 2019 | 18.2 |15.0.4384.2|
|.NET Core para Linux (versão prévia)|[arquivo zip](https://go.microsoft.com/fwlink/?linkid=2087431)|15 de abril de 2019 | 18.2 |15.0.4384.2|

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Gráfico | Adição de suporte de tabela de grafo para restrições de borda e cláusulas de restrição de borda. |
| Implantação | Habilitada a regra de validação de modelo para dar suporte a 32 colunas de chaves de índice para o SQL Server 2016 e superior. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Implantação | Correção de engenharia reversa do banco de dados do SQL Server 2016 RTM em razão de uma dica de consulta sem suporte que estava sendo usada. |
| Implantação | Correção da ordenação de implantação de instruções ALTER de fechamento automático a fim de ocorrer antes das instruções CREATE FILEGROUP. |
| ScriptDom | Correção da regressão de análise de ScriptDom em que a cadeia de caracteres da 'URL' era interpretada como um token de nível superior. |
| Implantação | Correção de uma exceção de referência NULL ao analisar uma instrução ALTER TABLE ADD INDEX. | 
| Comparação de Esquemas | Correção de comparação de esquema para colunas calculadas persistentes que permitem valor nulo que sempre se apresentavam como diferentes.|
| &nbsp; | &nbsp; |

## <a name="181-sqlpackage"></a>sqlpackage 18.1

Data do lançamento: &nbsp;1º de fevereiro de 2019  
Build: &nbsp; 15.0.4316.1  
Versão prévia.

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Implantação | Adicionado suporte a ordenações de UTF8. |
| Implantação | Habilitados os índices columnstore não clusterizados em uma exibição indexada. |
| Plataforma | Movido para o .NET Core 2.2. | 
| Comparação de Esquemas | Uso de armazenamento de backup na memória para a comparação de esquemas no .NET Core. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Desempenho | Correção de desempenho para usar o estimador de cardinalidade herdada para consultas de engenharia reversa. | 
| Desempenho | Correção de um problema de desempenho de comparação de esquema significativo ao gerar um script. | 
| Comparação de Esquemas | Correção da lógica de detecção de descompasso do esquema para ignorar determinadas sessões de evento estendido (xevent). |
| Gráfico | Correção da ordenação de importação para tabelas de grafo. | 
| Exportar | Correção de tabelas externas de exportação com permissões de objetos. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

Esta versão inclui os builds da versão prévia da plataforma cruzada do sqlpackage destinados ao .NET Core 2.2. O sqlpackage pode ser executado no macOS e no Linux.

| Problema conhecido | Detalhes |
| :---------- | :------ |
| Implantação | Não há suporte para os colaboradores de implantação e build do .NET Core. | 
| Implantação | Não há suporte para arquivos .dacpac e .bacpac antigos do .NET Core que usam a serialização de dados json. | 
| Implantação | Os .dacpacs referenciados do .NET Core (por exemplo, master.dacpac) podem não resolver em virtude de problemas com sistemas de arquivos que diferenciam maiúsculas de minúsculas. | Uma solução alternativa é colocar o nome do arquivo de referência todo em maiúsculas (por exemplo, MASTER.BACPAC). |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>sqlpackage 18.0

Data do lançamento: &nbsp; 24 de outubro de 2018  
Build: &nbsp;15.0.4200.1

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Implantação | Adicionado o suporte para nível de compatibilidade do banco de dados 150. | 
| Implantação | Adicionado suporte para instâncias gerenciadas. | 
| Desempenho | Adicionado o parâmetro de linha de comando MaxParallelism para especificar o grau de paralelismo das operações do banco de dados. | 
| Segurança | Adicionado o parâmetro de linha de comando AccessToken para especificar um token de autenticação ao se conectar ao SQL Server. | 
| Importar | Adicionado suporte para transmissão de tipos de dados BLOB/CLOB para importações. | 
| Implantação | Adicionado suporte para a opção escalar UDF 'INLINE'. | 
| Gráfico | Adicionado suporte para sintaxe 'MERGE' da tabela de grafo. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Gráfico | Correção de pseudo-coluna não resolvida para tabelas de grafo. |
| Implantação | Correção na criação de um banco de dados com grupos de arquivo otimizado para memória ao usar tabelas otimizadas para memória. |
| Implantação | Correção na inclusão de propriedades estendidas em tabelas externas. |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>sqlpackage 17.8

Data de lançamento: &nbsp; 22 de junho de 2018  
Build: &nbsp; 14.0.4079.2

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Diagnóstico | Aprimoramento de mensagens de erro para falhas de conexão, incluindo a mensagem de exceção do SqlClient. |
| Implantação | Suporte à compactação de índice nos índices de partição única para importação/exportação. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Implantação | Correção de um problema de engenharia reversa de conjuntos de colunas XML com o SQL 2017 e posterior. | 
| Implantação | Correção de um problema em que a criação de script do nível de compatibilidade 140 do banco de dados foi ignorada no banco de dados SQL do Azure. |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>sqlpackage 17.4.1

Data do lançamento: &nbsp; 25 de janeiro de 2018  
Build: &nbsp; 14.0.3917.1

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Importar/Exportar | Inclusão do parâmetro de linha de comando ThreadMaxStackSize para analisar o Transact-SQL com um grande número de instruções aninhadas. |
| Implantação | Suporte à ordenação de catálogo do banco de dados. | 
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Importar | Na importação de um .bacpac do Banco de Dados SQL do Azure para instâncias locais, foram corrigidos erros em virtude da _falta de suporte, nesta versão do SQL Server, para chaves mestra sem senha do banco dados_. |
| Gráfico | Correção de um erro de pseudo-coluna não resolvida para tabelas de grafo. |
| Comparação de Esquemas | Correção de autenticação do SQL para comparar esquemas. | 
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>sqlpackage 17.4.0

Data de lançamento: &nbsp;12 de dezembro de 2017  
Build: &nbsp; 14.0.3881.1

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Implantação |  Inclusão de suporte à _política de retenção de dados_ no SQL 2017+ e no Banco de Dados SQL do Azure. | 
| Diagnóstico | Inclusão do parâmetro de linha de comando /DiagnosticsFile:"C:\Temp\sqlpackage.log" para especificar um caminho de arquivo para salvar as informações de diagnóstico. | 
| Diagnóstico | Inclusão do parâmetro de linha de comando /Diagnostics para registrar as informações de diagnóstico no console. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Implantação | Não bloquear ao encontrar um nível de compatibilidade do banco de dados que não seja compreendido. Em vez disso, o Banco de Dados SQL do Azure ou a plataforma local será assumida. |
| &nbsp; | &nbsp; |
