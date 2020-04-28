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
ms.openlocfilehash: 89093367532177ec87fb3a5fd86e38e98345962c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926047"
---
# <a name="ado-objects-and-collections"></a>Objetos e coleções ADO
O ADO consiste nos nove objetos e quatro coleções a seguir.  
  
|Objeto ou coleção|Descrição|  
|--------------------------|-----------------|  
|Objeto de **conexão**|Representa uma sessão exclusiva com uma fonte de dados. No caso de um sistema de banco de dados cliente/servidor, pode ser equivalente a uma conexão de rede real com o servidor. Dependendo da funcionalidade suportada pelo provedor, algumas coleções, métodos ou propriedades de um objeto de **conexão** podem não estar disponíveis.|  
|Objeto**Comando**|Usado para definir um comando específico, como uma consulta SQL, destinado para ser executado em uma fonte de dados.|  
|Objeto **Recordset**|Representa o conjunto inteiro de registros de uma tabela base ou os resultados de um comando executado. Todos os objetos **Recordset** consistem em registros (linhas) e campos (colunas).|  
|Objeto de **registro**|Representa uma única linha de dados, seja de um **conjunto de registros** ou do provedor. Esse registro pode representar um registro de banco de dados ou algum outro tipo de objeto, como um arquivo ou diretório, dependendo do seu provedor.|  
|Objeto **Stream**|Representa um fluxo de dados binários ou de texto. Por exemplo, um documento XML pode ser carregado em um fluxo para entrada de comando ou retornado de determinados provedores como os resultados de uma consulta. Um objeto de **fluxo** pode ser usado para manipular campos ou registros que contêm esses fluxos de dados.|  
|Objeto de **parâmetro**|Representa um parâmetro ou argumento associado a um objeto **Command** , com base em uma consulta parametrizada ou em um procedimento armazenado.|  
|Objeto **Field**|Representa uma coluna de dados com um tipo de dados comum. Cada objeto de **campo** corresponde a uma coluna no **conjunto de registros**.|  
|Objeto de **Propriedade**|Representa uma característica de um objeto ADO que é definido pelo provedor. Os objetos ADO têm dois tipos de propriedades: interno e dinâmico. As propriedades internas são aquelas implementadas no ADO e imediatamente disponibilizadas para qualquer novo objeto. O objeto **Property** é um contêiner para propriedades dinâmicas, definido pelo provedor subjacente.|  
|Objeto de **erro**|Contém detalhes sobre erros de acesso a dados que pertencem a uma única operação envolvendo o provedor.|  
|Coleção **Fields**|Contém todos os objetos de **campo** de um **conjunto de registros** ou objeto de **registro** .|  
|Coleção de **Propriedades**|Contém todos os objetos de **Propriedade** para uma instância específica de um objeto.|  
|Coleção de **parâmetros**|Contém todos os objetos de **parâmetro** de um objeto de **comando** .|  
|Coleção de **erros**|Contém todos os objetos de **erro** criados em resposta a uma falha relacionada a um único provedor.|  
  
## <a name="see-also"></a>Consulte Também  
 [Modelo do objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)
