---
title: Propriedades dinâmicas do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71396a071a42d7dd40a6537a2834541aab2b6bad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921090"
---
# <a name="ado-dynamic-properties"></a>Propriedades dinâmicas do ADO
As propriedades dinâmicas podem ser adicionadas às coleções de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) dos objetos [Connection](../../../ado/reference/ado-api/connection-object-ado.md), [Command](../../../ado/reference/ado-api/command-object-ado.md)ou [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) . A origem dessas propriedades é um provedor de dados, como o provedor de [OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)ou um provedor de serviços, como o [serviço de cursor da Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md). Consulte a documentação apropriada do provedor de dados ou provedor de serviços para obter mais informações sobre uma propriedade dinâmica específica.  
  
 O [índice de propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) fornece uma referência cruzada entre os nomes do ADO e do OLE DB para cada propriedade dinâmica do provedor de OLE DB padrão.  
  
 As propriedades dinâmicas a seguir são especialmente interessantes e também estão documentadas nas fontes que foram mencionadas anteriormente. A funcionalidade especial com ADO está documentada nos tópicos da ajuda do ADO na lista a seguir.  
  
|||  
|-|-|  
|[Formato](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Especifica se um índice deve ser criado neste campo.|  
|[Prompt](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|Especifica se o provedor de OLE DB deve solicitar informações de inicialização ao usuário.|  
|[Remodelar nome](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Especifica um nome para o objeto **Recordset** .|  
|[Comando Ressync](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Especifica uma cadeia de caracteres de comando fornecida pelo usuário que o método de **ressincronização** emite para atualizar os dados na tabela nomeada na propriedade dinâmica da **tabela exclusiva** .|  
|[Tabela exclusiva, esquema exclusivo, catálogo exclusivo](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**Tabela exclusiva** Especifica o nome da tabela base na qual são permitidas atualizações, inserções e exclusões.<br /><br /> **Esquema exclusivo** Especifica o esquema ou o nome do proprietário da tabela.<br /><br /> **Catálogo exclusivo** Especifica o catálogo ou o nome do banco de dados que contém a tabela.|  
|[Atualizar ressincronização](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|Especifica se o método **UpdateBatch** é seguido por uma operação de método de **ressincronização** implícita e, nesse caso, o escopo dessa operação.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice B: erros do ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos do ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Objetos e interfaces do ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
