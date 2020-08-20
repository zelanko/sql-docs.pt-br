---
description: '&lt;consulta de dados &gt; de origem – OPENROWSET'
title: OPENROWSET (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8da3686e7772b7e997690d509c8092917635497a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500752"
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;consulta de dados &gt; de origem – OPENROWSET
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Substitui uma consulta de dados de origem por uma consulta a um provedor externo. As instruções de inserção, seleção de junção de previsão e seleção de junção de previsão NATURAL dão suporte a **OPENROWSET**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>Argumentos  
 *provider_name*  
 Nome de um provedor de OLE DB.  
  
 *provider_string*  
 Cadeia de conexão OLE DB para o provedor especificado.  
  
 *query_syntax*  
 Sintaxe de consulta que retorna um conjunto de linhas.  
  
## <a name="remarks"></a>Comentários  
 O provedor de Data Mining estabelecerá uma conexão com o objeto de fonte de dados usando *provider_name* e *provider_string* e executará a consulta especificada em *query_syntax* para recuperar o conjunto de linhas dos dados de origem.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir pode ser usado em uma instrução PREDICTION JOIN para recuperar dados do banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], usando uma instrução [!INCLUDE[tsql](../includes/tsql-md.md)] SELECT.  
  
```  
OPENROWSET  
(  
'SQLOLEDB.1',  
'Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security     Info=False;Initial Catalog=AdventureWorksDW2012;Data Source=localhost',  
'SELECT TOP 1000 * FROM vTargetMail'  
)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#62;de consulta de dados de origem&#60;](../dmx/source-data-query.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
