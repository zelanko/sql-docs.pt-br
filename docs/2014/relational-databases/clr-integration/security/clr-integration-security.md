---
title: Segurança da integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- authorization [CLR integration]
- common language runtime [SQL Server], security
- database objects [CLR integration], security
ms.assetid: 05d7a471-c5d5-4730-b903-e4edc8157bb4
caps.latest.revision: 54
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 689d425c2f13a442b1d8bbd5515939135f44fa0c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009574"
---
# <a name="clr-integration-security"></a>Segurança da integração CLR
  O modelo de segurança a [!INCLUDE[ssNoVersion](../../../includes/dnprdnshort-md.md)] common language runtime (CLR) gerencia e protege o acesso entre tipos diferentes de objetos CLR e não CLR em execução dentro de [!INCLUDE[ssNoVersion](../../../includes/tsql-md.md)] instrução ou outro objeto CLR em execução no servidor. As chamadas entre objetos conhecidas como links. Os tipos de verificações de segurança realizados nesses objetos dependem dos tipos de links envolvidos.  
  
 O modelo de segurança de integração do CLR tem as seguintes metas:  
  
-   Por padrão, executando código de usuário gerenciado em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Realizar operações que podem comprometem a eficiência do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser protegido por meio de permissões de alto nível apropriadas.  
  
-   O código de usuário gerenciado não deve ter acesso não autorizado a dados de usuário ou outro código de usuário no banco de dados. O código definido pelo usuário deve ser executado no contexto de segurança da sessão do usuário que o invocou e com os privilégios corretos para o contexto de segurança.  
  
-   Deve haver controles para impedir que o código do usuário acesse qualquer recurso fora do servidor, usando-o estritamente para acesso a dados locais e computação.  
  
-   O código definido pelo usuário não deve obter acesso não autorizado a recursos do sistema em virtude da execução no processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o modelo de segurança baseada em acesso de código do CLR. Algumas das vantagens dessa abordagem combinada em relação à segurança são abordadas nesta seção.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Segurança de acesso do código da integração CLR](clr-integration-code-access-security.md)  
 Discute o modelo CAS (segurança de acesso do código) para código gerenciado.  
  
 [Atributos de proteção de host e programação da Integração CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)  
 Fornece informações sobre valores HPA (atributo de proteção do host) que são desaprovados nos assemblies SAFE e EXTERNAL_ACCESS.  
  
 [Links em segurança da integração CLR](../../../database-engine/dev-guide/links-in-clr-integration-security.md)  
 Descreve como partes do código do usuário podem se chamar uma à outra no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Representação e segurança de integração CLR](../../../database-engine/dev-guide/impersonation-and-clr-integration-security.md)  
 Aborda como o código gerenciado acessa recursos externos que usam representação.  
  
 [Permitindo chamadores parcialmente confiáveis](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
 Aborda problemas que surgem quando um método gerenciado invoca um método em uma classe contida em outro assembly.  
  
 [Domínios do aplicativo e segurança da integração CLR](../../../database-engine/dev-guide/application-domains-and-clr-integration-security.md)  
 Descreve como os assemblies são carregados em domínios de aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de assemblies de integração CLR](../assemblies/managing-clr-integration-assemblies.md)  
  
  