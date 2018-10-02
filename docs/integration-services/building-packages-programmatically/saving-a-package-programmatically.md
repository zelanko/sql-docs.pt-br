---
title: Salvar um pacote programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 822f6a364b06c6e2a88c8880cbe97fe94dba510f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650914"
---
# <a name="saving-a-package-programmatically"></a>Salvando um pacote programaticamente
  Depois de criar um pacote novo programaticamente, ou modificar um existente, em geral você deseja salvar as alterações.  
  
 Todos os métodos usados nesse tópico para salvar pacotes exigem uma referência ao assembly **Microsoft.SqlServer.ManagedDTS** . Após adicionar a referência em um novo projeto, importe o namespace <xref:Microsoft.SqlServer.Dts.Runtime> com uma instrução **using** ou **Imports**.  
  
## <a name="saving-a-package-programmatically"></a>Salvando um pacote programaticamente  
 Para salvar um pacote programaticamente, chame um dos seguintes métodos da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Arquivo|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> ou em<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  Os métodos da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabalhar com o Repositório de Pacotes SSIS só dão suporte a "." ou ao nome do servidor local. Você não pode usar"(local)" ou "localhost".  
  
## <a name="see-also"></a>Consulte Também  
 [Salvar pacotes](../../integration-services/save-packages.md)  
  
  
