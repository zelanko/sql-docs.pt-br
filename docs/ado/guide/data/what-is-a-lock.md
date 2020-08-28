---
description: O que é um bloqueio?
title: O que é um bloqueio? | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
author: rothja
ms.author: jroth
ms.openlocfilehash: d64d6b417f6430cb834c48b8caf93e041a2084e8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978867"
---
# <a name="what-is-a-lock"></a>O que é um bloqueio?
O bloqueio é o processo pelo qual um DBMS restringe o acesso a uma linha em um ambiente de vários usuários. Quando uma linha ou coluna é bloqueada exclusivamente, outros usuários não têm permissão para acessar os dados bloqueados até que o bloqueio seja liberado. Isso garante que dois usuários não possam atualizar simultaneamente a mesma coluna em uma linha.  
  
 Os bloqueios podem ser muito caros de uma perspectiva de recurso e devem ser usados somente quando necessário para preservar a integridade dos dados. Em um banco de dados em que centenas ou milhares de usuários podiam estar tentando acessar um registro a cada segundo, como um banco de dados conectado ao bloqueio desnecessário pela Internet, pode resultar rapidamente em um desempenho mais lento em seu aplicativo.  
  
 Você pode controlar como a fonte de dados e a biblioteca de cursores ADO gerenciam a simultaneidade escolhendo a opção de bloqueio apropriada.  
  
 Defina a propriedade **LockType** antes de abrir um **conjunto de registros** para especificar o tipo de bloqueio que o provedor deve usar ao abri-lo. Leia a propriedade para retornar o tipo de bloqueio em uso em um objeto Open **Recordset** .  
  
 Os provedores podem não dar suporte a todos os tipos de bloqueio. Se um provedor não puder oferecer suporte à configuração **LockType** solicitada, ele substituirá outro tipo de bloqueio. Para determinar a funcionalidade de bloqueio real disponível em um objeto **Recordset** , use o método com [suporte](../../../ado/reference/ado-api/supports-method.md) com **adUpdate** e **adUpdateBatch**.  
  
 A configuração **adLockPessimistic** não terá suporte se a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) estiver definida como **adUseClient.** Se um valor sem suporte for definido, nenhum erro será resultado; o **LockType** com suporte mais próximo será usado em seu lugar.  
  
 A propriedade **LockType** é leitura/gravação quando o **conjunto de registros** é fechado e somente leitura quando ele está aberto.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de bloqueios](../../../ado/guide/data/types-of-locks.md)
