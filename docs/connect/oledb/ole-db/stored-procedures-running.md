---
title: Executando procedimentos armazenados (OLE DB) | Microsoft Docs
description: Executando procedimentos armazenados (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- OLE DB Driver for SQL Server, stored procedures
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf576884f19f10ae7e82bc479229155775d674f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="stored-procedures---running"></a>Procedimentos armazenados - em execução
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando a execução de instruções, chamar um procedimento armazenado na fonte de dados (em vez de executar ou preparar uma instrução no aplicativo cliente diretamente) pode fornecer:  
  
-   Maior desempenho.  
  
-   Menor sobrecarga da rede.  
  
-   Melhor consistência.  
  
-   Maior exatidão.  
  
-   Maior funcionalidade.  
  
 O Driver OLE DB para SQL Server dá suporte a três dos mecanismos que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usam procedimentos armazenados para retornar dados:  
  
-   Toda instrução SELECT no procedimento gera um conjunto de resultados.  
  
-   O procedimento pode retornar dados através de parâmetros de saída.  
  
-   O procedimento pode ter um código de retorno de inteiro.  
  
 O aplicativo precisa ser capaz de tratar todas essas saídas provenientes dos procedimentos armazenados.  
  
 Provedores do OLE DB diferentes retornam parâmetros de saída e valores de retorno em horários diferentes durante o processamento de resultados. No caso do OLE DB Driver para SQL Server, os parâmetros de saída e códigos de retorno não são fornecidos até depois que o consumidor tiver recuperado ou cancelado os conjuntos de resultados retornados pelo procedimento armazenado. Os códigos de retorno e parâmetros de saída são retornados no último pacote TDS proveniente do servidor.  
  
 Os provedores usam a propriedade DBPROP_OUTPUTPARAMETERAVAILABILITY para informar o momento em que são retornados os parâmetros de saída e valores de retorno. Essa propriedade faz parte do conjunto de propriedades DBPROPSET_DATASOURCEINFO.  
  
 O Driver OLE DB para SQL Server define a propriedade DBPROP_OUTPUTPARAMETERAVAILABILITY como DBPROPVAL_OA_ATROWRELEASE para indicar que os códigos de retorno e parâmetros de saída não são retornados até que o conjunto de resultados é processado ou liberado.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados](../../oledb/ole-db/stored-procedures.md)  
  
  
