---
title: Coleções e objetos ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5743e04b402302cc53b7694d8160edfb11769e0c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783874"
---
# <a name="ado-objects-and-collections"></a>Objetos e coleções ADO
ADO consiste em nove seguintes objetos e coleções de quatro.  
  
|Objeto ou coleção|Description|  
|--------------------------|-----------------|  
|**Conexão** objeto|Representa uma sessão exclusiva com uma fonte de dados. No caso de um sistema de banco de dados cliente/servidor, é equivalente a uma conexão de rede reais para o servidor. Dependendo da funcionalidade compatível com o provedor, algumas coleções, métodos ou propriedades de um **Conexão** objeto pode não estar disponível.|  
|Objeto**Comando** |Usado para definir um comando específico, como uma consulta SQL, devem ser executados em relação a uma fonte de dados.|  
|**Conjunto de registros** objeto|Representa todo o conjunto de registros de uma tabela base ou os resultados de um comando executado. Todos os **Recordset** objetos consistem em registros (linhas) e campos (colunas).|  
|**Registro** objeto|Representa uma única linha de dados, a partir de um **Recordset** ou do provedor. Esse registro pode representar um registro de banco de dados ou algum outro tipo de objeto como um arquivo ou diretório, dependendo do seu provedor.|  
|**Stream** objeto|Representa um fluxo de dados de texto ou binárias. Por exemplo, um documento XML pode ser carregado em um fluxo para o comando de entrada ou retornados de certos provedores como os resultados de uma consulta. Um **Stream** objeto pode ser usado para manipular registros que contêm esses fluxos de dados ou campos.|  
|**Parâmetro** objeto|Representa um parâmetro ou um argumento associado a um **comando** objeto, com base em uma consulta parametrizada ou procedimento armazenado.|  
|**Campo** objeto|Representa uma coluna de dados com um tipo de dados comum. Cada **campo** objeto corresponde a uma coluna na **conjunto de registros**.|  
|**Propriedade** objeto|Representa uma característica de um objeto ADO que é definido pelo provedor. Objetos do ADO têm dois tipos de propriedades: interna e dinâmicos. Propriedades internas são as propriedades implementadas no ADO e fica imediatamente disponível para qualquer novo objeto. O **propriedade** objeto é um recipiente de propriedades dinâmicas, definido pelo provedor subjacente.|  
|Objeto**Erro** |Contém detalhes sobre erros de acesso de dados que pertencem a uma única operação que envolva o provedor.|  
|**Campos** coleção|Contém todos os **campo** objetos de uma **conjunto de registros** ou **registro** objeto.|  
|**Propriedades** coleção|Contém todos os **propriedade** objetos para uma instância específica de um objeto.|  
|**Parâmetros** coleção|Contém todos os **parâmetro** objetos de uma **comando** objeto.|  
|**Erros** coleção|Contém todos os **erro** objetos criados em resposta a uma única falha de provedor.|  
  
## <a name="see-also"></a>Consulte também  
 [Modelo do objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)
