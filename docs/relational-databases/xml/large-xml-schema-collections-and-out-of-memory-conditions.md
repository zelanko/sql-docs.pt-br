---
title: Falta de memória com coleções de esquema XML grandes | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- out-of-memory conditions
- XML schema collections [SQL Server], large
ms.assetid: 29b9d839-aaaf-48fb-be17-840c751f36f1
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 085a59ce8861c3f38e5c7540d4d56201c896ccea
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257650"
---
# <a name="large-xml-schema-collections-and-out-of-memory-conditions"></a>Coleções de esquema XML grandes e condições de memória insuficiente
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Durante uma chamada à função XML_SCHEMA_NAMESPACE() interna em uma coleção de esquema XML grande ou ao tentar descartar grandes coleções de esquema XML, pode ocorrer uma condição de memória insuficiente. Os seguintes soluções podem ser usadas para tratar essa situação:  
  
-   Quando a carga do sistema estiver leve, use o comando DROP_XML_SCHEMA_COLLECTION. Se isso falhar, coloque o banco de dados em modo do usuário único usando a instrução ALTER DATABASE e tente DROP XML SCHEMA COLLECTION novamente. Se a coleção de esquema XML existir em **master**, **model**ou **tempdb**uma reinicialização do servidor será necessária para o modo de usuário único.  
  
-   Ao chamar XML_SCHEMA_NAMESPACE, você pode tentar recuperar um único namespace do esquema XML. A chamada pode ser tentada quando a carga do sistema estiver mais leve ou em modo de usuário único.  
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos e limitações para o uso de Coleções de Esquemas XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
