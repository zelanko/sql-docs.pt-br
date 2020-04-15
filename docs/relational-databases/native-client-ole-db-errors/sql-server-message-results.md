---
title: Resultados da mensagem do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 577b609fd2f878e6c97010cac004e0b10b3a4e4e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300953"
---
# <a name="sql-server-message-results"></a>Resultados da mensagem do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  As [!INCLUDE[tsql](../../includes/tsql-md.md)] seguintes instruções não geram conjuntos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de linhas do provedor ULE DB nativo ou uma contagem de linhas afetadas quando executadas:  
  
-   PRINT  
  
-   RAISERROR com uma severidade de 10 ou menor  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instruções retornam uma ou mais mensagens informativas ou fazem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornar mensagens informativas em vez de resultados de contagens ou conjuntos de linhas. Após a execução bem-sucedida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB retorna S_OK, e as mensagens estão disponíveis para o consumidor do provedor OLE DB do Cliente Nativo.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB retorna S_OK e tem uma ou [!INCLUDE[tsql](../../includes/tsql-md.md)] mais mensagens informacionais disponíveis após a execução de muitas declarações ou a execução do consumidor de uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro do provedor DeLE DB do Cliente Nativo.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor Nativo Cliente OLE DB que permite especificação dinâmica do texto de consulta deve verificar interfaces de erro após a execução de cada função de membro, independentemente do valor do código de retorno, da presença ou ausência de uma referência de interface **IRowset** ou **IMultipleResults** retornada ou uma contagem de linhas afetadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Errors](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
