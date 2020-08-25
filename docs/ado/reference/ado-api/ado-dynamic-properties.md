---
description: Propriedades dinâmicas do ADO
title: Propriedades dinâmicas do ADO | Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: rothja
ms.author: jroth
ms.openlocfilehash: 83ab2320d3400c5be066af246b50daccaf468462
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771755"
---
# <a name="ado-dynamic-properties"></a>Propriedades dinâmicas do ADO
As propriedades dinâmicas podem ser adicionadas às coleções de [Propriedades](./properties-collection-ado.md) dos objetos [Connection](./connection-object-ado.md), [Command](./command-object-ado.md)ou [Recordset](./recordset-object-ado.md) . A origem dessas propriedades é um provedor de dados, como o provedor de [OLE DB para SQL Server](../../guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)ou um provedor de serviços, como o [serviço de cursor da Microsoft para OLE DB](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md). Consulte a documentação apropriada do provedor de dados ou provedor de serviços para obter mais informações sobre uma propriedade dinâmica específica.  
  
 O [índice de propriedades dinâmicas do ADO](./ado-dynamic-property-index.md) fornece uma referência cruzada entre os nomes do ADO e do OLE DB para cada propriedade dinâmica do provedor de OLE DB padrão.  
  
 As propriedades dinâmicas a seguir são especialmente interessantes e também estão documentadas nas fontes que foram mencionadas anteriormente. A funcionalidade especial com ADO está documentada nos tópicos da ajuda do ADO na lista a seguir.  
  
|Propriedade dinâmica|Descrição|  
|-|-|  
|[Otimizar](./optimize-property-dynamic-ado.md)|Especifica se um índice deve ser criado neste campo.|  
|[Prompt](./prompt-property-dynamic-ado.md)|Especifica se o provedor de OLE DB deve solicitar informações de inicialização ao usuário.|  
|[Remodelar nome](./reshape-name-property-dynamic-ado.md)|Especifica um nome para o objeto **Recordset** .|  
|[Comando Ressync](./resync-command-property-dynamic-ado.md)|Especifica uma cadeia de caracteres de comando fornecida pelo usuário que o método de **ressincronização** emite para atualizar os dados na tabela nomeada na propriedade dinâmica da **tabela exclusiva** .|  
|[Tabela exclusiva, esquema exclusivo, catálogo exclusivo](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**Tabela exclusiva** Especifica o nome da tabela base na qual são permitidas atualizações, inserções e exclusões.<br /><br /> **Esquema exclusivo** Especifica o esquema ou o nome do proprietário da tabela.<br /><br /> **Catálogo exclusivo** Especifica o catálogo ou o nome do banco de dados que contém a tabela.|  
|[Atualizar ressincronização](./update-resync-property-dynamic-ado.md)|Especifica se o método **UpdateBatch** é seguido por uma operação de método de **ressincronização** implícita e, nesse caso, o escopo dessa operação.|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](./ado-api-reference.md)   
 [Coleções ADO](./ado-collections.md)   
 [Constantes enumeradas do ADO](./ado-enumerated-constants.md)   
 [Apêndice B: erros do ADO](../../guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](./ado-events.md)   
 [Métodos do ADO](./ado-methods.md)   
 [Modelo de objeto ADO](./ado-object-model.md)   
 [Objetos e interfaces do ADO](./ado-objects-and-interfaces.md)   
 [Propriedades ADO](./ado-properties.md)