---
title: Elemento HelpLink | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 39db57e1c1acb0a63c6054b4be2975e05502dd91
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104626"
---
# <a name="helplink-element"></a>Elemento HelpLink
  O elemento **HelpLink** da propriedade **Detail** é uma cadeia de caracteres de URL gerada pelo servidor de relatório. A URL tem como destino uma página da Web gerenciada pela Ajuda e Suporte do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] e fornece ajuda adicional e artigos da base de dados de conhecimento sobre erros específicos ocorridos no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. A URL tem a seguinte sintaxe:  
  
 **http://** www.microsoft.com**/** products**/** ee**/** transform.aspx **?EvtSrc**=v*alue***&EvtID**=* value ***&ProdName**=* value***&ProdVer**=* value*  
  
 A tabela a seguir lista os argumentos da URL **HelpLink**.  
  
|Argumento|Valor|  
|--------------|-----------|  
|**EvtSrc**|"Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings"|  
|**EvtID**|Por exemplo, o código de erro do servidor de relatório, rsReservedItem.|  
|**ProdName**|"Microsoft SQL%20Server%20Reporting%20Services". O valor do nome do produto é codificado na URL.|  
|**ProdVer**|O número da versão do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Um valor “8,00” indica o [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
  
 O exemplo a seguir ilustra a **HelpLink** URL retornada para o código de erro `rsReservedItem`. Esse erro ocorre quando um usuário tenta modificar ou excluir um item reservado no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]:  
  
```  
http://www.microsoft.com/products/ee/transform.aspx?  
EvtSrc=Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings  
&EvtID=rsReservedItem&ProdName=Microsoft%20SQL%20Server%20Reporting%20Services&ProdVer=8.00  
```  
  
 Acesse o elemento **HelpLink** no código usando a classe **SoapException**.  
  
```vb  
Try  
   rs.DeleteItem("/Report1")  
  
Catch e As SoapException  
   Console.WriteLine(e.Detail("HelpLink").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.DeleteItem("/Report1");  
}  
  
catch (SoapException e)  
{  
   Console.WriteLine(e.Detail["HelpLink"].InnerXml);  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao tratamento de exceção no Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException do Reporting Services](reporting-services-soapexception-class.md)   
 [Usar a propriedade Detail para manipular erros específicos](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
