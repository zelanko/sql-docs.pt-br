---
title: O elemento &lt;xsd:redefine&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8d7fe9246e0b689335d43a124c4a2391778f127a
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48905010"
---
# <a name="the-ltxsdredefinegt-element"></a>O elemento &lt;xsd:redefine&gt;
  O elemento **redefine** do W3C XSD fornece suporte para redefinição de componentes de esquema. Entretanto, há suporte para essa diretiva é potencialmente cara para o desempenho e também requer que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revalide todas as instâncias da `xml` tipo de dados associado ao esquema redefinido. Portanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a esse elemento. Esquemas XML que incluem o elemento **\<xsd:redefine>** são rejeitados pelo servidor.  
  
 Para atualizar um esquema ou seus componentes, é possível fazer o seguinte:  
  
1.  Crie uma nova coleção de esquema XML com os componentes do esquema modificado.  
  
2.  Digite novamente todos os `xml` tipos de dados (XML DT) que usam a coleção de esquemas XML a serem redefinidos para usarem a nova coleção de esquema XML em vez disso. Para isso, use a opção ALTER COLUMN do comando ALTER TABLE para redefinir o tipo das colunas ou altere as restrições da coleção de esquema XML sobre variáveis ou parâmetros.  
  
3.  Descarte a versão antiga da coleção de esquema XML.  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos e limitações de uso de coleções de esquema XML no servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
