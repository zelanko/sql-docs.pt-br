---
title: ICommand (OLE DB) | Microsoft Docs
description: Interface ICommand (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3f8599e9e353b4683b59e5717e25812b8562aed8
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35305995"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este artigo aborda o comportamento de OLE DB que é específico do OLE DB do driver para SQL Server.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 Inserir dados maiores do que o tamanho de uma coluna normalmente resulta em um erro. No entanto, existem situações em que S_OK será retornado, mas *dwStatus* será definido como DBSTATUS_S_TRUNCATED. Ele geralmente ocorre ao inserir dados com parâmetros, onde a coluna não é grande o suficiente para manter os dados, e **ICommandWithParameters:: SetParameterInfo** ainda não foi chamado.  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
