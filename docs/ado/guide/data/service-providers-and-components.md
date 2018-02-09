---
title: "Componentes e provedores de serviço | Microsoft Docs"
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
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97e738fb4f5bd4635a8a53a87d000b72736edc5d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="service-providers-and-components"></a>Provedores de serviços e componentes
Provedores de serviços são componentes que estendem a funcionalidade dos provedores de dados implementando interfaces estendidas que não são suportados nativamente pelo repositório de dados.  
  
 Fornece acesso a dados universal um *arquitetura do componente* que permite que os componentes individuais, especializados implementar conjuntos distintos de funcionalidade de banco de dados, ou "serviços" sobre repositórios de menor capacidade. Assim, em vez de imposição de cada repositório de dados para fornecer sua própria implementação da funcionalidade estendida ou forçar aplicativos genéricos para implementar a funcionalidade de banco de dados internamente, componentes de serviço fornecem uma implementação comum que qualquer aplicativo pode Use quando acessar qualquer repositório de dados. O fato de que algumas funcionalidades é implementada nativamente pelo repositório de dados e outros componentes genérico é transparente para o aplicativo.  
  
 Por exemplo, um cursor do mecanismo, como [o serviço de Cursor do OLE DB](http://msdn.microsoft.com/en-us/57638feb-4ecd-4051-becb-8f828d21cf44), é um componente de serviço que pode consumir dados de um repositório de dados sequenciais e somente de encaminhamento para produzir dados roláveis. Outros provedores de serviço usadas pelo ADO incluem o [provedor Microsoft OLE DB persistência (provedor de serviços de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (para salvar dados em um arquivo), o [Microsoft Data Shaping Service para OLE DB (provedor de serviços de ADO) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (para hierárquica **conjuntos de registros**) e o [provedor Microsoft OLE DB Remoting (provedor de serviços de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (para invocar os provedores de dados em um computador remoto).  
  
 Para obter mais informações sobre os provedores de serviços e dados, consulte [apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md).
