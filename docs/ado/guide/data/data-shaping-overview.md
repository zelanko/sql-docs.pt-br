---
title: "Visão geral de modelagem de dados | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], overview
ms.assetid: 4cb5fd29-4e56-46ac-ae48-a6771c321c0c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f885a8585d3665efcc39bfe979b501d779c35c00
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="data-shaping-overview"></a>Visão geral de modelagem de dados
*Modelagem de dados* significa criar relações hierárquicas entre dois ou mais entidades lógicas em uma consulta. A hierarquia pode ser vista em relações pai-filho entre um registro de um [registros](../../../ado/reference/ado-api/recordset-object-ado.md)e um ou mais registros (também conhecido como um capítulo) de outro **registros**. Em uma relação pai-filho, o pai **registros** contém o filho **registros**. Um exemplo de tal relação hierárquica é customers e orders. Para cada cliente em um banco de dados, pode ser zero ou mais pedidos. A relação hierárquica pode ser recursivos, que significa que os registros de neto podem ser aninhados em um registro filho. Em princípio, um registro hierárquico pode ser aninhado para qualquer profundidade. Na prática, o ADO limita a recursão para um máximo de 512 **registros**s.  
  
 Em gerais, colunas de uma forma **registros** pode conter dados de um provedor de dados como o Microsoft® SQL Server, referências a outro **registros**, valores derivados de um cálculo em uma única linha de um ** Conjunto de registros**, ou valores derivados de uma operação em uma coluna de toda uma **registros**. Uma coluna pode também ser recentemente fabricadas vazio.  
  
 Quando você recuperar o valor de uma coluna que contém uma referência a outro **registros**, ADO retorna automaticamente real **registros** representado pela referência de. A referência a um **registros** é, na verdade, uma referência a um subconjunto do filho, chamado um *capítulo*. Um único pai pode fazer referência a mais de um filho **registros**.  
  
 Suporte de ADO para modelagem de dados permite que você consultar uma fonte de dados e retornar um **registros** em que um registro (pai) representa (filho) **registros**. No cenário de pedidos do cliente, você pode usar dados de formatação para recuperar informações de clientes, bem como os pedidos feitos por cada cliente em uma única consulta. O RSoP **registros** é também conhecido como em forma de **registros**.  
  
 Além disso, dados de formatação no ADO permitirem criar novos **registros** objetos sem uma fonte de dados subjacente usando a **novo** palavra-chave para descrever os campos de pai e filho ** Conjuntos de registros**. O novo **registros** objeto pode ser preenchido com dados e armazenado de forma persistente. Os desenvolvedores também podem executar vários cálculos ou agregações (por exemplo, **soma**, **AVG**, e **MAX**) em campos de filho. Modelagem de dados também pode criar um pai **registros** de filho **registros** agrupar registros no filho e colocando uma linha no pai para cada grupo filho.  
  
 Regular SQL permite que você recupere dados usando **INGRESSAR** sintaxe, mas isso pode ser ineficiente e complicada porque dados redundantes pai são repetidos em cada registro retornado para uma relação pai-filho especificado. Modelagem de dados pode estar relacionada a um registro único pai no pai **registros** para vários registros filho no filho **registros**, evitando a redundância de um **INGRESSAR**. A maioria das pessoas localizar o pai-filho vários **registros** modelo de programação mais natural e mais fácil trabalhar com que a única **Recordset INGRESSAR** modelo.
