---
title: Salvando um pacote programaticamente | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: f6b99377f6eaf720b9511b560e5cf563ede2b869
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="saving-a-package-programmatically"></a>Salvando um pacote programaticamente
  Depois de criar um pacote novo programaticamente, ou modificar um existente, em geral você deseja salvar as alterações.  
  
 Todos os métodos usados nesse tópico para salvar pacotes exigem uma referência ao assembly **Microsoft.SqlServer.ManagedDTS** . Após adicionar a referência em um novo projeto, importe o <xref:Microsoft.SqlServer.Dts.Runtime> namespace com um **usando** ou **Imports** instrução.  
  
## <a name="saving-a-package-programmatically"></a>Salvando um pacote programaticamente  
 Para salvar um pacote programaticamente, chame um dos seguintes métodos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application> classe:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Arquivo|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> ou<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  Os métodos da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabalhar com o Repositório de Pacotes SSIS só dão suporte a "." ou ao nome do servidor local. Você não pode usar"(local)" ou "localhost".  
  
## <a name="see-also"></a>Consulte também  
 [Salvar pacotes](../../integration-services/save-packages.md)  
  
  

