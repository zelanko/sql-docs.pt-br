---
title: Notas de versão do Microsoft DacFx e sqlpackage | Microsoft Docs
description: Notas de versão do Microsoft sqlpackage
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: f9fe0558b169acea58bb98a4f9a07267549aa58f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012997"
---
# <a name="sqlpackage-release-notes"></a>Notas de versão do sqlpackage

**[Baixar a versão mais recente](sqlpackage-download.md)**

## <a name="sqlpackage-181"></a>sqlpackage 18.1

Data de lançamento: 1 de fevereiro de 2019  
Compilação 

A versão inclui os seguintes recursos e correções:

- Adicionado suporte para agrupamentos UTF8.
- Correção de desempenho ao usar o avaliador de cardinalidade herdada para consultas de engenharia reversos.
- Habilitada a índices columnstore não clusterizado em um exibições indexadas.
- Corrigido um problema de desempenho significativas de esquema comparado ao gerar um script.
- Corrigida a lógica de detecção de descompasso de esquema para ignorar determinadas sessões de xevent.
- Importação fixa ordenação para tabelas de gráfico.
- Correção de exportação de tabelas externas com permissões de objeto.
- Movido para o .NET Core 2.2 
- Use o armazenamento de memória com suporte para a comparação de esquemas no .NET Core.

Esta versão inclui as compilações de visualização de plataforma cruzada do sqlpackage 2.2 do .NET Core de destino, e podem ser executada em macOS e Linux. Esta versão de visualização tem os seguintes problemas conhecidos:

- Não há suporte para os colaboradores de compilação e implantação.
- Não há suporte para arquivos. dacpac e. bacpac mais antigos que usam a serialização de dados json.
- .Dacpacs referenciado (por exemplo, master.dacpac) podem não ser resolvidas devido a problemas com sistemas de arquivos diferencia maiusculas de minúsculas.
  - Uma solução alternativa é colocar em maiusculas do nome do arquivo de referência (por exemplo, mestre. BACPAC).
## <a name="sqlpackage-180"></a>sqlpackage 18.0

Data de lançamento: 24 de outubro de 2018  
Compilação: 15.0.4200.1 

A versão inclui os seguintes recursos e correções:

- Adicionado suporte para o nível de compatibilidade do banco de dados 150.
- Adicionado suporte para instâncias gerenciadas.
- Adicionado o parâmetro de linha de comando MaxParallelism para especificar o grau de paralelismo para operações de banco de dados.
- Adicione parâmetro de linha de comando AccessToken para especificar um token de autenticação ao se conectar ao SQL Server.
- Adicionado suporte para tipos de dados BLOB/CLOB de fluxo para importações.
- Adicionado suporte para UDF escalar opção 'INLINE'.
- Adicionado suporte para sintaxe 'MERGE' da tabela de gráfico.
- Coluna de pseudo não resolvida fixa para tabelas de grafo.
- Correção de criação de um banco de dados com um arquivo otimizado de memória grupos quando tabelas com otimização de memória são usados.
- Correção incluindo as propriedades estendidas em tabelas externas.

## <a name="sqlpackage-178"></a>sqlpackage 17.8

Data do lançamento: 22 de junho de 2018  
Build: 14.0.4079.2  

A versão inclui as seguintes correções:

- Aprimorada a mensagens de erro para falhas de conexão, incluindo a mensagem de exceção do SqlClient.
- Suporte à compactação de índice nos índices de partição única para importação/exportação.
- Corrigido um problema de engenharia reverso para conjuntos de colunas XML com o SQL 2017 e posterior.
- Corrigido um problema em que o nível de compatibilidade 140 do banco de dados de criação de scripts foi ignorada para o banco de dados SQL.

## <a name="sqlpackage-1741"></a>sqlpackage 17.4.1

Data de lançamento: 25 de janeiro de 2018  
Build: 14.0.3917.1

A versão inclui as seguintes correções:

- Ao importar um. bacpac de banco de dados SQL para uma instância local, correção de erros devido a 'chaves mestras do banco de dados sem senha não têm suporte nesta versão do SQL Server'.
- Suporte ao agrupamento de catálogo de banco de dados.
- Corrigido um erro de coluna de pseudo não resolvidos para tabelas de gráfico.
- Adicionado o parâmetro de linha de comando ThreadMaxStackSize analisar TSQL com um grande número de instruções aninhadas.
- Corrigido usando o SchemaCompareDataModel com autenticação do SQL para comparar esquemas.

## <a name="sqlpackage-1740"></a>sqlpackage 17.4.0

Data de lançamento: 12 de dezembro de 2017  
Build: 14.0.3881.1

A versão inclui as seguintes correções:

- Não bloqueie quando encontrar um nível de compatibilidade do banco de dados não compreendida. Em vez disso, o banco de dados de SQL do Azure mais recente ou a plataforma de local será considerada.
- Adicionado suporte para 'política de retenção temporal' em SQL2017 + e o banco de dados SQL.
- Adicionado /DiagnosticsFile:"C:\Temp\sqlpackage.log" o parâmetro de linha de comando para especificar um caminho de arquivo para salvar as informações de diagnóstico.
- Adicionado o parâmetro de linha de comando /Diagnostics para registrar informações de diagnóstico no console.

