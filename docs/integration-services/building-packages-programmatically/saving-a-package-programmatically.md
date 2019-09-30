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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7a65b7559770b6de0d1ebd928815458c02acfd41
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71299047"
---
# <a name="saving-a-package-programmatically"></a>Salvando um pacote programaticamente

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
  
