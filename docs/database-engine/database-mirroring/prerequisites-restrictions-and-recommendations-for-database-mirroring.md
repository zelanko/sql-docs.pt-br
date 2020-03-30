---
title: 'Espelhamento de banco de dados: Pré-requisitos, restrições e recomendações'
description: Saiba mais sobre os pré-requisitos, as restrições e as recomendações para configurar o espelhamento de banco de dados com o SQL Server.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- partners [SQL Server]
- database mirroring [SQL Server], prerequisites
- database mirroring [SQL Server], recommendations
- database mirroring [SQL Server], restrictions
- database mirroring [SQL Server], planning
- database mirroring [SQL Server], about database mirroring
ms.assetid: fdcf2251-9895-44c6-b81e-768fef32e732
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1f6a1c47cf5672cdf0f9a22be6a252cfc8cdbe87
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75244374"
---
# <a name="prerequisites-restrictions-and-recommendations-for-database-mirroring"></a>Pré-requisitos, restrições e recomendações para espelhamento de banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
 Este tópico descreve os pré-requisitos e as recomendações para configuração do espelhamento de banco de dados. Para obter uma introdução ao espelhamento de banco de dados, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
  
##  <a name="support-for-database-mirroring"></a><a name="DbmSupport"></a> Suporte para espelhamento de banco de dados  
 Para obter mais informações sobre o suporte para o espelhamento de banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte [Edições e recursos com suporte do SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).
  
 Observe que o espelhamento de banco de dados funciona com qualquer nível de compatibilidade de banco de dados com suporte. Para obter informações sobre os níveis de compatibilidade com suporte, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Para que uma sessão de espelhamento seja estabelecida, os parceiros e a testemunha, se houver, deverão ser executados na mesma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Os dois parceiros, ou seja, o servidor principal e servidor espelho, deve estar executando a mesma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A testemunha, se houver, pode ser executada em qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que oferecer suporte ao espelhamento de banco de dados.  
  
    > [!NOTE]  
    >  Você pode atualizar instâncias de servidor parceiras em uma sessão de espelhamento para uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Atualizando instâncias espelhadas](../../database-engine/database-mirroring/upgrading-mirrored-instances.md).  
  
-   O banco de dados deve usar o modelo de recuperação completa. Os modelos de recuperação simples e bulk-logged não oferecem suporte ao espelhamento de banco de dados. Por isso, todas as operações em massa são sempre totalmente registradas para um banco de dados espelhado. Para obter informações sobre modelos de recuperação, veja [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
-   Verifique se o servidor espelho tem espaço em disco suficiente para o banco de dados espelho.  
  
    > [!NOTE]  
    >  Para obter informações sobre como usar o espelhamento de banco de dados em um banco de dados replicado, veja [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
-   Quando você está criando o banco de dados espelho no servidor espelho, assegure-se de restaurar o backup do banco de dados principal especificando o mesmo nome de banco de dados WITH NORECOVERY. Além disso, todos os backups de log criados depois daquele backup também devem ser aplicados, novamente com WITH NORECOVERY.  
  
    > [!IMPORTANT]  
    >  Se o espelhamento de banco de dados for interrompido, antes que você possa reiniciá-lo, todos os backups de logs subsequentes do banco de dados principal deverão ser aplicados ao banco de dados espelho.  
  
  
##  <a name="restrictions"></a><a name="Restrictions"></a> Restrições  
  
-   Somente bancos de dados de usuários podem ser espelhados. Você não pode espelhar os bancos de dados **master**, **msdb**, **tempdb**ou **model** .  
  
-   Um banco de dados espelhado não pode ser renomeado durante uma sessão de espelhamento de banco de dados.  
  
-   O espelhamento de banco de dados não oferece suporte a FILESTREAM. Um grupo de arquivos FILESTREAM não pode ser criado no servidor principal. O espelhamento de banco de dados não pode ser configurado para um banco de dados que contenha grupos de arquivos FILESTREAM.  
  
-   Não há suporte para espelhamento de banco de dados com transações de banco de dados cruzado ou transações distribuídas. Para obter mais informações, consulte [Transações entre bancos de dados e transações distribuídas para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
  
##  <a name="recommendations-for-configuring-partner-servers"></a><a name="RecommendationsForPartners"></a> Recomendações para configuração de servidores de parceiro  
  
-   Os parceiros devem ser executados em sistemas comparáveis que podem controlar cargas de trabalho idênticas.  
  
    > [!NOTE]  
    >  Se você planeja usar modo de alta segurança com failover automático, a carga normal em cada parceiro de failover deve ser menor que 50 por cento da CPU. Se sua carga de trabalho sobrecarregar a CPU, haverá a possibilidade de um parceiro de failover não verificar as outras instâncias de servidor na sessão de espelhamento. Isso causa um failover desnecessário. Se você não puder manter o uso de CPU abaixo de 50 por cento, recomendaremos que use o modo alta segurança sem failover automático ou modo de alto desempenho.  
  
-   Se possível, o caminho (inclusive a letra da unidade) do banco de dados espelho deve ser idêntico ao caminho do banco de dados principal. Será necessário incluir a opção MOVE na instrução RESTORE se os layouts de arquivo forem diferentes. Por exemplo, se o banco de dados principal estiver na unidade 'F:' mas o sistema espelho não tiver uma unidade F:.  
  
    > [!IMPORTANT]  
    >  Se você mover os arquivos de banco de dados quando estiver criando o banco de dados espelho, é possível que não consiga adicionar arquivos ao banco de dados posteriormente, sem suspender o espelhamento.  
  
-   Todas as instâncias de servidor em uma sessão de espelhamento devem usar a mesma página de código mestre e ordenação. Diferenças podem causar um problema durante a sessão de espelhamento.  
  
-   Opcionalmente, calcule a hora de parar um banco de dados, para garantir que a configuração do sistema fornecerá o desempenho solicitado. Para obter mais informações, veja [Estime a interrupção do serviço durante troca de função &#40;Espelhamento de Banco de Dados&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md).  
  
-   Para obter um melhor desempenho, use um adaptador de rede dedicado (placa de interface de rede) para espelhamento.  
  
-   Não fazemos nenhuma recomendação sobre a confiabilidade de uma WAN (rede de longa distância) para espelhamento de banco de dados no modo de alta segurança. Se você decidir usar o modo de alta segurança em uma WAN, cuidado ao adicionar uma testemunha à sessão, porque podem ocorrer failovers automáticos indesejados. Para obter mais informações, veja [Recomendações para implantação de espelhamento de banco de dados](#RecommendationsForDeploying), posteriormente neste tópico.  
  
  
##  <a name="recommendations-for-deploying-database-mirroring"></a><a name="RecommendationsForDeploying"></a> Recomendações para implantação de espelhamento de banco de dados  
 Um desempenho ideal de espelhamento de banco de dados é obtido usando uma operação assíncrona. Uma sessão de espelhamento que usa operação síncrona pode experimentar desempenho reduzido quando sua carga de trabalho gerar grandes quantidades de dados de log de transações.  
  
 Em ambientes de teste, é apropriado explorar todos os modos operacionais para avaliar o desempenho do espelhamento de banco de dados. Porém, antes de implantar o espelhamento em um ambiente de produção, verifique se você entendeu o funcionamento real da rede.  
  
 O modo de alta segurança com failover automático é projetado para uma rede de muito serviço que tem uma conexão dedicada, ou uma configuração de rede bastante simples que minimiza as origens de possíveis falhas na rede. Tal ambiente de rede de alta qualidade é necessário no modo de alta segurança com failover automático e é recomendado em todas as sessões de espelhamento de banco de dados. No entanto, o modo de alto desempenho e o modo de alta segurança sem failover automático são muito menos afetados pela confiabilidade da rede.  
  
 Portanto, para ambientes de produção, recomendamos que você obedeça às seguintes diretrizes de implantação:  
  
1.  Inicie a execução no modo assíncrono, de alto desempenho. Esse modo é o menos sensível ao ambiente de rede e fornece a melhor configuração para explorar o espelhamento. Recomendamos que você execute seu sistema de forma assíncrona até ter confiança de que sua largura de banda oferece suporte ao espelhamento e ter desenvolvido uma compreensão da configuração de espelhamento e do desempenho do modo assíncrono em seu ambiente. Para obter mais informações, consulte [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
    > [!IMPORTANT]  
    >  Durante o teste, recomendamos que você monitore suas sessões quanto a erros de rede que possam causar falhas no espelhamento de banco de dados. Para obter mais informações sobre origens de falha potenciais, consulte [Possible Failures During Database Mirroring](../../database-engine/database-mirroring/possible-failures-during-database-mirroring.md). Para obter informações sobre como monitorar o espelhamento de banco de dados, veja [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md).  
  
2.  Quando você tiver certeza de que a operação assíncrona está atendendo a suas necessidades empresariais, tente a operação síncrona para aumentar a proteção dos dados. Quando você testar o funcionamento do espelhamento síncrono em seu ambiente, recomendamos que tente primeiro o modo de alta segurança sem failover automático. O principal objetivo desse teste é verificar como a operação síncrona afeta o desempenho do banco de dados. Para obter mais informações, consulte [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
3.  Aguarde para habilitar o failover automático até que esteja confiante de que o modo de alta segurança sem failover automático esteja atendendo às necessidades comerciais e que os erros de rede não estejam provocando falhas. Para obter mais informações, consulte [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).  
  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
