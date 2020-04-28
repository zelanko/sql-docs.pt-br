---
title: Objetos e interfaces do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5ecc6de67defb2366bf208c38bd2de5bff643e4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920905"
---
# <a name="ado-objects-and-interfaces"></a>Objetos e interfaces do ADO
As relações entre esses objetos são representadas no [modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md).  
  
 Cada objeto pode estar contido em sua coleção correspondente. Por exemplo, um objeto de [erro](../../../ado/reference/ado-api/error-object.md) pode estar contido em uma coleção de [erros](../../../ado/reference/ado-api/errors-collection-ado.md) . Para obter mais informações, consulte [coleções de ADO](../../../ado/reference/ado-api/ado-collections.md) ou um tópico de coleção específico.  
  
|||  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|Usado para recuperar o comando OLEDB subjacente de um objeto ADOCommand.|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|Constrói um objeto de **registro** ado de um objeto de **linha** OLE DB em um aplicativo C/C++.|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|Constrói um objeto **RECORDSET** ado a partir de um objeto de **conjunto de linhas** OLE DB em um aplicativo C/C++.|  
|[ADOStreamConstruction Interface](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|Constrói um objeto de **fluxo** ado de um objeto OLE DB **IStream** em um aplicativo C/C++.|  
|[Comando](../../../ado/reference/ado-api/command-object-ado.md)|Define um comando específico que você pretende executar em uma fonte de dados.<br /><br /> O objeto de **comando** não é seguro para scripts.|  
|[Conexão](../../../ado/reference/ado-api/connection-object-ado.md)|Representa uma conexão aberta com uma fonte de dados.<br /><br /> O objeto de **conexão** é seguro para scripts.|  
|[Interface IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|Obtém o objeto de fonte de dados OLEDB subjacente para o provedor de forma.|  
|[Erro](../../../ado/reference/ado-api/error-object.md)|Contém detalhes sobre erros de acesso a dados que pertencem a uma única operação envolvendo o provedor.<br /><br /> O objeto de **erro** não é seguro para scripts.|  
|[Campo](../../../ado/reference/ado-api/field-object.md)|Representa uma coluna de dados com um tipo de dados comum.|  
|[Parâmetro](../../../ado/reference/ado-api/parameter-object.md)|Representa um parâmetro ou argumento associado a um objeto de **comando** com base em uma consulta parametrizada ou em um procedimento armazenado.<br /><br /> O objeto de **parâmetro** não é seguro para scripts.|  
|[Propriedade](../../../ado/reference/ado-api/property-object-ado.md)|Representa uma característica dinâmica de um objeto ADO que é definido pelo provedor.|  
|[Gravável](../../../ado/reference/ado-api/record-object-ado.md)|Representa uma linha de um **conjunto de registros**ou um diretório ou arquivo em um sistema de arquivos. O objeto de **registro** é seguro para scripts.|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|Representa o conjunto de registros de uma tabela base ou os resultados de um comando executado. A qualquer momento, o objeto **Recordset** refere-se apenas a um único registro dentro do conjunto como o registro atual.<br /><br /> O objeto **Recordset** é seguro para scripts.|  
|[Fluxo](../../../ado/reference/ado-api/stream-object-ado.md)|Representa um fluxo de dados binário.<br /><br /> O objeto de **fluxo** é seguro para scripts.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice B: erros do ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos do ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
