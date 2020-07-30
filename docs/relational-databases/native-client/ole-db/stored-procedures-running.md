---
title: Executando procedimentos armazenados (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ca0211f6cab19b09ac0be43ba32768511f0f6a4f
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247111"
---
# <a name="stored-procedures---running-in-sql-server-native-client"></a>Procedimentos armazenados-em execução no SQL Server Native Client
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Ao executar instruções, a chamada a um procedimento armazenado na fonte de dados (em vez de executar ou preparar uma instrução diretamente no aplicativo cliente) pode fornecer:  
  
-   Maior desempenho.  
  
-   Menor sobrecarga da rede.  
  
-   Melhor consistência.  
  
-   Maior exatidão.  
  
-   Maior funcionalidade.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte a três dos mecanismos que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] os procedimentos armazenados usam para retornar dados:  
  
-   Toda instrução SELECT no procedimento gera um conjunto de resultados.  
  
-   O procedimento pode retornar dados através de parâmetros de saída.  
  
-   O procedimento pode ter um código de retorno de inteiro.  
  
 O aplicativo precisa ser capaz de tratar todas essas saídas provenientes dos procedimentos armazenados.  
  
 Provedores do OLE DB diferentes retornam parâmetros de saída e valores de retorno em horários diferentes durante o processamento de resultados. No caso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo, os parâmetros de saída e os códigos de retorno não são fornecidos até que o consumidor tenha recuperado ou cancelado os conjuntos de resultados retornados pelo procedimento armazenado. Os códigos de retorno e parâmetros de saída são retornados no último pacote TDS proveniente do servidor.  
  
 Os provedores usam a propriedade DBPROP_OUTPUTPARAMETERAVAILABILITY para informar o momento em que são retornados os parâmetros de saída e valores de retorno. Essa propriedade faz parte do conjunto de propriedades DBPROPSET_DATASOURCEINFO.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo define a propriedade DBPROP_OUTPUTPARAMETERAVAILABILITY como DBPROPVAL_OA_ATROWRELEASE para indicar que os códigos de retorno e os parâmetros de saída não são retornados até que o conjunto de resultados seja processado ou liberado.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
