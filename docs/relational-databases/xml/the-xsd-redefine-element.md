---
title: O elemento &lt;xsd:redefine&gt; | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 74822cb1a24319e1926866da283b1ada379709e8
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="the-ltxsdredefinegt-element"></a>O elemento &lt;xsd:redefine&gt;
  O elemento **redefine** do W3C XSD fornece suporte para redefinição de componentes de esquema. No entanto, o suporte para essa diretiva é potencialmente caro para o desempenho e também exige que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revalide todas as instâncias do tipo de dados **xml** associadas ao esquema redefinido. Portanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a esse elemento. Esquemas XML que incluem o elemento **\<xsd:redefine>** são rejeitados pelo servidor.  
  
 Para atualizar um esquema ou seus componentes, é possível fazer o seguinte:  
  
1.  Crie uma nova coleção de esquema XML com os componentes do esquema modificado.  
  
2.  Redefina o tipo de todos os tipos de dados **xml** (XML DT) que usam a coleção de esquema XML a serem redefinidos para usarem a nova coleção de esquema XML. Para isso, use a opção ALTER COLUMN do comando ALTER TABLE para redefinir o tipo das colunas ou altere as restrições da coleção de esquema XML sobre variáveis ou parâmetros.  
  
3.  Descarte a versão antiga da coleção de esquema XML.  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos e limitações de uso de coleções de esquema XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
