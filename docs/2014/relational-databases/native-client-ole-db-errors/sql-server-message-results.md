---
title: Resultados de mensagem do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7d1f6519c927bc8050590c1cc13821a7b7895f8a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011122"
---
# <a name="sql-server-message-results"></a>Resultados de mensagem do SQL Server
  O seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções não geram [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor OLE DB Native Client ou uma contagem de linhas afetadas quando executadas:  
  
-   PRINT  
  
-   RAISERROR com uma severidade de 10 ou menor  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instruções retornam uma ou mais mensagens informativas ou fazem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornar mensagens informativas em vez de resultados de contagens ou conjuntos de linhas. Na execução bem sucedida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client Retorna S_OK e as mensagens estão disponíveis para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB Native Client.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client Retorna S_OK e tem uma ou mais mensagens informativas disponíveis após a execução de várias [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções ou a execução do consumidor de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] membro do provedor OLE DB Native Client função.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB Native Client que permite a especificação dinâmica do texto da consulta deve verificar as interfaces de erro após cada execução da função de membro, independentemente do valor do código de retorno, a presença ou ausência de um retornado**IRowset** ou **IMultipleResults** referência de interface ou uma contagem de linhas afetadas.  
  
## <a name="see-also"></a>Consulte também  
 [Erros](errors.md)  
  
  