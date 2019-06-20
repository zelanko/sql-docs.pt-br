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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e160733e01c3df2063a57d61bb8178438d383e1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63155019"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Usando IMultipleResults para processar vários conjuntos de resultados
  Os consumidores usam a **IMultipleResults** interface para processar os resultados retornados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execução de comando do provedor OLE DB do Native Client. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client envia um comando para execução, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa as instruções e retorna quaisquer resultados.  
  
 Um cliente deve processar todos os resultados a partir da execução do comando. Porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execução de comando do provedor OLE DB do Native Client pode gerar objetos de vários conjuntos de linhas como resultados, use o **IMultipleResults** interface para garantir que a recuperação de dados de aplicativo conclui o iniciada pelo cliente de ida e volta.  
  
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
  
 Se um consumidor executar um comando que contém esse texto e solicitar um conjunto de linhas como a interface de resultados retornados, apenas o primeiro conjunto de linhas será retornado. O consumidor pode processar todas as linhas no conjunto de linhas retornado. Mas, se a propriedade de fonte de dados DBPROP_MULTIPLECONNECTIONS estiver definida como VARIANT_FALSE e o MARS não está habilitado na conexão, nenhum outro comando pode ser executado no objeto de sessão (o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client não criará outro conexão) até que o comando seja cancelado. Se o MARS não estiver habilitado na conexão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client retornará um erro DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS for VARIANT_FALSE e retornará E_FAIL se houver uma transação ativa.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client também retornará DB_E_OBJECTOPEN quando usar transmitido parâmetros de saída e o aplicativo não tiver usado todos os valores de parâmetro de saída retornados antes de chamar **imultipleresults:: GetResults**  para obter o próximo conjunto de resultados. Se o MARS não está habilitado e a conexão está ocupado executando um comando que não produz um conjunto de linhas ou que produz um conjunto de linhas que não é um cursor de servidor e se a propriedade de fonte de dados DBPROP_MULTIPLECONNECTIONS for definida como VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Provedor OLE DB cria conexões adicionais para dar suporte a objetos de comando simultâneos, a menos que uma transação está ativa, caso em que ele retorna um erro. As transações e o bloqueio são gerenciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por conexão. Se uma segunda conexão for gerada, o comando nas conexões separadas não compartilhará bloqueios. É necessário ser cuidadoso em assegurar que um comando não bloqueie outro ao manter bloqueios em linhas solicitadas pelo outro comando. Se o MARS estiver habilitado, vários comandos poderão estar ativos nas conexões e, se estiverem sendo usadas transações explícitas, todos os comandos compartilharão uma transação comum.  
  
 O consumidor pode cancelar o comando usando [ISSAbort::Abort](../native-client-ole-db-interfaces/issabort-abort-ole-db.md) ou liberando todas as referências mantidas no objeto de comando e no conjunto de linhas derivado.  
  
 O uso de **IMultipleResults** em todas as instâncias permite que o consumidor obtenha todos os conjuntos de linhas gerados pela execução do comando e permite que os consumidores determinem apropriadamente quando cancelar a execução do comando e liberar um objeto de sessão para uso por outros comandos.  
  
> [!NOTE]  
>  Ao usar cursores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a execução de comandos cria o cursor. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna o êxito ou a falha da criação do cursor; assim, a viagem de ida e volta à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é concluída no retorno da execução do comando. Em seguida, cada chamada de **GetNextRows** se torna uma viagem de ida e volta. Dessa forma, podem existir vários objetos de comando ativos, cada um processando um conjunto de linhas que é o resultado uma busca do cursor de servidor. Para obter mais informações, confira [Conjuntos de linha e cursores do SQL Server](../native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Consulte também  
 [Comandos](commands.md)  
  
  
