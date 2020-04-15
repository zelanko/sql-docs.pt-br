---
title: Usando cursors de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ede31d9d59ef7d01dfd7e7b610edae273cbc5d64
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305366"
---
# <a name="using-server-cursors"></a>Usando cursores de servidor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Se um aplicativo ODBC definir qualquer um dos atributos do cursor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC para qualquer outra coisa que não seja a inadimplência, o driver ODBC cliente nativo solicita que o servidor implemente um cursor de servidor API do mesmo tipo. O uso de cursores de servidor de API libera memória no cliente e pode reduzir significativamente o tráfego de rede entre o cliente e o servidor.  
  
 Uma desvantagem potencial de cursores de servidor de API é que atualmente eles não dão suporte a todas as instruções SQL. Os cursores de servidor de API não podem ser usados para executar:  
  
-   Lotes ou procedimentos armazenados que retornam vários conjuntos de resultados.  
  
-   Instruções SELECT que contêm cláusulas COMPUTE, COMPUTE BY, FOR BROWSE ou INTO.  
  
-   Uma instrução EXECUTE que faz referência a um procedimento armazenado remoto.  
  
 Em caso de conexão a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a execução de uma instrução com essas características usando um cursor de servidor faz com que o cursor seja convertido em um conjunto de resultados padrão. Em caso de conexão a versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], é gerado um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Como os cursores são implementados](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
