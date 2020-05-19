---
title: Transformações XSLT | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
author: rothja
ms.author: jroth
ms.openlocfilehash: 8556576656d4b6eb6ba5e38216a78074cd1f9fc4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748206"
---
# <a name="xslt-transformations"></a>Transformações XSLT
O XSLT pode ser aplicado ao XML gerado para transformá-lo em outro formato. Entender o formato XML no ADO ajuda a desenvolver modelos XSLT que podem transformá-los em um formulário mais amigável.  
  
 Por exemplo, você sabe que cada linha do conjunto de registros é salva como o elemento z:Row dentro do elemento RS: Data. Da mesma forma, cada campo do conjunto de registros é salvo como um par atributo-valor para esse elemento.  
  
## <a name="remarks"></a>Comentários  
 O script XSLT a seguir pode ser aplicado ao XML mostrado na seção anterior para transformá-lo em uma tabela HTML a ser exibida no navegador:  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 O XSLT converte o fluxo XML gerado pelo método ADO Save em uma tabela HTML que exibe cada campo do conjunto de registros junto com um título de tabela. As linhas e os cabeçalhos de tabela também recebem fontes e cores diferentes.  
  
## <a name="see-also"></a>Consulte Também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
