---
title: O que é um bloqueio? | Microsoft Docs
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
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 396faecd122eef7ad6e40f790252a0902a508ba8
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273285"
---
# <a name="what-is-a-lock"></a>O que é um bloqueio?
O bloqueio é o processo pelo qual um DBMS restringe o acesso a uma linha em um ambiente multiusuário. Quando uma linha ou coluna está bloqueada exclusivamente, outros usuários não têm permissão para acessar os dados bloqueados até que o bloqueio seja liberado. Isso garante que os dois usuários não é possível atualizar simultaneamente a mesma coluna em uma linha.  
  
 Bloqueios podem ser muito caros de uma perspectiva de recurso e devem ser usados somente quando necessário para preservar a integridade dos dados. Em um banco de dados onde centenas ou milhares de usuários podem estar tentando acessar um registro a cada segundo — como um banco de dados conectado à Internet — bloqueio desnecessário rapidamente pode resultar em desempenho mais lento em seu aplicativo.  
  
 Você pode controlar como a fonte de dados e a biblioteca de cursor de ADO gerenciar a simultaneidade, selecionando a opção de bloqueio apropriada.  
  
 Definir o **LockType** propriedade antes de abrir um **registros** para especificar o tipo de bloqueio do provedor deve usar ao abri-lo. Ler a propriedade para retornar o tipo de bloqueio em uso em um aberto **registros** objeto.  
  
 Provedores podem não suportar todos os tipos de bloqueio. Se um provedor não oferecer suporte a solicitação **LockType** configuração, ele substituirá outro tipo de bloqueio. Para determinar a funcionalidade de bloqueio real em um **registros** de objeto, use o [dá suporte a](../../../ado/reference/ado-api/supports-method.md) método com **adUpdate** e **adUpdateBatch**.  
  
 O **adLockPessimistic** configuração não é suportada se o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) está definida como **adUseClient.** Se for definido um valor sem suporte, nenhum erro ocorrerá; suporte a mais próximo **LockType** será usado.  
  
 O **LockType** propriedade é leitura/gravação quando o **registros** está fechado e somente leitura quando ela é aberta.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tipos de bloqueios](../../../ado/guide/data/types-of-locks.md)
