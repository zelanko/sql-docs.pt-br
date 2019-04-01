---
title: Notas de versão do DacFx e SqlPackage | Microsoft Docs
description: Notas de versão do sqlpackage da Microsoft.
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: de45add2b02686f990d68f7c1c23eec385848751
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538772"
---
# <a name="release-notes-for-sqlpackageexe"></a>Notas de versão do SqlPackage.exe

**[Baixar a versão mais recente](sqlpackage-download.md)**

Este artigo lista os recursos e correções entregues por versões liberadas do SqlPackage.exe.

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="181-sqlpackage"></a>sqlpackage 18.1

Data do lançamento: &nbsp;1º de fevereiro de 2019  
Build: &nbsp; 15.0.4316.1  
Versão de visualização.

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Adicionado suporte para agrupamentos UTF8. | &nbsp; |
| Habilitada a índices columnstore não clusterizado em uma exibição indexada. | &nbsp; |
| Movido para o .NET Core 2.2. | &nbsp; |
| Use o armazenamento de memória com suporte para a comparação de esquemas no .NET Core. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Correção de desempenho ao usar o avaliador de cardinalidade herdada para consultas de engenharia reversos. | &nbsp; |
| Corrigido um problema de desempenho significativas de esquema comparado ao gerar um script. | &nbsp; |
| Corrigida a lógica de detecção de descompasso de esquema para ignorar determinadas sessões de eventos estendidos (xevent). | &nbsp; |
| Importação fixa ordenação para tabelas de gráfico. | &nbsp; |
| Correção de exportação de tabelas externas com permissões de objeto. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

Esta versão inclui as compilações de visualização de plataforma cruzada do sqlpackage destinados ao .NET Core 2.2. O sqlpackage pode executar no macOS e Linux.

| Problema conhecido | Detalhes |
| :---------- | :------ |
| Não há suporte para os colaboradores de compilação e implantação. | &nbsp; |
| Não há suporte para arquivos. dacpac e. bacpac mais antigos que usam a serialização de dados json. | &nbsp; |
| .Dacpacs referenciado (por exemplo, master.dacpac) podem não ser resolvidas devido a problemas com sistemas de arquivos diferencia maiusculas de minúsculas. | Uma solução alternativa é colocar em maiusculas do nome do arquivo de referência (por exemplo, mestre. BACPAC). |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>sqlpackage 18.0

Data de lançamento: &nbsp; 24 de outubro de 2018  
Build: &nbsp;15.0.4200.1

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Adicionado suporte para o nível de compatibilidade do banco de dados 150. | &nbsp; |
| Adicionado suporte para instâncias gerenciadas. | &nbsp; |
| Adicionado o parâmetro de linha de comando MaxParallelism para especificar o grau de paralelismo para operações de banco de dados. | &nbsp; |
| Adicionado o parâmetro de linha de comando AccessToken para especificar um token de autenticação ao se conectar ao SQL Server. | &nbsp; |
| Adicionado suporte para tipos de dados BLOB/CLOB de fluxo para importações. | &nbsp; |
| Adicionado suporte para UDF escalar opção 'INLINE'. | &nbsp; |
| Adicionado suporte para sintaxe 'MERGE' da tabela de gráfico. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Coluna de pseudo não resolvida fixa para tabelas de grafo. | &nbsp; |
| Correção de criação de um banco de dados com um arquivo otimizado de memória grupos quando tabelas com otimização de memória são usados. | &nbsp; |
| Correção incluindo as propriedades estendidas em tabelas externas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>sqlpackage 17.8

Data de lançamento: &nbsp; 22 de junho de 2018  
Build: &nbsp; 14.0.4079.2

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Aprimorada a mensagens de erro para falhas de conexão, incluindo a mensagem de exceção do SqlClient. | &nbsp; |
| Suporte à compactação de índice nos índices de partição única para importação/exportação. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Corrigido um problema de engenharia reverso para conjuntos de colunas XML com o SQL 2017 e posterior. | &nbsp; |
| Corrigido um problema em que o nível de compatibilidade 140 do banco de dados de criação de scripts foi ignorada para o banco de dados SQL. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>sqlpackage 17.4.1

Data de lançamento: &nbsp; 25 de janeiro de 2018  
Build: &nbsp; 14.0.3917.1

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Adicionado o parâmetro de linha de comando ThreadMaxStackSize ao analisar o Transact-SQL com um grande número de instruções aninhadas. | &nbsp; |
| Suporte ao agrupamento de catálogo de banco de dados. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Ao importar um. bacpac de banco de dados SQL para uma instância local, correção de erros de devido à _não há suporte para chaves mestras do banco de dados sem senha nesta versão do SQL Server_. | &nbsp; |
| Corrigido um erro de coluna de pseudo não resolvidos para tabelas de gráfico. | &nbsp; |
| Corrigido usando o SchemaCompareDataModel com autenticação do SQL para comparar esquemas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>sqlpackage 17.4.0

Data de lançamento: &nbsp;12 de dezembro de 2017  
Build: &nbsp; 14.0.3881.1

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Adicionado suporte para _política de retenção temporal_ no SQL 2017 + e o banco de dados SQL. | &nbsp; |
| Adicionado /DiagnosticsFile:"C:\Temp\sqlpackage.log" o parâmetro de linha de comando para especificar um caminho de arquivo para salvar as informações de diagnóstico. | &nbsp; |
| Adicionado o parâmetro de linha de comando /Diagnostics para registrar informações de diagnóstico no console. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Não bloqueie ao encontrar um nível de compatibilidade do banco de dados que não é compreendido. | Em vez disso, a plataforma mais recente do banco de dados SQL ou no local será considerada. |
| &nbsp; | &nbsp; |
