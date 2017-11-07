---
title: Acessar o contexto de consulta nos procedimentos armazenados | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- execution context [Analysis Services]
- stored procedures [Analysis Services], query context
- Context object
- query context [Analysis Services]
ms.assetid: bdc7dad8-2f22-4265-aba4-a3a451527840
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ea922bed66dbcb625614259346794c9ba7856e9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="accessing-query-context-in-stored-procedures"></a>Acessando o contexto de consulta nos procedimentos armazenados
  O contexto de execução de um procedimento armazenado está disponível dentro do código do procedimento armazenado como o **contexto** objeto do modelo de objeto de servidor do ADOMD.NET. Trata-se de um contexto somente leitura e que não pode ser modificado pelo procedimento armazenado. As propriedades a seguir estão disponíveis nesse objeto.  
  
|Propriedade|Tipo|Description|  
|--------------|----------|-----------------|  
|**CurrentCube**|Cube|O cubo do contexto de consulta atual.|  
|**CurrentDatabaseName**|Cadeia de caracteres|O identificador do banco de dados atual.|  
|**CurrentConnection**|Conexão|Uma referência ao objeto de conexão no contexto atual.|  
|**Passar**|Integer|O número da passagem do contexto atual.|  
  
 O **contexto** objeto existe quando o modelo de objeto MDX (Multidimensional Expressions) é usado em um procedimento armazenado. Ele não estará disponível quando o modelo de objeto MDX for usado em um cliente. O **contexto** objeto é passado para ou retornado pelo procedimento armazenado não explicitamente. Ele fica disponível durante a execução do procedimento armazenado.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de Assemblies de modelo multidimensional](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definindo procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  

