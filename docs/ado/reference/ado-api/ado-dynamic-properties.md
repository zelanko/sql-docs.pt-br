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
manager: jroth
ms.openlocfilehash: 2ad6c2804b70011380a12b5b9e0cd1f52fd56398
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696871"
---
# <a name="ado-dynamic-properties"></a>Propriedades dinâmicas do ADO
Propriedades dinâmicas podem ser adicionadas para o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleções da [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [comando](../../../ado/reference/ado-api/command-object-ado.md), ou [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos. O código-fonte para essas propriedades é qualquer um provedor de dados, como o [OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), ou um provedor de serviços, como o [Microsoft Cursor Service para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md). Consulte a documentação do provedor de serviços para obter mais informações sobre uma propriedade dinâmica específica ou provedor de dados apropriado.  
  
 O [índice de propriedade dinâmica do ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) fornece uma referência cruzada entre os nomes de ADO e OLE DB para cada propriedade dinâmico do provedor OLE DB padrão.  
  
 As seguintes propriedades dinâmicas são especialmente interessantes e também estão documentadas nas fontes mencionadas anteriormente. Uma funcionalidade especial com o ADO está documentada nos tópicos da Ajuda ADO na lista a seguir.  
  
|||  
|-|-|  
|[Otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Especifica se um índice deve ser criado por esse campo.|  
|[Solicitar](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|Especifica se o provedor OLE DB deve solicitar ao usuário para informações de inicialização.|  
|[Alterar a forma de nome](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Especifica um nome para o **Recordset** objeto.|  
|[Comando de ressincronização](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Especifica um comando fornecido pelo usuário de cadeia de caracteres que o **ressincronizar** problemas para atualizar os dados na tabela chamada no método da **tabela exclusiva** propriedade dinâmica.|  
|[Tabela exclusiva, esquema exclusivo, catálogo exclusivo](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**Tabela exclusiva** Especifica o nome da tabela base na qual as atualizações, inserções e exclusões são permitidas.<br /><br /> **Esquema exclusivo** Especifica o esquema ou o nome do proprietário da tabela.<br /><br /> **Catálogo exclusivo** Especifica o catálogo ou o nome do banco de dados que contém a tabela.|  
|[Ressincronização de atualização](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|Especifica se o **UpdateBatch** método é seguido por implícito **ressincronizar** operação de método e nesse caso, o escopo da operação.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice b: Erros ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces e os objetos do ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
