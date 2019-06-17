---
title: Conceitos básicos do ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bbff704e174dd824eca7b1f71c8f9d3fc15def51
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704418"
---
# <a name="ado-md-fundamentals"></a>Conceitos básicos do ADO MD
Microsoft® ActiveX® Data Objects (Multidimensional) (ADO MD) oferece acesso fácil a dados multidimensionais de linguagens como Microsoft Visual Basic®, Microsoft Visual C++®. ADO MD estende o Microsoft ActiveX® Data Objects (ADO) para incluir objetos específicos para dados multidimensionais, como o [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) e [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objetos. Com o ADO MD procurar esquema multidimensional, um cubo de consulta e recuperar os resultados.  
  
 Como ADO, o ADO MD usa um provedor OLE DB subjacente para obter acesso aos dados. Para trabalhar com ADO MD, o provedor deve ser um provedor de dados multidimensional (MDP) conforme definido pelo OLE DB para a especificação OLAP. Um MDP apresenta os dados nos modos de exibição multidimensionais em vez de modos de exibição tabulares, que é como um provedor de dados de tabela (TDP) apresenta os dados. Consulte a documentação para o seu provedor de OLE DB OLAP para obter mais informações sobre a sintaxe específica e o comportamento compatível com seu provedor.  
  
 Este documento presume um conhecimento prático da linguagem de programação Visual Basic e um conhecimento geral do ADO e OLAP. Para obter mais informações, consulte o [guia do programador do ADO](../../../ado/guide/ado-programmer-s-guide.md) e [OLE DB para Online Analytical Processing (OLAP)](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Visão geral de esquemas Multidimensional e de dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [Manipular dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [Usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [Programando com o ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de objeto do ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Guia do programador do ADO](../../../ado/guide/ado-programmer-s-guide.md)   
 [Extensões ADO para a linguagem de definição de dados e segurança (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [Visão geral de esquemas Multidimensional e de dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programando com ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Manipular dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
