---
title: Usando IMultipleResults para processar vários conjuntos de resultados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
ms.assetid: 754d3f30-7d94-4b67-8dac-baf2699ce9c6
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e4c2ee0f7a96ad30f3b13c36625077a74deca9fd
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707515"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Usando IMultipleResults para processar vários conjuntos de resultados
  Os consumidores usam a interface **IMultipleResults** para processar resultados retornados pela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execução do comando do provedor de OLE DB de cliente nativo. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo envia um comando para execução, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o executa as instruções e retorna os resultados.  
  
 Um cliente deve processar todos os resultados a partir da execução do comando. Como a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execução do comando do provedor de OLE DB de cliente nativo pode gerar objetos de vários conjuntos de linhas como resultados, use a interface **IMultipleResults** para garantir que a recuperação de dados do aplicativo conclua a viagem de ida e volta iniciada pelo cliente.  
  
 A seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] gera vários conjuntos de linhas, alguns contendo dados de linhas da tabela **OrderDetails** e alguns contendo resultados da cláusula COMPUTE BY:  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 Se um consumidor executar um comando que contém esse texto e solicitar um conjunto de linhas como a interface de resultados retornados, apenas o primeiro conjunto de linhas será retornado. O consumidor pode processar todas as linhas no conjunto de linhas retornado. Mas, se a propriedade de fonte de dados DBPROP_MULTIPLECONNECTIONS for definida como VARIANT_FALSE e o MARS não estiver habilitado na conexão, nenhum outro comando poderá ser executado no objeto de sessão (o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do cliente nativo não criará outra conexão) até que o comando seja cancelado. Se o MARS não estiver habilitado na conexão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retornará um erro de DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS for VARIANT_FALSE e retornar E_FAIL se houver uma transação ativa.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo também retornará DB_E_OBJECTOPEN ao usar parâmetros de saída em fluxo e o aplicativo não consumiu todos os valores de parâmetro de saída retornados antes de chamar **IMultipleResults:: GetResults** para obter o próximo conjunto de resultados. Se o MARS não estiver habilitado e a conexão estiver ocupada executando um comando que não produz um conjunto de linhas ou que produz um conjunto de linhas que não é um cursor de servidor, e se a propriedade de fonte de dados DBPROP_MULTIPLECONNECTIONS for definida como VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo criará conexões adicionais para dar suporte a objetos de comando simultâneos, a menos que uma transação esteja ativa; nesse As transações e o bloqueio são gerenciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por conexão. Se uma segunda conexão for gerada, o comando nas conexões separadas não compartilhará bloqueios. É necessário ser cuidadoso em assegurar que um comando não bloqueie outro ao manter bloqueios em linhas solicitadas pelo outro comando. Se o MARS estiver habilitado, vários comandos poderão estar ativos nas conexões e, se estiverem sendo usadas transações explícitas, todos os comandos compartilharão uma transação comum.  
  
 O consumidor pode cancelar o comando usando [ISSAbort::Abort](../native-client-ole-db-interfaces/issabort-abort-ole-db.md) ou liberando todas as referências mantidas no objeto de comando e no conjunto de linhas derivado.  
  
 O uso de **IMultipleResults** em todas as instâncias permite que o consumidor obtenha todos os conjuntos de linhas gerados pela execução do comando e permite que os consumidores determinem apropriadamente quando cancelar a execução do comando e liberar um objeto de sessão para uso por outros comandos.  
  
> [!NOTE]  
>  Ao usar cursores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a execução de comandos cria o cursor. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna o êxito ou a falha da criação do cursor; assim, a viagem de ida e volta à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é concluída no retorno da execução do comando. Em seguida, cada chamada de **GetNextRows** se torna uma viagem de ida e volta. Dessa forma, podem existir vários objetos de comando ativos, cada um processando um conjunto de linhas que é o resultado uma busca do cursor de servidor. Para obter mais informações, confira [Conjuntos de linha e cursores do SQL Server](../native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Comandos](commands.md)  
  
  
