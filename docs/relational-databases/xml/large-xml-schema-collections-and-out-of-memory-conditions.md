---
title: "Coleções de esquemas XML grandes e condições de memória insuficiente | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- out-of-memory conditions
- XML schema collections [SQL Server], large
ms.assetid: 29b9d839-aaaf-48fb-be17-840c751f36f1
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 61ed00e41622ed19c9707974921e68a12d66e020
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="large-xml-schema-collections-and-out-of-memory-conditions"></a>Coleções de esquema XML grandes e condições de memória insuficiente
  Durante uma chamada à função XML_SCHEMA_NAMESPACE() interna em uma coleção de esquema XML grande ou ao tentar descartar grandes coleções de esquema XML, pode ocorrer uma condição de memória insuficiente. Os seguintes soluções podem ser usadas para tratar essa situação:  
  
-   Quando a carga do sistema estiver leve, use o comando DROP_XML_SCHEMA_COLLECTION. Se isso falhar, coloque o banco de dados em modo do usuário único usando a instrução ALTER DATABASE e tente DROP XML SCHEMA COLLECTION novamente. Se a coleção de esquema XML existir em **master**, **model**ou **tempdb**uma reinicialização do servidor será necessária para o modo de usuário único.  
  
-   Ao chamar XML_SCHEMA_NAMESPACE, você pode tentar recuperar um único namespace do esquema XML. A chamada pode ser tentada quando a carga do sistema estiver mais leve ou em modo de usuário único.  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos e limitações de uso de coleções de esquema XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
