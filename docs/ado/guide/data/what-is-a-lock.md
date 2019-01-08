---
title: O que é um bloqueio? | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 744ae9a9541b5c73d579e097f375b4141e771fce
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501760"
---
# <a name="what-is-a-lock"></a>O que é um bloqueio?
O bloqueio é o processo pelo qual um DBMS restringe o acesso a uma linha em um ambiente multiusuário. Quando uma linha ou coluna está bloqueada exclusivamente, outros usuários não têm permissão para acessar os dados bloqueados até que o bloqueio seja liberado. Isso garante que dois usuários não é possível atualizar simultaneamente a mesma coluna em uma linha.  
  
 Bloqueios podem ser muito caros de uma perspectiva de recurso e devem ser usados somente quando necessário para preservar a integridade dos dados. Em um banco de dados em que centenas ou milhares de usuários podem estar tentando acessar um registro a cada segundo - como um banco de dados conectado à Internet, o bloqueio desnecessário pode rapidamente resultar em desempenho mais lento em seu aplicativo.  
  
 Você pode controlar como a fonte de dados e a biblioteca de cursor de ADO gerenciar a simultaneidade, escolhendo a opção apropriada de bloqueio.  
  
 Defina as **LockType** propriedade antes de abrir um **Recordset** para especificar que tipo de bloqueio do provedor deve usar ao abri-lo. Ler a propriedade para retornar o tipo de bloqueio em uso em um aberto **Recordset** objeto.  
  
 Provedores podem não dar suporte a todos os tipos de bloqueio. Se um provedor não oferecer suporte a solicitada **LockType** configuração, ele substituirá outro tipo de bloqueio. Para determinar a funcionalidade de bloqueio real em um **conjunto de registros** do objeto, use o [dá suporte à](../../../ado/reference/ado-api/supports-method.md) método com **adUpdate** e **adUpdateBatch**.  
  
 O **adLockPessimistic** configuração não tem suporte se o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) estiver definida como **adUseClient.** Se um valor sem suporte for definido, nenhum erro ocorrerá; suporte a mais próxima **LockType** será usado.  
  
 O **LockType** propriedade é leitura/gravação quando o **Recordset** é fechada e somente leitura quando ele é aberto.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tipos de bloqueios](../../../ado/guide/data/types-of-locks.md)
