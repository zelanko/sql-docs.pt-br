---
title: Cursores de servidor | Microsoft Docs
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
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 689df4a5d8201fa6f7f59ead9ce87de01e0cd705
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118105"
---
# <a name="using-server-cursors"></a>Usando cursores de servidor
  Se um aplicativo ODBC definir qualquer um dos atributos de cursor ODBC para algo diferente dos padrões, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client solicita o servidor para implementar um cursor de servidor de API do mesmo tipo. O uso de cursores de servidor de API libera memória no cliente e pode reduzir significativamente o tráfego de rede entre o cliente e o servidor.  
  
 Uma desvantagem potencial de cursores de servidor de API é que atualmente eles não dão suporte a todas as instruções SQL. Os cursores de servidor de API não podem ser usados para executar:  
  
-   Lotes ou procedimentos armazenados que retornam vários conjuntos de resultados.  
  
-   Instruções SELECT que contêm cláusulas COMPUTE, COMPUTE BY, FOR BROWSE ou INTO.  
  
-   Uma instrução EXECUTE que faz referência a um procedimento armazenado remoto.  
  
 Em caso de conexão a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a execução de uma instrução com essas características usando um cursor de servidor faz com que o cursor seja convertido em um conjunto de resultados padrão. Em caso de conexão a versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], é gerado um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Como os cursores são implementados](how-cursors-are-implemented.md)  
  
  