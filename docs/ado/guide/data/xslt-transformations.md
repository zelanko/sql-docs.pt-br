---
title: "Transformações XSLT | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7dc90399ec31c921bfebbd342bbc082365dc238d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="xslt-transformations"></a>Transformações XSLT
XSLT pode ser aplicado ao XML gerado para transformá-la em outro formato. Noções básicas sobre o formato XML no ADO ajuda a desenvolver modelos XSLT que podem transformar em um formato mais amigável.  
  
 Por exemplo, você sabe que cada linha do conjunto de registros é salvo como elemento z: linha dentro do elemento de dados do rs:. Da mesma forma, cada campo do conjunto de registros é salvo como um par atributo-valor para este elemento.  
  
## <a name="remarks"></a>Remarks  
 O seguinte script XSLT pode ser aplicado ao XML mostrado na seção anterior para transformá-la em uma tabela HTML a ser exibida no navegador:  
  
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
  
 O XSLT converte o fluxo XML gerado pelo método de ADO salvar em uma tabela HTML que exibe cada campo do conjunto de registros com um cabeçalho de tabela. Linhas e títulos de tabela também são atribuídas diferentes fontes e cores.  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
