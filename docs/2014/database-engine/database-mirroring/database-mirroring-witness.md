---
title: Testemunha de espelhamento de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- witness [SQL Server], about witness
- witness [SQL Server]
- database mirroring [SQL Server], witness
ms.assetid: 05606de8-90c3-451a-938d-1ed34211dad7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 682a3692414f89beb0c5e0f0204bc1a69b532e64
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807613"
---
# <a name="database-mirroring-witness"></a>Testemunha de espelhamento de banco de dados
  Para dar suporte a failover automático, a sessão de espelhamento de banco de dados deve ser configurada em modo de alta segurança e também deve possuir uma terceira instância de servidor, conhecida como *testemunha*. A testemunha é uma instância opcional do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite ao servidor espelho, em uma sessão de modo de alta segurança, reconhecer se um failover automático deve ser iniciado. Ao contrário dos dois parceiros, a testemunha não atende ao banco de dados. O suporte ao failover automático é a única função da testemunha.  
  
> [!NOTE]  
>  No modo de alto desempenho, a testemunha pode prejudicar a disponibilidade. Se uma testemunha for configurada para uma sessão de espelhamento de banco de dados, o servidor principal deverá ser conectado a pelo menos uma das outras instâncias de servidor, o servidor espelho ou a testemunha, ou ambos. Caso contrário, o banco de dados ficará indisponível e será impossível forçar o serviço (com possível perda de dados). Portanto, para o modo de alto desempenho, é altamente recomendável que você sempre mantenha a testemunha definida como OFF. Para obter informações sobre o impacto de uma testemunha no modo de alto desempenho, veja [Modos de operação de espelhamento de banco de dados](database-mirroring-operating-modes.md).  
  
 A ilustração a seguir mostra uma sessão de modo de alta segurança com uma testemunha.  
  
 ![Sessão de espelhamento com uma testemunha](../media/dbm-3-way-session-intro.gif "Mirroring session with a witness")  
  
 **Neste tópico:**  
  
-   [Usando uma testemunha em várias sessões](#InMultipleSessions)  
  
-   [Recomendações de software e hardware](#SwHwRecommendations)  
  
-   [Função da testemunha no failover automático](#InAutoFo)  
  
-   [Para adicionar ou remover uma testemunha](#AddRemoveWitness)  
  
##  <a name="InMultipleSessions"></a> Usando uma testemunha em várias sessões  
 Uma instância de servidor específica pode agir como uma testemunha em sessões de espelhamento de banco de dados, cada uma para um banco de dados diferente. As sessões diferentes podem ser com parceiros diferentes. A ilustração a seguir mostra uma instância de servidor que é uma testemunha em duas sessões de espelhamento de banco de dados com parceiros diferentes.  
  
 ![Instância de servidor que é uma testemunha de dois bancos de dados](../media/dbm-witness-in-2-sessions.gif "Instância de servidor que é uma testemunha de dois bancos de dados")  
  
 Uma instância de servidor único também pode funcionar ao mesmo tempo como uma testemunha em algumas sessões e um parceiro em outras sessões. Porém, na prática, uma instância de servidor normalmente funciona como uma testemunha ou um parceiro. Isso porque os parceiros exigem computadores sofisticados com hardware suficiente para oferecer suporte a um banco de dados de produção, ao passo que a testemunha pode ser executada em qualquer sistema Windows disponível que ofereça suporte ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
##  <a name="SwHwRecommendations"></a> Recomendações de software e hardware  
 A localização da testemunha em um computador separado dos parceiros é altamente recomendável. Os parceiros de espelhamento de banco de dados só têm suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard edition e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Enterprise edition. As testemunhas, em contrapartida, também têm suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Workgroup e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express. Exceto durante uma atualização de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as instâncias de servidor em uma sessão de espelhamento devem todas estar executando a mesma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, uma testemunha do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tem suporte quando você está atualizando de uma configuração de espelhamento do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , mas não pode ser adicionada a uma configuração de espelhamento do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] existente, nova ou posterior.  
  
 Uma testemunha pode ser executada em qualquer sistema de computador confiável que forneça suporte a quaisquer edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, é recomendável que toda instância de servidor usada como testemunha atenda à configuração mínima exigida para a versão Standard do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo executada. Para obter mais informações sobre esses requisitos, consulte [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
##  <a name="InAutoFo"></a> Função da testemunha no failover automático  
 Ao longo de uma sessão de espelhamento de banco de dados, todas as instâncias de servidor monitoram seus status de conexão. Se os parceiros forem desconectados uns dos outros, confiarão na testemunha para assegurar que apenas um deles esteja atendendo ao banco de dados atualmente. Se um servidor espelho sincronizado perder sua conexão com o servidor principal, mas continuar conectado à testemunha, o servidor espelho entrará em contato com a testemunha para determinar se a testemunha perdeu sua conexão com o servidor principal:  
  
-   Se o servidor principal ainda estiver conectado à testemunha, não acontecerá o failover automático. Em vez disso, o servidor principal continuará atendendo ao banco de dados enquanto estiver acumulando registros de log para enviar ao servidor espelho quando os parceiros forem reconectados.  
  
-   Se a testemunha também estiver desconectada do servidor principal, o servidor espelho saberá que o banco de dados principal ficou indisponível. Nesse caso, o servidor espelho iniciará imediatamente um failover automático.  
  
-   Se o servidor espelho estiver desconectado da testemunha e também do servidor principal, não será possível o failover automático, independentemente do estado do servidor principal.  
  
 O requisito de que pelo menos duas das instâncias de servidor estejam conectadas é conhecido como *quorum*. O quorum assegura que o banco de dados só possa ser atendido por um parceiro de cada vez. Para obter informações sobre como o quorum funciona e seu impacto em uma sessão, consulte [Quorum: Como uma testemunha afeta a disponibilidade do banco de dados &#40;Espelhamento de Banco de Dados&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
##  <a name="AddRemoveWitness"></a> Para adicionar ou remover uma testemunha  
 **Para adicionar uma testemunha**  
  
-   [Adicionar ou substituir uma testemunha de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](../database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
-   [Adicionar uma testemunha de espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
 **Para remover a testemunha**  
  
-   [Remover a testemunha de uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Modos de operação de espelhamento de banco de dados](database-mirroring-operating-modes.md)   
 [Quorum: Como uma testemunha afeta a disponibilidade do banco de dados &#40;espelhamento de banco de dados&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md)   
 [Possíveis falhas durante o espelhamento de banco de dados](possible-failures-during-database-mirroring.md)   
 [Estados de espelhamento &#40;SQL Server&#41;](mirroring-states-sql-server.md)  
  
  
