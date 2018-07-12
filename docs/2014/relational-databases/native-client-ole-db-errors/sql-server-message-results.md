---
title: Resultados de mensagem do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5db120da45f57debacd2717983fe4ea4118cabe
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431835"
---
# <a name="sql-server-message-results"></a>Resultados de mensagem do SQL Server
  O seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] não geram instruções [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor OLE DB do Native Client ou uma contagem de linhas afetadas quando executadas:  
  
-   PRINT  
  
-   RAISERROR com uma severidade de 10 ou menor  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instruções retornam uma ou mais mensagens informativas ou fazem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornar mensagens informativas em vez de resultados de contagens ou conjuntos de linhas. Em uma execução bem-sucedida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client Retorna S_OK e as mensagens estão disponíveis para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client Retorna S_OK e tem um ou mais mensagens informativas disponíveis após a execução de muitas [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções ou a execução do consumidor de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] membro do provedor OLE DB do Native Client função.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client que permite a especificação dinâmica do texto da consulta deve verificar as interfaces de erro após cada execução de função de membro, independentemente do valor do código de retorno, a presença ou ausência de um retornada **IRowset** ou **IMultipleResults** referência da interface ou uma contagem de linhas afetadas.  
  
## <a name="see-also"></a>Consulte também  
 [Erros](errors.md)  
  
  
