---
description: Provedores de serviços e componentes
title: Provedores de serviços e componentes | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d8405ad88ca2fc087eb6f71f665a508690bf1142
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452868"
---
# <a name="service-providers-and-components"></a>Provedores de serviços e componentes
Provedores de serviço são componentes que estendem a funcionalidade de provedores de dados implementando interfaces estendidas que não têm suporte nativo do armazenamento de dados.  
  
 O Universal Data Access fornece uma *arquitetura de componentes* que permite que componentes individuais e especializados implementem conjuntos discretos de funcionalidade de banco de dados, ou "serviços", em cima de lojas com menos capacidade. Portanto, em vez de forçar cada repositório de dados a fornecer sua própria implementação de funcionalidade estendida ou forçar aplicativos genéricos para implementar a funcionalidade de banco de dados internamente, os componentes de serviço fornecem uma implementação comum que qualquer aplicativo pode usar ao acessar qualquer armazenamento de dado. O fato de que algumas funcionalidades são implementadas nativamente pelo armazenamento de dados e alguns por meio de componentes genéricos é transparente para o aplicativo.  
  
 Por exemplo, um mecanismo de cursor, como [o serviço de cursor para OLE DB](https://msdn.microsoft.com/57638feb-4ecd-4051-becb-8f828d21cf44), é um componente de serviço que pode consumir dados de um armazenamento de dados sequencial somente de encaminhamento para produzir dados roláveis. Outros provedores de serviços comumente usados pelo ADO incluem o [provedor de persistência do microsoft OLE DB (provedor de serviços ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (para salvar dados em um arquivo), o [Microsoft Data Shaping Service para OLE DB (provedor de serviços ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (para **conjuntos de registros**hierárquicos) e o provedor de [comunicação remota do Microsoft OLE DB (provedor de serviços ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (para invocar provedores de dados em um computador remoto)  
  
 Para obter mais informações sobre provedores de dados e serviço, consulte [o apêndice A: provedores](../../../ado/guide/appendixes/appendix-a-providers.md).
