---
title: Componentes e provedores de serviços | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a78db07f5ba445c54108558b2ff222bd217c2bbe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924242"
---
# <a name="service-providers-and-components"></a>Provedores de serviços e componentes
Provedores de serviço são componentes que estendem a funcionalidade dos provedores de dados com a implementação de interfaces estendidas que não são suportados nativamente pelo armazenamento de dados.  
  
 Fornece acesso a dados universal uma *arquitetura do componente* que permite que os componentes individuais, especializados implementar conjuntos distintos de funcionalidades de banco de dados, ou "serviços", na parte superior de lojas com menor capacidade. Assim, em vez de forçar a cada armazenamento de dados para fornecer sua própria implementação de funcionalidade estendida ou forçar os aplicativos genéricos para implementar a funcionalidade de banco de dados internamente, componentes de serviço fornecem uma implementação comum que qualquer aplicativo pode Use quando acessar qualquer armazenamento de dados. O fato de que algumas funcionalidades é implementada nativamente pelo repositório de dados e outros por meio de componentes genéricos é transparente para o aplicativo.  
  
 Por exemplo, um cursor do mecanismo, como [o Cursor Service para OLE DB](https://msdn.microsoft.com/57638feb-4ecd-4051-becb-8f828d21cf44), é um componente de serviço que pode consumir dados de um armazenamento de dados sequenciais, apenas de encaminhamento para gerar dados roláveis. Outros provedores de serviço usadas pelo ADO incluem o [provedor Microsoft OLE DB persistência (provedor de serviços do ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (para salvar dados em um arquivo), o [Microsoft Data Shaping Service para OLE DB (provedor de serviços do ADO) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (para hierárquica **conjuntos de registros**) e o [provedor Microsoft OLE DB Remoting (provedor de serviços do ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (para invocar os provedores de dados em um computador remoto).  
  
 Para obter mais informações sobre os provedores de serviços e dados, consulte [apêndice a: Provedores de](../../../ado/guide/appendixes/appendix-a-providers.md).
