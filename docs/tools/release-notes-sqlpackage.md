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
ms.openlocfilehash: 411a2cf4c9a3170e9fb3a3dc7709d8b3882f066b
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59670862"
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

## <a name="182-sqlpackage"></a>sqlpackage 18.2

Data do lançamento: &nbsp; 15 de abril de 2019  
Build: &nbsp; 15.0.4384.2 

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Adição de suporte de tabela de grafo para restrições de borda e cláusulas de restrição de borda. | &nbsp; |
| Habilitada a regra de validação de modelo para dar suporte a 32 colunas de chaves de índice para o SQL Server 2016 e superior. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Correção de engenharia reversa do banco de dados do SQL Server 2016 RTM em razão de uma dica de consulta sem suporte que estava sendo usada. | &nbsp; |
| Correção da ordenação de implantação de instruções ALTER de fechamento automático a fim de ocorrer antes das instruções CREATE FILEGROUP. | &nbsp; |
| Correção da regressão de análise de ScriptDom em que a cadeia de caracteres da 'URL' era interpretada como um token de nível superior. | &nbsp; |
| Correção de uma exceção de referência NULL ao analisar uma instrução ALTER TABLE ADD INDEX. | &nbsp; |
| Correção de comparação de esquema para colunas calculadas persistentes que permitem valor nulo que sempre se apresentavam como diferentes.| &nbsp; |
| &nbsp; | &nbsp; |

## <a name="181-sqlpackage"></a>sqlpackage 18.1

Data do lançamento: &nbsp;1º de fevereiro de 2019  
Build: &nbsp; 15.0.4316.1  
Versão prévia.

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Adicionado suporte a ordenações de UTF8. | &nbsp; |
| Habilitados os índices columnstore não clusterizados em uma exibição indexada. | &nbsp; |
| Movido para o .NET Core 2.2. | &nbsp; |
| Uso de armazenamento de backup na memória para a comparação de esquemas no .NET Core. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Correção de desempenho para usar o estimador de cardinalidade herdada para consultas de engenharia reversa. | &nbsp; |
| Correção de um problema de desempenho de comparação de esquema significativo ao gerar um script. | &nbsp; |
| Correção da lógica de detecção de descompasso do esquema para ignorar determinadas sessões de evento estendido (xevent). | &nbsp; |
| Correção da ordenação de importação para tabelas de grafo. | &nbsp; |
| Correção de tabelas externas de exportação com permissões de objetos. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

Esta versão inclui os builds da versão prévia da plataforma cruzada do sqlpackage destinados ao .NET Core 2.2. O sqlpackage pode ser executado no macOS e no Linux.

| Problema conhecido | Detalhes |
| :---------- | :------ |
| Colaboradores de implantação e build não têm suporte. | &nbsp; |
| Não há suporte para arquivos .dacpac e .bacpac antigos que usam a serialização de dados json. | &nbsp; |
| .dacpacs referenciados (por exemplo, master.dacpac) podem não resolver em virtude de problemas com sistemas de arquivos que diferenciam maiúsculas de minúsculas. | Uma solução alternativa é colocar o nome do arquivo de referência todo em maiúsculas (por exemplo, MASTER.BACPAC). |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>sqlpackage 18.0

Data do lançamento: &nbsp; 24 de outubro de 2018  
Build: &nbsp;15.0.4200.1

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Adicionado o suporte para nível de compatibilidade do banco de dados 150. | &nbsp; |
| Adicionado suporte para instâncias gerenciadas. | &nbsp; |
| Adicionado o parâmetro de linha de comando MaxParallelism para especificar o grau de paralelismo das operações do banco de dados. | &nbsp; |
| Adicionado o parâmetro de linha de comando AccessToken para especificar um token de autenticação ao se conectar ao SQL Server. | &nbsp; |
| Adicionado suporte para transmissão de tipos de dados BLOB/CLOB para importações. | &nbsp; |
| Adicionado suporte para a opção escalar UDF 'INLINE'. | &nbsp; |
| Adicionado suporte para sintaxe 'MERGE' da tabela de grafo. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Correção de pseudo-coluna não resolvida para tabelas de grafo. | &nbsp; |
| Correção na criação de um banco de dados com grupos de arquivo otimizado para memória ao usar tabelas otimizadas para memória. | &nbsp; |
| Correção na inclusão de propriedades estendidas em tabelas externas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>sqlpackage 17.8

Data de lançamento: &nbsp; 22 de junho de 2018  
Build: &nbsp; 14.0.4079.2

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Aprimoramento de mensagens de erro para falhas de conexão, incluindo a mensagem de exceção do SqlClient. | &nbsp; |
| Suporte à compactação de índice nos índices de partição única para importação/exportação. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Correção de um problema de engenharia reversa de conjuntos de colunas XML com o SQL 2017 e posterior. | &nbsp; |
| Correção de um problema em que a criação de script do nível de compatibilidade 140 do banco de dados foi ignorada no banco de dados SQL do Azure. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>sqlpackage 17.4.1

Data do lançamento: &nbsp; 25 de janeiro de 2018  
Build: &nbsp; 14.0.3917.1

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Inclusão do parâmetro de linha de comando ThreadMaxStackSize para analisar o Transact-SQL com um grande número de instruções aninhadas. | &nbsp; |
| Suporte à ordenação de catálogo do banco de dados. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Na importação de um .bacpac do banco de dados SQL do Azure para uma instância local, foram corrigidos erros em virtude da _falta de suporte, nesta versão do SQL Server, para chaves mestra sem senha do banco dados_. | &nbsp; |
| Correção de um erro de pseudo-coluna não resolvida para tabelas de grafo. | &nbsp; |
| Correção no uso do SchemaCompareDataModel com autenticação do SQL para comparação de esquemas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>sqlpackage 17.4.0

Data de lançamento: &nbsp;12 de dezembro de 2017  
Build: &nbsp; 14.0.3881.1

### <a name="features"></a>Recursos

| Recurso | Detalhes |
| :------ | :------ |
| Inclusão de suporte à _política de retenção de dados_ no SQL 2017+ e no Banco de Dados SQL do Azure. | &nbsp; |
| Inclusão do parâmetro de linha de comando /DiagnosticsFile:"C:\Temp\sqlpackage.log" para especificar um caminho de arquivo para salvar as informações de diagnóstico. | &nbsp; |
| Inclusão do parâmetro de linha de comando /Diagnostics para registrar as informações de diagnóstico no console. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correções

| Fix | Detalhes |
| :-- | :------ |
| Não bloquear ao encontrar um nível de compatibilidade do banco de dados que não seja compreendido. | Em vez disso, o Banco de Dados SQL do Azure ou a plataforma local será assumida. |
| &nbsp; | &nbsp; |
