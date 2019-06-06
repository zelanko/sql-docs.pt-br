---
title: Visão geral de modelagem de dados | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6d693ccbeb06860cd4633a933e80b9ccbe6526a8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702228"
---
# <a name="data-shaping-overview"></a>Visão geral de data shaping
*Formatação de dados* significa criar relações hierárquicas entre dois ou mais entidades lógicas em uma consulta. A hierarquia pode ser vista em relações pai-filho entre um registro de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)e um ou mais registros (também conhecido como um capítulo) de outro **conjunto de registros**. Em uma relação pai-filho, o pai **conjunto de registros** contém o filho **conjunto de registros**. Um exemplo de tal relação hierárquica é customers e orders. Para cada cliente em um banco de dados, pode ser zero ou mais pedidos. A relação hierárquica pode ser recursivo, o que significa que os registros de neto podem ser aninhados em um registro filho. Em princípio, um registro hierárquico pode ser aninhado em qualquer profundidade. Na prática, o ADO limita a recursão para um máximo de 512 **Recordset**s.  
  
 Em gerais, colunas de uma forma **conjunto de registros** pode conter dados de um provedor de dados, como o Microsoft® SQL Server, as referências para outra **conjunto de registros**, valores derivados de um cálculo em uma única linha de um  **Conjunto de registros**, ou valores derivados de uma operação em uma coluna de um todo **conjunto de registros**. Uma coluna também pode ser recentemente fabricadas e vazio.  
  
 Quando você recupera o valor de uma coluna que contém uma referência a outro **conjunto de registros**, ADO retorna automaticamente real **Recordset** representado pela referência de. A referência a um **conjunto de registros** é na verdade, uma referência a um subconjunto do filho, chamado um *capítulo*. Um único pai pode fazer referência a mais de um filho **conjunto de registros**.  
  
 Suporte ADO para data shaping permite consultar uma fonte de dados e retornar um **conjunto de registros** em que um registro (pai) representa (filho) **conjunto de registros**. No cenário de pedido de cliente, você pode usar dados de formatação para recuperar informações dos clientes, bem como os pedidos feitos por cada cliente em uma única consulta. O resultante **conjunto de registros** também conhecido como em forma **conjunto de registros**.  
  
 Além disso, dados de formatação no ADO permitem criar novos **conjunto de registros** objetos sem uma fonte de dados subjacente usando a **NEW** palavra-chave para descrever os campos de pai e filho  **Conjuntos de registros**. O novo **Recordset** objeto pode ser preenchido com dados e persistentemente armazenado. Os desenvolvedores também podem executar vários cálculos ou agregações (por exemplo, **soma**, **AVG**, e **MAX**) nos campos de filho. Formatação de dados também pode criar um pai **conjunto de registros** de um filho **Recordset** agrupar registros do filho e colocando uma linha no pai para cada grupo do filho.  
  
 SQL regular permite que você recupere dados usando **INGRESSAR** sintaxe, mas isso pode ser ineficiente e complicada porque os dados redundantes pai são repetidos em cada registro retornado para uma relação pai-filho especificado. Formatação de dados pode estar relacionada a um registro único pai no pai **conjunto de registros** a vários registros filho na filho **conjunto de registros**, evitando a redundância de um **INGRESSAR**. A maioria das pessoas localizar o pai-filho várias **conjunto de registros** modelo de programação mais natural e fácil de trabalhar com o que a única **conjunto de registros é INGRESSAR** modelo.
