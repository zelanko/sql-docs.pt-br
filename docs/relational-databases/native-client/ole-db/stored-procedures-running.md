---
title: Executando procedimentos armazenados (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ed9df8c1c51143442b622e9aa14831ede809a1b6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415395"
---
# <a name="stored-procedures---running"></a>Procedimentos armazenados – execução
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Quando a execução de instruções, chamar um procedimento armazenado na fonte de dados (em vez de executar ou preparar uma instrução no aplicativo cliente diretamente) pode fornecer:  
  
-   Maior desempenho.  
  
-   Menor sobrecarga da rede.  
  
-   Melhor consistência.  
  
-   Maior exatidão.  
  
-   Maior funcionalidade.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client dá suporte a três dos mecanismos que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] procedimentos armazenados usam para retornar dados:  
  
-   Toda instrução SELECT no procedimento gera um conjunto de resultados.  
  
-   O procedimento pode retornar dados através de parâmetros de saída.  
  
-   O procedimento pode ter um código de retorno de inteiro.  
  
 O aplicativo precisa ser capaz de tratar todas essas saídas provenientes dos procedimentos armazenados.  
  
 Provedores do OLE DB diferentes retornam parâmetros de saída e valores de retorno em horários diferentes durante o processamento de resultados. No caso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client, os parâmetros de saída e códigos de retorno não serão fornecidos enquanto depois que o consumidor tiver recuperado ou cancelado os conjuntos de resultados retornados pelo procedimento armazenado. Os códigos de retorno e parâmetros de saída são retornados no último pacote TDS proveniente do servidor.  
  
 Os provedores usam a propriedade DBPROP_OUTPUTPARAMETERAVAILABILITY para informar o momento em que são retornados os parâmetros de saída e valores de retorno. Essa propriedade faz parte do conjunto de propriedades DBPROPSET_DATASOURCEINFO.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client define a propriedade DBPROP_OUTPUTPARAMETERAVAILABILITY como DBPROPVAL_OA_ATROWRELEASE para indicar que os códigos de retornados e parâmetros de saída não são retornados até que o conjunto de resultados for processado ou liberado.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
