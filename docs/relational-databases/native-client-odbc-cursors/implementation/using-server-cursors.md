---
title: Usando cursores de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3ae2321d41d9c6938ae771998bdb365f0d25695f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37412675"
---
# <a name="using-server-cursors"></a>Usando cursores de servidor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Se um aplicativo ODBC definir qualquer um dos atributos de cursor ODBC para algo diferente dos padrões, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client solicitará que o servidor para implementar um cursor de servidor de API do mesmo tipo. O uso de cursores de servidor de API libera memória no cliente e pode reduzir significativamente o tráfego de rede entre o cliente e o servidor.  
  
 Uma desvantagem potencial de cursores de servidor de API é que atualmente eles não dão suporte a todas as instruções SQL. Os cursores de servidor de API não podem ser usados para executar:  
  
-   Lotes ou procedimentos armazenados que retornam vários conjuntos de resultados.  
  
-   Instruções SELECT que contêm cláusulas COMPUTE, COMPUTE BY, FOR BROWSE ou INTO.  
  
-   Uma instrução EXECUTE que faz referência a um procedimento armazenado remoto.  
  
 Em caso de conexão a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a execução de uma instrução com essas características usando um cursor de servidor faz com que o cursor seja convertido em um conjunto de resultados padrão. Em caso de conexão a versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], é gerado um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Como os cursores são implementados](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
