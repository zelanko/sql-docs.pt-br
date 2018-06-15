---
title: Coleções e objetos ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d8b1967071b5dc420577ecbee3f1b124d917057
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271375"
---
# <a name="ado-objects-and-collections"></a>Coleções e objetos de ADO
ADO consiste em nove objetos a seguir e quatro coleções.  
  
|Objeto ou coleção|Description|  
|--------------------------|-----------------|  
|**Conexão** objeto|Representa uma sessão exclusiva com uma fonte de dados. No caso de um sistema de banco de dados cliente/servidor, é equivalente a uma conexão de rede reais para o servidor. Dependendo da funcionalidade com suporte do provedor, algumas coleções, métodos ou propriedades de um **Conexão** objeto pode não estar disponível.|  
|Objeto**Comando** |Usado para definir um comando específico, como uma consulta SQL, devem ser executados em uma fonte de dados.|  
|**Conjunto de registros** objeto|Representa todo o conjunto de registros de uma tabela base ou os resultados de um comando executado. Todos os **registros** objetos consistem em registros (linhas) e campos (colunas).|  
|**Registro** objeto|Representa uma única linha de dados, de um **registros** ou do provedor. Esse registro pode representar um registro de banco de dados ou algum outro tipo de objeto como um arquivo ou diretório, dependendo de seu provedor.|  
|**Fluxo** objeto|Representa um fluxo de dados binários ou de texto. Por exemplo, um documento XML pode ser carregado em um fluxo de entrada ou retornados de certos provedores como os resultados de uma consulta de comando. Um **fluxo** objeto pode ser usado para manipular campos ou registros que contêm esses fluxos de dados.|  
|**Parâmetro** objeto|Representa um parâmetro ou um argumento associado com um **comando** objeto, com base em um procedimento armazenado ou uma consulta parametrizada.|  
|**Campo** objeto|Representa uma coluna de dados com um tipo de dados comum. Cada **campo** objeto corresponde a uma coluna de **registros**.|  
|**Propriedade** objeto|Representa uma característica de um objeto ADO que é definido pelo provedor. Objetos de ADO têm dois tipos de propriedades: interna e dinâmicos. Propriedades internas são as propriedades implementadas no ADO e imediatamente disponíveis para qualquer novo objeto. O **propriedade** objeto é um recipiente de propriedades dinâmicas, definido pelo provedor subjacente.|  
|Objeto**Erro** |Contém detalhes sobre erros de acesso de dados que pertencem a uma única operação que envolve o provedor.|  
|**Campos** coleção|Contém todos os **campo** objetos de um **Recordset** ou **registro** objeto.|  
|**Propriedades** coleção|Contém todos os **propriedade** objetos para uma instância específica de um objeto.|  
|**Parâmetros** coleção|Contém todos os **parâmetro** objetos de um **comando** objeto.|  
|**Erros** coleção|Contém todos os **erro** objetos criados em resposta a uma única falha de provedor.|  
  
## <a name="see-also"></a>Consulte também  
 [Modelo do objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)
