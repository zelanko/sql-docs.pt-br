---
title: Visão geral do data Shaping | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], overview
ms.assetid: 4cb5fd29-4e56-46ac-ae48-a6771c321c0c
author: rothja
ms.author: jroth
ms.openlocfilehash: a6258c44d267462cea097c5553c9814b10d3787f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750285"
---
# <a name="data-shaping-overview"></a>Visão geral de data shaping
A *modelagem de dados* significa criar relações hierárquicas entre duas ou mais entidades lógicas em uma consulta. A hierarquia pode ser vista em relações pai-filho entre um registro de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)e um ou mais registros (também conhecido como um capítulo) de outro **conjunto**de registros. Em uma relação pai-filho, o **conjunto de registros** pai contém o **conjunto de registros**filho. Um exemplo dessa relação hierárquica é os clientes e pedidos. Para cada cliente em um banco de dados, pode haver zero ou mais pedidos. A relação hierárquica pode ser recursiva, o que significa que os registros de neto podem ser aninhados em um registro filho. Em princípio, um registro hierárquico pode ser aninhado em qualquer profundidade. Na prática, o ADO limita a recursão a um máximo de 512 **conjuntos de registros**s.  
  
 Em geral, as colunas de um **conjunto de registros** moldado podem conter dados de um provedor de dados, como o Microsoft® SQL Server, referências a outro **conjunto de registros**, valores derivados de um cálculo em uma única linha de um conjunto de **registros**ou valores derivados de uma operação em uma coluna de um **conjunto de registros**inteiro. Uma coluna também pode ser recentemente crieida e vazia.  
  
 Quando você recupera o valor de uma coluna que contém uma referência a outro **conjunto de registros**, o ADO retorna automaticamente o **conjunto de registros** real representado pela referência. A referência a um **conjunto de registros** é, na verdade, uma referência a um subconjunto do filho, chamado de *capítulo*. Um único pai pode fazer referência a mais de um **conjunto de registros**filho.  
  
 O suporte ADO para Shaping de dados permite consultar uma fonte de dados e retornar um **conjunto de registros** no qual um registro (pai) representa um **conjunto de registros**(filho). No cenário de ordem de cliente, você pode usar o Shaping de dados para recuperar informações de clientes, bem como os pedidos feitos por cada cliente em uma única consulta. O conjunto de **registros** resultante também é conhecido como **conjunto de registros**moldado.  
  
 Além disso, o data Shaping no ADO permite que você crie novos objetos de **conjunto de registros** sem uma fonte de dados subjacente usando a **nova** palavra-chave para descrever os campos dos **conjuntos de registros**pai e filho. O novo objeto **Recordset** pode ser preenchido com dados e armazenados de forma persistente. Os desenvolvedores também podem executar vários cálculos ou agregações (por exemplo, **sum**, **AVG**e **Max**) em campos filho. O data Shaping também pode criar um **conjunto de registros** pai de um **conjunto** de registros filho agrupando registros no filho e colocando uma linha no pai para cada grupo no filho.  
  
 O SQL regular permite que você recupere dados usando a sintaxe de **junção** , mas isso pode ser ineficiente e complicado porque dados pai redundantes são repetidos em cada registro retornado para uma determinada relação pai-filho. A modelagem de dados pode relacionar um único registro pai no **conjunto de registros** pai a vários registros filho no conjunto de **registros**filho, evitando a redundância de uma **junção**. A maioria das pessoas encontra o modelo de programação pai-filho de vários **conjuntos de registros** mais natural e fácil de trabalhar com o único modelo de junção do **conjunto de registros** .
