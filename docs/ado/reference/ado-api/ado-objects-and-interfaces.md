---
title: ADO objetos e Interfaces | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad14c7327d3dc7186ff86c3ca0ba84d206143973
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="ado-objects-and-interfaces"></a>Interfaces e ADO
As relações entre esses objetos são representadas no [modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md).  
  
 Cada objeto pode ser contido em sua coleção correspondente. Por exemplo, um [erro](../../../ado/reference/ado-api/error-object.md) objeto pode estar contido em um [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção. Para obter mais informações, consulte [ADO coleções](../../../ado/reference/ado-api/ado-collections.md) ou um tópico de coleção específica.  
  
|||  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|Usado para recuperar o comando OLEDB subjacente de um objeto ADOCommand.|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|Constrói um ADO **registro** objeto a partir de um banco de dados OLE **linha** objeto em um aplicativo C/C++.|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|Constrói um ADO **registros** objeto a partir de um banco de dados OLE **linhas** objeto em um aplicativo C/C++.|  
|[ADOStreamConstruction Interface](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|Constrói um ADO **fluxo** objeto a partir de um banco de dados OLE **IStream** objeto em um aplicativo C/C++.|  
|[Comando](../../../ado/reference/ado-api/command-object-ado.md)|Define um comando específico que você pretende executar em relação a uma fonte de dados.<br /><br /> O **comando** o objeto não é seguro para script.|  
|[Conexão](../../../ado/reference/ado-api/connection-object-ado.md)|Representa uma conexão aberta com uma fonte de dados.<br /><br /> O **Conexão** objeto é seguro para script.|  
|[Interface IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|Obtém o objeto de fonte de dados OLEDB subjacente para o provedor de forma.|  
|[Erro](../../../ado/reference/ado-api/error-object.md)|Contém detalhes sobre erros de acesso de dados que pertencem a uma única operação que envolve o provedor.<br /><br /> O **erro** o objeto não é seguro para script.|  
|[Campo](../../../ado/reference/ado-api/field-object.md)|Representa uma coluna de dados com um tipo de dados comum.|  
|[Parâmetro](../../../ado/reference/ado-api/parameter-object.md)|Representa um parâmetro ou um argumento associado com um **comando** objeto com base em um procedimento armazenado ou uma consulta parametrizada.<br /><br /> O **parâmetro** o objeto não é seguro para script.|  
|[Propriedade](../../../ado/reference/ado-api/property-object-ado.md)|Representa uma característica dinâmica de um objeto ADO que é definido pelo provedor.|  
|[Registro](../../../ado/reference/ado-api/record-object-ado.md)|Representa uma linha de um **registros**, ou um diretório ou arquivo em um sistema de arquivos. O **registro** objeto é seguro para script.|  
|[Conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)|Representa o conjunto de registros de uma tabela base ou os resultados de um comando executado. A qualquer momento, o **registros** objeto se refere a um único registro dentro do conjunto de como o registro atual.<br /><br /> O **registros** objeto é seguro para script.|  
|[Fluxo](../../../ado/reference/ado-api/stream-object-ado.md)|Representa um fluxo binário de dados.<br /><br /> O **fluxo** objeto é seguro para script.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice b: erros de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
