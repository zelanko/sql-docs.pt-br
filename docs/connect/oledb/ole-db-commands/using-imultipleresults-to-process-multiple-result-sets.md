---
title: Usando IMultipleResults para processar vários conjuntos de resultados | Microsoft Docs
description: Usando IMultipleResults para processar vários conjuntos de resultados
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: d5ea43d5607dc999bfbcc85d821167c6cdd8ae96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643654"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Usando IMultipleResults para processar vários conjuntos de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Os consumidores usam a interface **IMultipleResults** para processar os resultados retornados pela execução de comandos do OLE DB Driver for SQL Server. Quando o OLE DB Driver for SQL Server envia um comando para execução, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] executa as instruções e retorna os resultados.  
  
 Um cliente deve processar todos os resultados a partir da execução do comando. Como a execução de comandos do OLE DB Driver for SQL Server pode gerar objetos com vários conjuntos de linhas como resultados, use a interface **IMultipleResults** para garantir que a recuperação de dados de aplicativos conclua a viagem de ida e volta iniciada pelo cliente.  
  
 A seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] gera vários conjuntos de linhas, alguns contendo dados de linhas da tabela **OrderDetails** e alguns contendo resultados da cláusula COMPUTE BY:  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 Se um consumidor executar um comando que contém esse texto e solicitar um conjunto de linhas como a interface de resultados retornados, apenas o primeiro conjunto de linhas será retornado. O consumidor pode processar todas as linhas no conjunto de linhas retornado. No entanto, se a propriedade da fonte de dados DBPROP_MULTIPLECONNECTIONS for definida como VARIANT_FALSE e o MARS não estiver habilitado na conexão, nenhum outro comando poderá ser executado no objeto de sessão (o OLE DB Driver for SQL Server não criará outra conexão) até que o comando seja cancelado. Se o MARS não estiver habilitado na conexão, o OLE DB Driver for SQL Server retornará um erro DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS for VARIANT_FALSE e retornará E_FAIL se houver uma transação ativa.  
  
 O OLE DB Driver for SQL Server também retornará DB_E_OBJECTOPEN ao usar parâmetros de saída transmitidos e o aplicativo não tiver usado todos os valores de parâmetro de saída retornados antes de chamar **IMultipleResults::GetResults** para obter o próximo conjunto de resultados. Se o MARS não estiver habilitado e a conexão estiver ocupada executando um comando que não produz um conjunto de linhas ou que produz um conjunto de linhas que não seja um cursor de servidor e se a propriedade de fonte de dados DBPROP_MULTIPLECONNECTIONS estiver definida como VARIANT_TRUE, o OLE DB Driver for SQL Server criará conexões adicionais para dar suporte a objetos de comando simultâneos, a menos que exista uma transação ativa, quando então retornará um erro. As transações e o bloqueio são gerenciados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por conexão. Se uma segunda conexão for gerada, o comando nas conexões separadas não compartilhará bloqueios. É necessário ser cuidadoso em assegurar que um comando não bloqueie outro ao manter bloqueios em linhas solicitadas pelo outro comando. Se o MARS estiver habilitado, vários comandos poderão estar ativos nas conexões e, se estiverem sendo usadas transações explícitas, todos os comandos compartilharão uma transação comum.  
  
 O consumidor pode cancelar o comando usando [ISSAbort::Abort](../../oledb/ole-db-interfaces/issabort-abort-ole-db.md) ou liberando todas as referências mantidas no objeto de comando e no conjunto de linhas derivado.  
  
 O uso de **IMultipleResults** em todas as instâncias permite que o consumidor obtenha todos os conjuntos de linhas gerados pela execução do comando e permite que os consumidores determinem apropriadamente quando cancelar a execução do comando e liberar um objeto de sessão para uso por outros comandos.  
  
> [!NOTE]  
>  Ao usar cursores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a execução de comandos cria o cursor. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retorna o êxito ou a falha da criação do cursor; assim, a viagem de ida e volta à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é concluída no retorno da execução do comando. Em seguida, cada chamada de **GetNextRows** se torna uma viagem de ida e volta. Dessa forma, podem existir vários objetos de comando ativos, cada um processando um conjunto de linhas que é o resultado uma busca do cursor de servidor. Para obter mais informações, confira [Conjuntos de linha e cursores do SQL Server](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
