---
title: "Propriedades dinâmicas do ADO | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fca9f032f5a72df58b18206c8441365ce3c8a746
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="ado-dynamic-properties"></a>Propriedades dinâmicas do ADO
Propriedades dinâmicas que podem ser adicionadas para o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleções do [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [comando](../../../ado/reference/ado-api/command-object-ado.md), ou [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos. A fonte para essas propriedades é um provedor de dados, como o [OLE DB Provider para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), ou um provedor de serviços, como o [do serviço Microsoft Cursor do OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md). Consulte a documentação do provedor de serviço para obter mais informações sobre uma propriedade dinâmica específica ou provedor de dados apropriado.  
  
 O [índice de propriedade dinâmica de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) fornece uma referência cruzada entre os nomes de ADO e OLE DB para cada propriedade de dinâmico do provedor OLE DB padrão.  
  
 As seguintes propriedades dinâmicas são especialmente interessantes e também estão documentadas nas fontes que foram mencionadas anteriormente. Uma funcionalidade especial com o ADO está documentada nos tópicos da Ajuda ADO na lista a seguir.  
  
|||  
|-|-|  
|[Otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Especifica se um índice deve ser criado neste campo.|  
|[Solicitar](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|Especifica se o provedor OLE DB deve solicitar ao usuário informações de inicialização.|  
|[Alterar a forma de nome](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Especifica um nome para o **registros** objeto.|  
|[Sincronizar de comando](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Especifica um comando fornecido pelo usuário de cadeia de caracteres que o **Resync** problemas de método para atualizar os dados na tabela chamada no **tabela exclusiva** propriedades dinâmicas.|  
|[Tabela exclusiva, o esquema exclusivo, o catálogo exclusivo](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**Tabela exclusiva** Especifica o nome da tabela base na qual as atualizações, inserções e exclusões são permitidas.<br /><br /> **Esquema exclusivo** Especifica o esquema ou o nome do proprietário da tabela.<br /><br /> **Catálogo exclusivo** Especifica o catálogo ou o nome do banco de dados que contém a tabela.|  
|[Ressincronização de atualização](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|Especifica se o **UpdateBatch** método é seguido por um implícita **Resync** operação de método e nesse caso, o escopo dessa operação.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice b: erros de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces e ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)

