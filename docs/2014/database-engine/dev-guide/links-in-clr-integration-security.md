---
title: Links em segurança da integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- table-access links [CLR integration]
- security [CLR integration]
- invocation links [CLR integration]
- gated links [CLR integration]
ms.assetid: 168efd01-d12e-4bdf-a1b3-0b5c76474eaf
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37aa64129658128bd7297f147f317166917e05a6
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156772"
---
# <a name="links-in-clr-integration-security"></a>Links em segurança da integração CLR
  Esta seção descreve como partes do código do usuário podem chamar uma à outra no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tanto em [!INCLUDE[tsql](../../includes/tsql-md.md)] quanto em uma das linguagens gerenciadas. Essas relações entre objetos são conhecidas como links.  
  
## <a name="invocation-links"></a>Links de invocação  
 Os links de invocação correspondem a uma invocação de código, em uma chamada para um objeto feita pelo usuário (como, por exemplo, uma chamada de lote [!INCLUDE[tsql](../../includes/tsql-md.md)] para um procedimento armazenado), ou um procedimento armazenado ou função CLR (Common Language Runtime). Os links de invocação fazem com que uma permissão `EXECUTE` no destinatário seja verificada.  
  
## <a name="table-access-links"></a>Links de acesso à tabela  
 Os links de acesso à tabela correspondem à recuperação ou à modificação de valores em uma tabela, exibição ou uma função de valor de tabela. Eles são semelhantes aos links de invocação, exceto por apresentarem um controle de acesso mais refinado em termos de permissões SELECT, INSERT, UPDATE e DELETE.  
  
## <a name="gated-links"></a>Links de entrada  
 Os links de entrada significam que, durante a execução, as permissões, uma vez estabelecidas, não são verificadas em todas as relações de objeto. Quando há um link de entrada entre dois objetos (por exemplo, objetos **x** e **y**), as permissões no objeto **y** e nos demais objetos acessados no objeto **y** só são verificadas no momento da criação do objeto **x**. No momento da criação do objeto **x**, `REFERENCE` permissão é verificada no **y** em comparação com o proprietário da **x**. Em tempo de execução, (por exemplo, quando alguém chama o objeto **x**), nenhuma permissão é verificada em relação a **y** ou outros objetos referenciados estatisticamente. Em tempo de execução, uma permissão apropriada será verificada em relação ao próprio objeto **x** .  
  
 Os links de entrada são sempre usados em conjunto com uma dependência de metadados entre dois objetos. Essa dependência de metadados é uma relação estabelecida nos catálogos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que impede um objeto de ser descartado enquanto outro objeto depender dele.  
  
 Os links de entrada são úteis quando não é apropriado ou gerenciável conceder permissões a muitos objetos dependentes. Os links de entrada são introduzidos entre objetos que definem pontos de entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] em assemblies do CLR (por exemplo, procedimentos CLR, gatilhos, funções, tipos e agregações) e assemblies nos quais são definidos. A segurança de entrada nesses objetos implica que, para invocar um ponto de entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] definido em um assembly do CLR, o chamador só precisa de uma permissão apropriada nesse ponto de entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] . Não é obrigatório que o chamador tenha permissões nesse assembly ou em qualquer outro referenciado estaticamente. As permissões no assembly são verificadas durante a criação do ponto de entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
## <a name="sql-server-authorization-based-security"></a>Segurança baseada na autorização do SQL Server  
 Estas são as regras básicas por trás das verificações de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para invocações de e entre objetos de banco de dados baseados no CLR; as três primeiras regras definem quais permissões são verificadas e em quais objetos; a quarta, o contexto de execução em que a permissão é verificada.  
  
1.  Todas as invocações exigem permissões `EXECUTE`, a menos que essas invocações ocorram no mesmo objeto, ou seja, as chamadas dentro do mesmo assembly não exigem verificações de permissão. A permissão é verificada em tempo de execução.  
  
2.  Os links de entrada exigem a permissão `REFERENCE` no destinatário durante a criação do objeto de chamada. A permissão é verificada para o proprietário do objeto de chamada quando o objeto é criado.  
  
3.  Os links de acesso à tabela exigem as permissões `SELECT`, `INSERT`, `UPDATE` ou `DELETE` correspondentes na tabela ou exibição acessada.  
  
4.  A permissão é verificada no contexto de execução atual. Procedimentos e funções podem ser criados com um contexto de execução diferente do chamador. Os assemblies sempre são criados com o contexto de execução do procedimento, da função, do disparador definido.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança da integração CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
