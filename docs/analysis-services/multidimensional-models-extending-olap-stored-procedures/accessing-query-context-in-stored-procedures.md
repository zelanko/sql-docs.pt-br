---
title: Acessar o contexto de consulta nos procedimentos armazenados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13facbc44747bedc6f28e1ff4d3bda81b60004ad
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="accessing-query-context-in-stored-procedures"></a>Acessando o contexto de consulta nos procedimentos armazenados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
  
