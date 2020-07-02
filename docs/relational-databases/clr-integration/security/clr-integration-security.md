---
title: Segurança de integração CLR | Microsoft Docs
description: SQL Server integração com o .NET Framework a segurança do CLR gerencia o acesso entre objetos. As verificações de segurança realizadas em objetos dependem das chamadas envolvidas.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- authorization [CLR integration]
- common language runtime [SQL Server], security
- database objects [CLR integration], security
ms.assetid: 05d7a471-c5d5-4730-b903-e4edc8157bb4
author: rothja
ms.author: jroth
ms.openlocfilehash: c81f513b40945e3c535d16c822016f24a0cfaa62
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723858"
---
# <a name="clr-integration-security"></a>Segurança da integração CLR

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  O modelo de segurança da integração do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o CLR (Common Language Runtime) [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] gerencia e protege o acesso entre tipos diferentes de objetos CLR e não CLR em execução no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esses objetos podem ser chamados por uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou outro objeto CLR em execução no servidor. As chamadas entre objetos conhecidas como links. Os tipos de verificações de segurança realizados nesses objetos dependem dos tipos de links envolvidos.  
  
 O modelo de segurança de integração do CLR tem as seguintes metas:  
  
-   Por padrão, executar código de usuário gerenciado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não deve comprometer a integridade e a estabilidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Realizar operações que podem comprometem a eficiência do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser protegido por meio de permissões de alto nível apropriadas.  
  
-   O código de usuário gerenciado não deve ter acesso não autorizado a dados de usuário ou outro código de usuário no banco de dados. O código definido pelo usuário deve ser executado no contexto de segurança da sessão do usuário que o invocou e com os privilégios corretos para o contexto de segurança.  
  
-   Deve haver controles para impedir que o código do usuário acesse qualquer recurso fora do servidor, usando-o estritamente para acesso a dados locais e computação.  
  
-   O código definido pelo usuário não deve obter acesso não autorizado a recursos do sistema em virtude da execução no processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agora integra o modelo de segurança baseado no usuário do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o modelo de segurança baseado no acesso ao código do CLR. Algumas das vantagens dessa abordagem combinada em relação à segurança são abordadas nesta seção.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Segurança de acesso a código da integração CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
 Discute o modelo CAS (segurança de acesso do código) para código gerenciado.  
  
 [Atributos de proteção de host e programação da Integração CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)  
 Fornece informações sobre valores HPA (atributo de proteção do host) que são desaprovados nos assemblies SAFE e EXTERNAL_ACCESS.  
  
 [Links em segurança da integração CLR](https://msdn.microsoft.com/library/168efd01-d12e-4bdf-a1b3-0b5c76474eaf)  
 Descreve como partes do código do usuário podem se chamar uma à outra no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Representação e segurança de integração CLR](https://msdn.microsoft.com/library/1495a7af-2248-4cee-afdb-9269fb3a7774)  
 Aborda como o código gerenciado acessa recursos externos que usam representação.  
  
 [Permitindo chamadores parcialmente confiáveis](https://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
 Aborda problemas que surgem quando um método gerenciado invoca um método em uma classe contida em outro assembly.  
  
 [Domínios do aplicativo e segurança da integração CLR](/sql/database-engine/dev-guide/allowing-partially-trusted-callers?view=sql-server-2014)  
 Descreve como os assemblies são carregados em domínios de aplicativo.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando assemblies de integração CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
  
  
