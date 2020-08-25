---
description: Objetos e interfaces do ADO
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d4cce8ba7913b80ea971c563b1235a15b84d372
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776615"
---
# <a name="ado-objects-and-interfaces"></a>Objetos e interfaces do ADO
As relações entre esses objetos são representadas no [modelo de objeto ADO](./ado-object-model.md).  
  
 Cada objeto pode estar contido em sua coleção correspondente. Por exemplo, um objeto de [erro](./error-object.md) pode estar contido em uma coleção de [erros](./errors-collection-ado.md) . Para obter mais informações, consulte [coleções de ADO](./ado-collections.md) ou um tópico de coleção específico.  
  
|Objeto ou interface|Descrição|  
|-|-|  
|[IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))|Usado para recuperar o comando OLEDB subjacente de um objeto ADOCommand.|  
|[ADORecordConstruction](./adorecordconstruction-interface.md)|Constrói um objeto de **registro** ado de um objeto de **linha** OLE DB em um aplicativo C/C++.|  
|[ADORecordsetConstruction](./adorecordsetconstruction-interface.md)|Constrói um objeto **RECORDSET** ado a partir de um objeto de **conjunto de linhas** OLE DB em um aplicativo C/C++.|  
|[ADOStreamConstruction Interface](./adostreamconstruction-interface.md)|Constrói um objeto de **fluxo** ado de um objeto OLE DB **IStream** em um aplicativo C/C++.|  
|[Comando](./command-object-ado.md)|Define um comando específico que você pretende executar em uma fonte de dados.<br /><br /> O objeto de **comando** não é seguro para scripts.|  
|[Conexão](./connection-object-ado.md)|Representa uma conexão aberta com uma fonte de dados.<br /><br /> O objeto de **conexão** é seguro para scripts.|  
|[Interface IDSOShapeExtensions](./idsoshapeextensions-interface.md)|Obtém o objeto de fonte de dados OLEDB subjacente para o provedor de forma.|  
|[Erro](./error-object.md)|Contém detalhes sobre erros de acesso a dados que pertencem a uma única operação envolvendo o provedor.<br /><br /> O objeto de **erro** não é seguro para scripts.|  
|[Campo](./field-object.md)|Representa uma coluna de dados com um tipo de dados comum.|  
|[Parâmetro](./parameter-object.md)|Representa um parâmetro ou argumento associado a um objeto de **comando** com base em uma consulta parametrizada ou em um procedimento armazenado.<br /><br /> O objeto de **parâmetro** não é seguro para scripts.|  
|[Propriedade](./property-object-ado.md)|Representa uma característica dinâmica de um objeto ADO que é definido pelo provedor.|  
|[Registro](./record-object-ado.md)|Representa uma linha de um **conjunto de registros**ou um diretório ou arquivo em um sistema de arquivos. O objeto de **registro** é seguro para scripts.|  
|[Recordset](./recordset-object-ado.md)|Representa o conjunto de registros de uma tabela base ou os resultados de um comando executado. A qualquer momento, o objeto **Recordset** refere-se apenas a um único registro dentro do conjunto como o registro atual.<br /><br /> O objeto **Recordset** é seguro para scripts.|  
|[Fluxo](./stream-object-ado.md)|Representa um fluxo de dados binário.<br /><br /> O objeto de **fluxo** é seguro para scripts.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](./ado-api-reference.md)   
 [Coleções ADO](./ado-collections.md)   
 [Propriedades dinâmicas do ADO](./ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](./ado-enumerated-constants.md)   
 [Apêndice B: erros do ADO](../../guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](./ado-events.md)   
 [Métodos do ADO](./ado-methods.md)   
 [Modelo de objeto ADO](./ado-object-model.md)   
 [Propriedades ADO](./ado-properties.md)