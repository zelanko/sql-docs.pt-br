---
title: Parâmetros com valor de tabela (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC)
- ODBC, table-valued parameters
ms.assetid: ef06cd13-18e2-4c65-8ede-c3955d820e54
author: rothja
ms.author: jroth
ms.openlocfilehash: d98e8d4ab44709947d8786bce2829954703c77e5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039418"
---
# <a name="table-valued-parameters-odbc"></a>Parâmetros com valor de tabela (ODBC)
  O suporte de ODBC para parâmetros com valor de tabela permite que o aplicativo cliente envie dados com parâmetros para o servidor de forma mais eficiente, enviando várias linhas ao servidor com uma chamada.  
  
 Para obter informações sobre parâmetros com valor de tabela no servidor, consulte [usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../tables/use-table-valued-parameters-database-engine.md).  
  
 No ODBC, há duas formas de enviar parâmetros com valor de tabela para o servidor:  
  
-   Todos os dados de parâmetro com valor de tabela podem estar na memória no momento em que SQLExecDirect ou SQLExecute é chamado. Esses dados são armazenados em matrizes, se houver várias linhas com valor de tabela.  
  
-   Um aplicativo pode especificar dados em execução para um parâmetro com valor de tabela quando SQLExecDirect ou SQLExecute é chamado. Nesse caso, linhas de dados com valor de tabela podem ser fornecidas em lotes ou a qualquer momento, a fim de reduzir os requisitos de memória.  
  
 A primeira opção permite que os procedimentos armazenados encapsulem mais lógica corporativa. Por exemplo, um único procedimento armazenado pode encapsular toda uma transação de entrada de pedido quando o item solicitado for transmitido como um parâmetro com valor de tabela. Essa opção é muito eficiente, porque é necessária apenas uma viagem de ida e volta ao servidor. Como alternativa, você pode usar procedimentos diferentes para lidar com o cabeçalho do pedido e itens do pedido separadamente, o que exigiria mais código e um contrato mais complexo entre o cliente e o servidor.  
  
 O segundo método fornece um mecanismo eficiente para operações em massa com grandes quantidades de dados. Isso permite que um aplicativo transmita linhas de dados para o servidor sem precisar armazenar todas elas em buffer na memória antes.  
  
 Você pode criar restrições e chaves primárias quando criar a variável da tabela. Restrições são uma boa forma de assegurar que os dados de uma tabela atendam a requisitos específicos.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Usos de parâmetros ODBC com valor de tabela](uses-of-odbc-table-valued-parameters.md)  
 Descreve os cenários principais de usuário para parâmetros com valor de tabela e ODBC.  
  
 [Tipo ODBC SQL para parâmetros com valor de tabela](odbc-sql-type-for-table-valued-parameters.md)  
 Descreve o tipo SQL_SS_TABLE. Esse é um novo tipo ODBC SQL que oferece suporte a parâmetros com valor de tabela.  
  
 [Campos do descritor de parâmetro com valor de tabela](table-valued-parameter-descriptor-fields.md)  
 Descreve campos do descritor que oferece suporte a parâmetros com valor de tabela.  
  
 [Campos descritores para colunas constituintes do parâmetro com valor de tabela](descriptor-fields-for-table-valued-parameter-constituent-columns.md)  
 Descreve campos de descritor que têm significado para parâmetros com valor de tabela.  
  
 [Campos de registro de diagnóstico de parâmetro com valor de tabela](table-valued-parameter-diagnostic-record-fields.md)  
 Descreve dois campos de diagnóstico que foram acrescentados a registros de diagnóstico para oferecer suporte a parâmetros com valor de tabela.  
  
 [Atributos de instruções que afetam parâmetros com valor de tabela](statement-attributes-that-affect-table-valued-parameters.md)  
 Descreve um novo campo de cabeçalho do descritor que permite tratar as colunas de parâmetros com valor de tabela.  
  
 [Associação e transferência de dados de parâmetros com valor de tabela e valores de coluna](binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)  
 Descreve a associação de parâmetro e como transmitir um parâmetro com valor de tabela ao servidor.  
  
 [Metadados do parâmetro com valor de tabela para instruções preparadas](table-valued-parameter-metadata-for-prepared-statements.md)  
 Descreve como um aplicativo pode obter metadados para uma chamada de procedimento preparada.  
  
 [Metadados adicionais de parâmetros com valor de tabela](additional-table-valued-parameter-metadata.md)  
 Descreve como usar SQLProcedureColumns, SQLTables e SQLColumns para recuperar metadados para um parâmetro com valor de tabela.  
  
 [Conversão de dados de parâmetros com valor de tabela e outros erros e avisos](table-valued-parameter-data-conversion-and-other-errors-and-warnings.md)  
 Descreve como processar erros em valores de colunas de parâmetros com valor de tabela.  
  
 [Compatibilidade entre versões](cross-version-compatibility.md)  
 Descreve conflitos que podem ocorrer quando parâmetros com valor de tabela são usados por um cliente ou servidor com versão anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 [Resumo de APIs de parâmetros com valor de tabela ODBC](odbc-table-valued-parameter-api-summary.md)  
 Lista as funções do ODBC com suporte a parâmetros com valor de tabela.  
  
 [Exemplos de programação de parâmetros com valor de tabela (ODBC)](../../database-engine/dev-guide/odbc-table-valued-parameter-programming-examples.md)  
 Descreve como executar tarefas comuns.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [Os parâmetros com valor de tabela &#40;SQL Server Native Client&#41;](../native-client/features/table-valued-parameters-sql-server-native-client.md)  
  
  
