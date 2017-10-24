---
title: "Componentes e provedores de serviço | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8f574b00b5c53caef2184d2923e79746d3ef56c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="service-providers-and-components"></a>Provedores de serviços e componentes
Provedores de serviços são componentes que estendem a funcionalidade dos provedores de dados implementando interfaces estendidas que não são suportados nativamente pelo repositório de dados.  
  
 Fornece acesso a dados universal um *arquitetura do componente* que permite que os componentes individuais, especializados implementar conjuntos distintos de funcionalidade de banco de dados, ou "serviços" sobre repositórios de menor capacidade. Assim, em vez de imposição de cada repositório de dados para fornecer sua própria implementação da funcionalidade estendida ou forçar aplicativos genéricos para implementar a funcionalidade de banco de dados internamente, componentes de serviço fornecem uma implementação comum que qualquer aplicativo pode Use quando acessar qualquer repositório de dados. O fato de que algumas funcionalidades é implementada nativamente pelo repositório de dados e outros componentes genérico é transparente para o aplicativo.  
  
 Por exemplo, um cursor do mecanismo, como [o serviço de Cursor do OLE DB](http://msdn.microsoft.com/en-us/57638feb-4ecd-4051-becb-8f828d21cf44), é um componente de serviço que pode consumir dados de um repositório de dados sequenciais e somente de encaminhamento para produzir dados roláveis. Outros provedores de serviço usadas pelo ADO incluem o [provedor Microsoft OLE DB persistência (provedor de serviços de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (para salvar dados em um arquivo), o [Microsoft Data Shaping Service para OLE DB (provedor de serviços de ADO) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (para hierárquica **conjuntos de registros**) e o [provedor Microsoft OLE DB Remoting (provedor de serviços de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (para invocar os provedores de dados em um computador remoto).  
  
 Para obter mais informações sobre os provedores de serviços e dados, consulte [apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md).

