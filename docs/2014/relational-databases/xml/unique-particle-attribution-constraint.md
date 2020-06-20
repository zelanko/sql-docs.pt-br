---
title: Restrição de atribuição de partícula exclusiva | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
f1_keywords:
- unique particle attribution
helpviewer_keywords:
- schema collections [SQL Server], unique particle attribution
- XML schema collections [SQL Server], unique particle attribution
- UPA constraint rule
- unique particle attribution constraint rule
ms.assetid: 6bb879e9-a5ee-402e-94e4-fe8cec5966b0
author: rothja
ms.author: jroth
ms.openlocfilehash: 62c87f71ea77a6a6a5b19c2faf913425aed816b8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059421"
---
# <a name="unique-particle-attribution-constraint"></a>Restrição de atribuição de partícula exclusiva
  Em XSD, modelos de conteúdo complexos são restritos pela regra de restrição UPA (atribuição de partícula exclusiva). Essa regra requer que cada elemento em um documento da instância corresponda sem-ambiguidade a exatamente uma partícula `<xsd:element>` ou `<xsd:any>` no modelo de conteúdo de seu pai. Qualquer esquema que contenha um tipo com um modelo de conteúdo potencialmente ambíguo é rejeitado.  
  
 Os casos mais comuns de ambiguidade são caracteres curinga `<xsd:any>` e partículas que têm intervalos variáveis de ocorrências, como minOccurs < maxOccurs. Por exemplo, o modelo de conteúdo a seguir é ambíguo porque um elemento <`e1`> pode corresponder ao elemento `<xsd:element>` ou `<xsd:any>`.  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
            <xsd:element name="e1"/>  
            <xsd:any namespace="##any"/>  
        </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 O modelo de conteúdo seguinte também é ambíguo:  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:sequence>  
            <xsd:element name="e1" maxOccurs="2"/>  
            <xsd:element name="e2" minOccurs="0"/>  
            <xsd:element name="e1"/>  
        </xsd:sequence>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 Embora seja possível validar um documento como `<root><e1/><e2/><e1/></root>` de maneira não ambígua, um documento como `<root><e1/><e1/></root>` não pode ser validado, porque não está claro para qual `<xsd:element>` o segundo `<e1/>` corresponde. Embora alguns documentos possam ser validados de maneira não ambígua, o esquema será rejeitado por causa do potencial de ambiguidade.  
  
 Observe que para que um modelo de conteúdo seja válido, deve ser possível validar todas as suas instâncias de maneira não ambígua sem olhar adiante. Por exemplo, considere o seguinte modelo de conteúdo:  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e2"/>  
           </xsd:sequence>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e3"/>  
           </xsd:sequence>  
       </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 Para um documento como `<root><e1/><e3/></root>`, a sequência `<e1/><e3/>` corresponde de maneira não ambígua à segunda `<xsd:sequence>`. No entanto, como o `<xsd:element>` ao qual `<e1/>` corresponde não pode ser determinado sem olhar adiante para `<e3/>`, o modelo de conteúdo viola a regra de restrição de UPA.  
  
## <a name="finding-more-information"></a>Descobrindo mais informações  
 O documento a seguir é publicado pelo World Wide Web Consortium (W3C) e contém a descrição técnica da restrição de atribuição de partícula ambígua.  
  
 "XML Schema Part 1: Structures Second Edition, W3C Proposed Edited Recommendation":  
  
-   Section 3.8.6: Constraints on Model Group Schema Components  
  
-   Appendix H: Analysis of the Unique Particle Attribution Constraint (non-normative)  
  
 Para consultar o documento, visite [http://www.w3.org/TR/xmlschema-1](https://go.microsoft.com/fwlink/?linkid=48881).  
  
## <a name="see-also"></a>Consulte Também  
 [Coleções de esquemas XML &#40;SQL Server&#41;](xml-schema-collections-sql-server.md)  
  
  
