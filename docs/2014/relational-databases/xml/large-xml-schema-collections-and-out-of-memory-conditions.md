---
title: Coleções de esquemas XML grandes e condições de memória insuficiente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- out-of-memory conditions
- XML schema collections [SQL Server], large
ms.assetid: 29b9d839-aaaf-48fb-be17-840c751f36f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 513e95798062f85484b5693d5c75e6aef3efcc82
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63285553"
---
# <a name="large-xml-schema-collections-and-out-of-memory-conditions"></a>Coleções de esquema XML grandes e condições de memória insuficiente
  Durante uma chamada à função XML_SCHEMA_NAMESPACE() interna em uma coleção de esquema XML grande ou ao tentar descartar grandes coleções de esquema XML, pode ocorrer uma condição de memória insuficiente. Os seguintes soluções podem ser usadas para tratar essa situação:  
  
-   Quando a carga do sistema estiver leve, use o comando DROP_XML_SCHEMA_COLLECTION. Se isso falhar, coloque o banco de dados em modo do usuário único usando a instrução ALTER DATABASE e tente DROP XML SCHEMA COLLECTION novamente. Se a coleção de esquema XML existir em **master**, **model**ou **tempdb**uma reinicialização do servidor será necessária para o modo de usuário único.  
  
-   Ao chamar XML_SCHEMA_NAMESPACE, você pode tentar recuperar um único namespace do esquema XML. A chamada pode ser tentada quando a carga do sistema estiver mais leve ou em modo de usuário único.  
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos e limitações para o uso de Coleções de Esquemas XML no servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
