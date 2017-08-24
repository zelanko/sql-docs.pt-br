---
title: Ancestrais (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ANCESTORS
dev_langs:
- kbMDX
helpviewer_keywords:
- Ancestors function
ms.assetid: abdf2e9c-72c8-4f2e-a823-d42efc4cc7d5
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b2d6304b9a87bcdb87a98a8351d4e60074ebb4d8
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="ancestors-mdx"></a>Ancestors (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Uma função que retorna o conjunto de todos os ancestrais de um membro especificado em um nível especificado, ou à distância especificada, a partir do membro. Com [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], o conjunto retornado consistirá sempre em um único membro - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não dá suporte a vários pais para um único membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Level syntax  
Ancestors(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestors(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
 *Level_Expression*  
 Uma linguagem MDX válida que retorna um nível.  
  
 *Distância*  
 Uma expressão numérica válida que especifica a distância do membro especificado.  
  
## <a name="remarks"></a>Comentários  
 Com o **ancestrais** função, que você fornecer a função com uma expressão de membro MDX e, em seguida, forneça o uma expressão MDX de um nível que é um ancestral daquele membro ou uma expressão numérica que representa o número de níveis acima daquele membro. Com essas informações, o **ancestrais** função retorna o conjunto de membros (que será um conjunto consiste em um membro) naquele nível.  
  
> [!NOTE]  
>  Para retornar um membro ancestral, em vez de um conjunto ancestral, use o [ancestral](../mdx/ancestor-mdx.md) função.  
  
 Se uma expressão de nível for especificada, o **ancestrais** função retorna o conjunto de todos os ancestrais do membro especificado no nível especificado. Se o membro especificado não está dentro da mesma hierarquia como o nível especificado, a função retornará um erro.  
  
 Se uma distância for especificada, o **ancestrais** função retorna o conjunto de todos os membros que são o número de etapas especificadas na hierarquia especificada por uma expressão de membro. Um membro pode ser especificado como um membro de uma hierarquia de atributo, uma hierarquia definida pelo usuário, ou, em alguns casos, uma hierarquia pai-filho. Um número 1 retorna o conjunto de membros no nível pai, e um número 2 retorna o conjunto de membros no nível avô (se houver um). Um número 0 retorna o conjunto que inclui só o próprio membro.  
  
> [!NOTE]  
>  Use este formulário do **ancestrais** função para casos em que o nível do pai é desconhecido ou não pode ser nomeado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa o **ancestrais** função para retornar a medida quantidade de vendas pela Internet para um membro, seu pai e seu avô. Este exemplo usa expressões de nível para especificar os níveis a serem retornados. Os níveis estão na mesma hierarquia que o membro especificado na expressão de membro.  
  
```  
SELECT {  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Category]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Subcategory]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Product])  
    } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 O exemplo a seguir usa o **ancestrais** função para retornar a medida quantidade de vendas pela Internet para um membro, seu pai e seu avô. Este exemplo usa expressões numéricas para especificar os níveis que são retornados. Os níveis estão na mesma hierarquia que o membro especificado na expressão de membro.  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],2  
      ),  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],1  
      ),  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],0  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM  [Adventure Works]  
```  
  
 O exemplo a seguir usa o **ancestrais** função para retornar a medida quantidade de vendas pela Internet para o pai de um membro de uma hierarquia de atributo. Este exemplo usa uma expressão numérica para especificar o nível que é retornado. Desde que o membro na expressão de membro seja um membro de uma hierarquia de atributo, seu pai é o nível [All].  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product].[Mountain-100 Silver, 38],1  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

