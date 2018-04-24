---
title: Suporte a namespace no modo PATH | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- PATH FOR XML mode, namespace support
- namespaces [XML in SQL Server]
ms.assetid: 5f128ea2-0ceb-4b23-bce7-c8b3fd615466
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2244272fbcae4b7e31bb391720f34c76fa279904
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="namespace-support-in-path-mode"></a>Suporte a namespace em modo PATH
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  O suporte a namespace em modo PATH é fornecido usando WITH NAMESPACES. Por exemplo, a consulta a seguir demonstra a sintaxe de WITH NAMESPACES para declarar um namespace ("a:") que pode , em seguida, ser usado na instrução SELECT subsequente.  
  
```  
WITH XMLNAMESPACES('a' as a)  
SELECT 1 as 'a:b'  
FOR XML PATH  
```  
  
## <a name="examples"></a>Exemplos  
 Esses exemplos ilustram o uso do modo PATH para gerar XML de uma consulta SELECT. Muitas dessas consultas são especificadas em relação a documentos XML de instruções da fabricação de bicicletas que são armazenados na coluna Instructions da tabela ProductModel.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
