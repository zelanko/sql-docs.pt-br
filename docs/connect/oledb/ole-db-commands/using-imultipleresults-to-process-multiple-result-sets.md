---
title: Usando IMultipleResults para processar vários conjuntos de resultados | Microsoft Docs
description: Usando IMultipleResults para processar resultados múltiplos conjuntos
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a2b3a902c071e29729fae4eee5f208626cb47440
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Usando IMultipleResults para processar vários conjuntos de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os consumidores usam o **IMultipleResults** interface para processar os resultados retornados pelo Driver do OLE DB para a execução de comando do SQL Server. Quando o Driver OLE DB para SQL Server envia um comando para execução, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] executa as instruções e retorna todos os resultados.  
  
 Um cliente deve processar todos os resultados a partir da execução do comando. Como o Driver OLE DB para a execução de comando do SQL Server pode gerar objetos de vários conjuntos de linhas como resultados, use o **IMultipleResults** interface para garantir que a recuperação de dados de aplicativo conclui a ida e volta iniciada pelo cliente.  
  
 O seguinte [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução gera vários conjuntos de linhas, alguns dados da linha que contém o **OrderDetails** tabela e alguns contendo resultados da cláusula COMPUTE BY:  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 Se um consumidor executar um comando que contém esse texto e solicitar um conjunto de linhas como a interface de resultados retornados, apenas o primeiro conjunto de linhas será retornado. O consumidor pode processar todas as linhas no conjunto de linhas retornado. Mas, se a propriedade de fonte de dados DBPROP_MULTIPLECONNECTIONS for definida como VARIANT_FALSE e o MARS não está habilitado na conexão, não há outros comandos podem ser executados no objeto de sessão (o Driver OLE DB para SQL Server não criará outra conexão) até que o comando é cancelado. Se o MARS não está ativado a conexão, o Driver OLE DB para SQL Server retorna um erro DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS for VARIANT_FALSE e retornará E_FAIL se houver uma transação ativa.  
  
 O Driver OLE DB para SQL Server também retornará DB_E_OBJECTOPEN quando usar streaming de parâmetros de saída e o aplicativo não tiver usado a todos os valores de parâmetro de saída retornados antes de chamar **imultipleresults:: GetResults** para obter o próximo conjunto de resultados. Se o MARS não está habilitado e a conexão está ocupada executando um comando que não produz um conjunto de linhas ou que produz um conjunto de linhas que não é um cursor de servidor e se a propriedade da fonte de dados DBPROP_MULTIPLECONNECTIONS for definido como VARIANT_TRUE, o Driver OLE DB para SQL Server Cria conexões adicionais para dar suporte a objetos de comando simultâneos, a menos que uma transação está ativa, caso em que ele retorna um erro. As transações e o bloqueio são gerenciados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por conexão. Se uma segunda conexão for gerada, o comando nas conexões separadas não compartilhará bloqueios. É necessário ser cuidadoso em assegurar que um comando não bloqueie outro ao manter bloqueios em linhas solicitadas pelo outro comando. Se o MARS estiver habilitado, vários comandos poderão estar ativos nas conexões e, se estiverem sendo usadas transações explícitas, todos os comandos compartilharão uma transação comum.  
  
 O consumidor pode cancelar o comando usando [issabort:: Abort](../../oledb/ole-db-interfaces/issabort-abort-ole-db.md) ou liberando todas as referências mantidas no objeto de comando e o conjunto de linhas derivado.  
  
 Usando **IMultipleResults** em todas as instâncias permite que o consumidor Obtenha todos os conjuntos de linhas gerados pela execução de comando e permite que os consumidores determinem apropriadamente quando cancelar a execução do comando e liberar um objeto de sessão para uso pelo outros comandos.  
  
> [!NOTE]  
>  Ao usar cursores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a execução de comandos cria o cursor. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retorna o êxito ou a falha da criação do cursor; assim, a viagem de ida e volta à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é concluída no retorno da execução do comando. Cada **GetNextRows** chamada torna-se uma viagem de ida e. Dessa forma, podem existir vários objetos de comando ativos, cada um processando um conjunto de linhas que é o resultado uma busca do cursor de servidor. Para obter mais informações, consulte [conjuntos de linhas e cursores do SQL Server](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Consulte também  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
