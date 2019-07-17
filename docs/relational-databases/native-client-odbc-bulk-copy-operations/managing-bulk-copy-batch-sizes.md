---
title: Gerenciando tamanhos de lote de cópia em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- ODBC, bulk copy operations
- batches [ODBC]
- bulk copy [ODBC], batch sizes
ms.assetid: 4b24139f-788b-45a6-86dc-ae835435d737
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: accfe1881048c79c7b3228c90b37bf00c5629913
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130878"
---
# <a name="managing-bulk-copy-batch-sizes"></a>Gerenciando tamanhos de lote para cópia em massa
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  A principal finalidade de um lote em operações de cópia em massa é definir o escopo de uma transação. Se o tamanho de um lote não for definido, as funções de cópia em massa irão considerar uma cópia em massa inteira como uma única transação. Se o tamanho do lote for definido, cada lote constituirá uma transação que será confirmada quando o lote terminar.  
  
 Se uma cópia em massa for executada sem tamanho de lote especificado e um erro for retornado, a cópia em massa inteira será revertida. A recuperação de uma cópia em massa longa pode levar muito tempo. Quando um tamanho de lote é definido, a cópia em massa considera cada lote uma transação e confirma cada lote. Se um erro for encontrado, apenas o último lote pendente precisará ser revertido.  
  
 O tamanho do lote também pode afetar a sobrecarga de bloqueios. Ao executar uma cópia em massa contra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a dica TABLOCK pode ser especificada usando [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) para adquirir um bloqueio de tabela em vez de bloqueios de linha. É possível manter um bloqueio de tabela com sobrecarga mínima para uma operação de cópia em massa inteira. Se TABLOCK não for especificada, os bloqueios serão mantidos em filas individuais e a sobrecarga da manutenção de todos os bloqueios durante a cópia em massa poderá prejudicar o desempenho. Pelo fato de os bloqueios só serem mantidos durante o tempo de uma transação, a especificação do tamanho de um lote trata esse problema gerando periodicamente uma confirmação que libera os bloqueios mantidos.  
  
 O número de linhas que compõem um lote pode ter efeitos significativos no desempenho quando a operação de cópia em massa é feita em um grande número de linhas. As recomendações de tamanho de lote dependem do tipo de cópia em massa que está sendo executada.  
  
-   Ao fazer uma cópia em massa no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique a dica de cópia em massa TABLOCK e defina um tamanho de lote grande.  
  
-   Quando TABLOCK não é especificada, limite os tamanhos de lote para menos de 1.000 linhas.  
  
 Quando a cópia em massa no arquivo de dados, o tamanho do lote é especificado chamando **bcp_control** com a opção de BCPBATCH antes de chamar [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md). Quando cópia em massa de variáveis de programa usando [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) e [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md), o tamanho do lote é controlado pela chamada [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) depois de chamar [BCP _ sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) *x* vezes, onde *x* é o número de linhas em um lote.  
  
 Além de especificar o tamanho de uma transação, os lotes também controlam quando serão enviadas linhas ao servidor através da rede. Funções de cópia em massa cache normalmente as linhas de **bcp_sendrow** até que um pacote de rede é preenchido e, em seguida, enviar o pacote completo para o servidor. Quando um aplicativo chama **bcp_batch**, no entanto, o pacote atual é enviado ao servidor, independentemente se ele tiver sido preenchido. O uso de um tamanho de lote muito baixo pode prejudicar o desempenho se resultar no envio de muitos pacotes parcialmente preenchidos para o servidor. Por exemplo, chamar **bcp_batch** depois de cada **bcp_sendrow** faz com que cada linha a ser enviada em um pacote separado e, a menos que as linhas são muito grandes, isso desperdiça o espaço em cada pacote. O tamanho padrão de pacotes de rede para o SQL Server é 4 KB, embora um aplicativo pode alterar o tamanho, chamando [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) especificando o atributo SQL_ATTR_PACKET_SIZE.  
  
 Outro efeito colateral de lotes é que cada lote é considerado um conjunto até que ele seja concluído com de resultados pendentes **bcp_batch**. Se qualquer outra operação for tentada em um identificador de conexão enquanto um lote estiver pendente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client emitirá um erro com SQLState = "HY000" e uma cadeia de caracteres de mensagem de erro de:  
  
```  
"[Microsoft][SQL Server Native Client] Connection is busy with  
results for another hstmt."  
```  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações de cópia em massa &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
