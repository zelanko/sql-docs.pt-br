---
title: Usando cursores do servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4e8bcae5ab64fff47528c30a67c13fd1c859ea4e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702035"
---
# <a name="using-server-cursors"></a>Usando cursores de servidor
  Se um aplicativo ODBC definir qualquer um dos atributos de cursor do ODBC para qualquer coisa diferente dos padrões, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client solicitará que o servidor implemente um cursor do servidor de API do mesmo tipo. O uso de cursores de servidor de API libera memória no cliente e pode reduzir significativamente o tráfego de rede entre o cliente e o servidor.  
  
 Uma desvantagem potencial de cursores de servidor de API é que atualmente eles não dão suporte a todas as instruções SQL. Os cursores de servidor de API não podem ser usados para executar:  
  
-   Lotes ou procedimentos armazenados que retornam vários conjuntos de resultados.  
  
-   Instruções SELECT que contêm cláusulas COMPUTE, COMPUTE BY, FOR BROWSE ou INTO.  
  
-   Uma instrução EXECUTE que faz referência a um procedimento armazenado remoto.  
  
 Em caso de conexão a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a execução de uma instrução com essas características usando um cursor de servidor faz com que o cursor seja convertido em um conjunto de resultados padrão. Em caso de conexão a versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], é gerado um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Como os cursores são implementados](how-cursors-are-implemented.md)  
  
  
