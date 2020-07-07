---
title: Parâmetros com valor de tabela (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC)
- ODBC, table-valued parameters
ms.assetid: ef06cd13-18e2-4c65-8ede-c3955d820e54
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 290678e11a292304d8c7b3ed3493a66870b52b29
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999732"
---
# <a name="table-valued-parameters-odbc"></a>Parâmetros com valor de tabela (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O suporte de ODBC para parâmetros com valor de tabela permite que o aplicativo cliente envie dados com parâmetros para o servidor de forma mais eficiente, enviando várias linhas ao servidor com uma chamada.  
  
 Para obter informações sobre parâmetros com valor de tabela no servidor, consulte [usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
 No ODBC, há duas formas de enviar parâmetros com valor de tabela para o servidor:  
  
-   Todos os dados de parâmetro com valor de tabela podem estar na memória no momento em que SQLExecDirect ou SQLExecute é chamado. Esses dados são armazenados em matrizes, se houver várias linhas com valor de tabela.  
  
-   Um aplicativo pode especificar dados em execução para um parâmetro com valor de tabela quando SQLExecDirect ou SQLExecute é chamado. Nesse caso, linhas de dados com valor de tabela podem ser fornecidas em lotes ou a qualquer momento, a fim de reduzir os requisitos de memória.  
  
 A primeira opção permite que os procedimentos armazenados encapsulem mais lógica corporativa. Por exemplo, um único procedimento armazenado pode encapsular toda uma transação de entrada de pedido quando o item solicitado for transmitido como um parâmetro com valor de tabela. Essa opção é muito eficiente, porque é necessária apenas uma viagem de ida e volta ao servidor. Como alternativa, você pode usar procedimentos diferentes para lidar com o cabeçalho do pedido e itens do pedido separadamente, o que exigiria mais código e um contrato mais complexo entre o cliente e o servidor.  
  
 O segundo método fornece um mecanismo eficiente para operações em massa com grandes quantidades de dados. Isso permite que um aplicativo transmita linhas de dados para o servidor sem precisar armazenar todas elas em buffer na memória antes.  
  
 Você pode criar restrições e chaves primárias quando criar a variável da tabela. Restrições são uma boa forma de assegurar que os dados de uma tabela atendam a requisitos específicos.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Usos de parâmetros ODBC com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/uses-of-odbc-table-valued-parameters.md)  
 Descreve os cenários principais de usuário para parâmetros com valor de tabela e ODBC.  
  
 [Tipo ODBC SQL para parâmetros com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/odbc-sql-type-for-table-valued-parameters.md)  
 Descreve o tipo SQL_SS_TABLE. Esse é um novo tipo ODBC SQL que oferece suporte a parâmetros com valor de tabela.  
  
 [Campos do descritor de parâmetro com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md)  
 Descreve campos do descritor que oferece suporte a parâmetros com valor de tabela.  
  
 [Campos descritores para colunas constituintes do parâmetro com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)  
 Descreve campos de descritor que têm significado para parâmetros com valor de tabela.  
  
 [Campos de registro de diagnóstico de parâmetro com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-diagnostic-record-fields.md)  
 Descreve dois campos de diagnóstico que foram acrescentados a registros de diagnóstico para oferecer suporte a parâmetros com valor de tabela.  
  
 [Atributos de instruções que afetam parâmetros com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)  
 Descreve um novo campo de cabeçalho do descritor que permite tratar as colunas de parâmetros com valor de tabela.  
  
 [Associação e transferência de dados de parâmetros com valor de tabela e valores de coluna](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)  
 Descreve a associação de parâmetro e como transmitir um parâmetro com valor de tabela ao servidor.  
  
 [Metadados do parâmetro com valor de tabela para instruções preparadas](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)  
 Descreve como um aplicativo pode obter metadados para uma chamada de procedimento preparada.  
  
 [Metadados adicionais de parâmetros com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/additional-table-valued-parameter-metadata.md)  
 Descreve como usar SQLProcedureColumns, SQLTables e SQLColumns para recuperar metadados para um parâmetro com valor de tabela.  
  
 [Conversão de dados de parâmetros com valor de tabela e outros erros e avisos](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-data-conversion-and-other-errors-and-warnings.md)  
 Descreve como processar erros em valores de colunas de parâmetros com valor de tabela.  
  
 [Compatibilidade entre versões](../../relational-databases/native-client-odbc-table-valued-parameters/cross-version-compatibility.md)  
 Descreve conflitos que podem ocorrer quando parâmetros com valor de tabela são usados por um cliente ou servidor com versão anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 [Resumo de APIs de parâmetros com valor de tabela ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/odbc-table-valued-parameter-api-summary.md)  
 Lista as funções do ODBC com suporte a parâmetros com valor de tabela.  
  
 [Exemplos de programação de parâmetros com valor de tabela (ODBC)](https://msdn.microsoft.com/library/3f52b7a7-f2bd-4455-b79e-d015fb397726)  
 Descreve como executar tarefas comuns.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Os parâmetros com valor de tabela &#40;SQL Server Native Client&#41;](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
  
  
