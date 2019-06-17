---
title: ICommand (OLE DB) | Microsoft Docs
description: Interface ICommand (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 9622dfa505fd00bca639d1cfd8919aef4145a85a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790666"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artigo descreve o comportamento de OLE DB que é específico para o Driver do OLE DB para SQL Server.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 Inserir dados maiores do que o tamanho de uma coluna normalmente resulta em um erro. No entanto, existem situações em que S_OK será retornado, mas *dwStatus* será definido como DBSTATUS_S_TRUNCATED. Isso geralmente ocorre quando os dados são inseridos com parâmetros e a coluna não é grande o suficiente para armazenar os dados e **ICommandWithParameters::SetParameterInfo** não foi chamado.  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
