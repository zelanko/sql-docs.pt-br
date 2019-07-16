---
title: Objetos do ADO e Interfaces | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920905"
---
# <a name="ado-objects-and-interfaces"></a>Objetos e interfaces do ADO
As relações entre esses objetos são representadas na [modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md).  
  
 Cada objeto pode estar contido em sua coleção correspondente. Por exemplo, um [erro](../../../ado/reference/ado-api/error-object.md) objeto pode estar contido em um [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção. Para obter mais informações, consulte [coleções ADO](../../../ado/reference/ado-api/ado-collections.md) ou um tópico de coleção específica.  
  
|||  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|Usado para recuperar o comando OLE DB subjacente de um objeto de ADOCommand.|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|Constrói um ADO **registro** objeto a partir de um banco de dados OLE **linha** objeto em um aplicativo C/C++.|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|Constrói um ADO **conjunto de registros** objeto a partir de um banco de dados OLE **conjunto de linhas** objeto em um aplicativo C/C++.|  
|[ADOStreamConstruction Interface](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|Constrói um ADO **Stream** objeto a partir de um banco de dados OLE **IStream** objeto em um aplicativo C/C++.|  
|[Comando](../../../ado/reference/ado-api/command-object-ado.md)|Define um comando específico que você pretende executar em relação a uma fonte de dados.<br /><br /> O **comando** objeto não é seguro para script.|  
|[Conexão](../../../ado/reference/ado-api/connection-object-ado.md)|Representa uma conexão aberta com uma fonte de dados.<br /><br /> O **Conexão** objeto é seguro para script.|  
|[Interface IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|Obtém o objeto de fonte de dados OLEDB subjacente para o provedor SHAPE.|  
|[Erro](../../../ado/reference/ado-api/error-object.md)|Contém detalhes sobre erros de acesso de dados que pertencem a uma única operação que envolva o provedor.<br /><br /> O **erro** objeto não é seguro para script.|  
|[Campo](../../../ado/reference/ado-api/field-object.md)|Representa uma coluna de dados com um tipo de dados comum.|  
|[Parâmetro](../../../ado/reference/ado-api/parameter-object.md)|Representa um parâmetro ou um argumento associado a um **comando** objeto com base em uma consulta parametrizada ou procedimento armazenado.<br /><br /> O **parâmetro** objeto não é seguro para script.|  
|[Property](../../../ado/reference/ado-api/property-object-ado.md)|Representa uma característica dinâmica de um objeto ADO que é definido pelo provedor.|  
|[Record](../../../ado/reference/ado-api/record-object-ado.md)|Representa uma linha de uma **Recordset**, ou um arquivo ou diretório em um sistema de arquivos. O **registro** objeto é seguro para script.|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|Representa o conjunto de registros de uma tabela base ou os resultados de um comando executado. A qualquer momento, o **Recordset** objeto se refere a um único registro dentro do conjunto de como o registro atual.<br /><br /> O **Recordset** objeto é seguro para script.|  
|[fluxo](../../../ado/reference/ado-api/stream-object-ado.md)|Representa um fluxo binário de dados.<br /><br /> O **Stream** objeto é seguro para script.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice b: Erros ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
