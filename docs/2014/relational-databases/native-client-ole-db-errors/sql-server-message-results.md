---
title: Resultados da mensagem do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 19c0c3b044943e51c6d791e962fa830f0b6d0144
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704932"
---
# <a name="sql-server-message-results"></a>Resultados da mensagem do SQL Server
  As instruções a seguir [!INCLUDE[tsql](../../includes/tsql-md.md)] não geram [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor de OLE DB do cliente nativo ou uma contagem de linha afetada quando executadas:  
  
-   PRINT  
  
-   RAISERROR com uma severidade de 10 ou menor  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instruções retornam uma ou mais mensagens informativas ou fazem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornar mensagens informativas em vez de resultados de contagens ou conjuntos de linhas. Após a execução bem-sucedida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retorna S_OK e as mensagens estão disponíveis para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor de OLE DB do cliente nativo.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retorna S_OK e tem uma ou mais mensagens informativas disponíveis após a execução de muitas [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções ou a execução do consumidor de uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro do provedor de OLE DB de cliente nativo.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor de OLE DB de cliente nativo que permite a especificação dinâmica do texto da consulta deve verificar as interfaces de erro depois de cada execução de função de membro, independentemente do valor do código de retorno, da presença ou da ausência de uma referência de interface **IRowset** ou **IMultipleResults** retornada ou de uma contagem de linhas afetadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](errors.md)  
  
  
