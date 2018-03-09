---
title: Usando arquivos de dados e arquivos de formato | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], file formats
- ODBC, functions
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [SQL Server Native Client]
- ODBC, bulk copy operations
- bulk copy [ODBC], data files
ms.assetid: c01b7155-3f0a-473d-90b7-87a97bc56ca5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 423619a7d1a9a7b80cfab796f5c4a85969b3e167
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="using-data-files-and-format-files"></a>Usando arquivos de dados e de formato
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O programa de cópia em massa mais simples executa estas tarefas:  
  
1.  Chamadas [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) para especificar cópia em massa de saída (defina BCP_OUT) de uma tabela ou exibição para um arquivo de dados.  
  
2.  Chamadas [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) para executar a operação de cópia em massa.  
  
 O arquivo de dados é criado em modo nativo; portanto, os dados de todas as colunas na tabela ou exibição são armazenados no arquivo de dados com o mesmo formato do banco de dados. É possível executar cópia em massa de entrada do arquivo em um servidor usando essas mesmas etapas e definindo DB_IN em vez de DB_OUT. Isso só funcionará se ambas as tabelas (origem e destino) tiverem exatamente a mesma estrutura. O arquivo de dados resultante também pode ser inserido para o **bcp** utilitário usando o  **/n**  switch (modo nativo).  
  
 Para executar a cópia em massa de saída do conjunto de resultados de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)], em vez de diretamente de uma tabela ou exibição:  
  
1.  Chamar **bcp_init** para especificar a cópia em massa out, mas especifique NULL para o nome da tabela.  
  
2.  Chamar [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) com *eOption* definido como BCPHINTS e *iValue* definido como um ponteiro para uma cadeia de caracteres SQLTCHAR que contém a instrução Transact-SQL.  
  
3.  Chamar **bcp_exec** para executar a operação de cópia em massa.  
  
 A instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] pode ser qualquer instrução que gera um conjunto de resultados. Será criado o arquivo de dados que contém o primeiro conjunto de resultados da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. A cópia em massa ignora qualquer conjunto de resultados após o primeiro se a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] gera vários conjuntos de resultados.  
  
 Para criar um arquivo de dados na qual coluna os dados são armazenados em um formato diferente da tabela, chame [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) para especificar quantas colunas será alterado, em seguida, chame [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) para cada coluna cujo formato você deseja alterar. Isso é feito após a chamada **bcp_init** , mas antes de chamar **bcp_exec**. **bcp_colfmt** Especifica o formato no qual os dados da coluna são armazenados no arquivo de dados. Ele pode ser usado na cópia em massa de entrada ou de saída. Você também pode usar **bcp_colfmt** para definir os terminadores de linha e coluna. Por exemplo, se seus dados não contém nenhum caractere de guia, você pode criar um arquivo delimitado por tabulação usando **bcp_colfmt** para definir o caractere de tabulação como terminador de cada coluna.  
  
 Quando em massa copiando-out e usando **bcp_colfmt**, você pode criar facilmente um arquivo de formato que descreve o arquivo de dados criado chamando [bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) após a última chamada para **bcp_colfmt**.  
  
 Quando a cópia em massa de um arquivo de dados descrito por um arquivo de formato, leia o arquivo de formato chamando [bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) depois **bcp_init** mas antes **bcp_exec**.  
  
 O **bcp_control** função controla várias opções durante a cópia em massa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um arquivo de dados. **bcp_control** define as opções, como o número máximo de erros antes do término, a linha no arquivo no qual iniciar a cópia em massa, a linha para parar e o tamanho do lote.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações de cópia em massa &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
