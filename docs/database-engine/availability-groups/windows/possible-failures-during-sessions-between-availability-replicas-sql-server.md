---
title: "Possíveis falhas durante sessões entre réplicas de disponibilidade (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- troubleshooting [SQL Server], HADR
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], troubleshooting
ms.assetid: cd613898-82d9-482f-a255-0230a6c7d6fe
caps.latest.revision: "12"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3dea241da7685b1091704416c3a4a658198cfc4d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="possible-failures-during-sessions-between-availability-replicas-sql-server"></a>Possíveis falhas durante sessões entre réplicas de disponibilidade (SQL Server)
Problemas físicos, do sistema operacional ou do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem provocar uma falha em uma sessão entre duas réplicas de disponibilidade. Uma réplica de disponibilidade não verifica regularmente os componentes dos quais o Sqlservr.exe depende para verificar se estão funcionando corretamente ou se houve falha. Porém, para alguns tipos de falhas, o componente afetado informa um erro ao Sqlservr.exe. Um erro informado por outro componente é chamado um *erro de hardware*. Para detectar outras falhas, que de outra forma passariam despercebidas, o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] implementa seu próprio mecanismo de tempo limite de sessão. Especifica o tempo limite da sessão, em segundos. Esse tempo limite é o tempo máximo que uma instância de servidor espera para receber uma mensagem PING de outra instância antes de considerá-la desconectada. Quando um tempo limite de sessão ocorre entre duas réplicas de disponibilidade, as réplicas de disponibilidade pressupõem que ocorreu uma falha e declaram um *erro de software*.  
  
> [!IMPORTANT]  
>  Falhas em bancos de dados diferentes do banco de dados primário não são detectáveis. Além disso, é improvável que uma falha no disco de dados seja detectada, a menos que o banco de dados seja reiniciado por causa de uma falha no disco de dados.  
  
 A velocidade da detecção de erro e, consequentemente, o tempo de reação de uma falha depende do tipo do erro: de hardware ou de software. Alguns erros de hardware, como falhas de rede, são informados imediatamente. Porém, em alguns casos, períodos de tempo limite específicos do componente podem atrasar o relatório de alguns erros de hardware. Para erros de software, a duração do tempo limite da sessão determina a velocidade da detecção de erros. Por padrão, esse período é 10 segundos. Esse é o valor mínimo recomendado.  
  
## <a name="failures-due-to-hard-errors"></a>Falhas devido a erros de hardware  
 As possíveis causas de erros de hardware incluem (mas não se limitam a) as seguintes condições:  
  
-   Uma conexão ou um cabo interrompido  
  
-   Uma placa de rede incorreta  
  
-   Uma alteração no roteador  
  
-   Alterações no firewall  
  
-   Reconfiguração de ponto de extremidade  
  
-   Perda da unidade onde o log de transações reside  
  
-   Falha de sistema operacional ou de processo  
  
 Por exemplo, quando a unidade de log do banco de dados primário se torna sem resposta e apresenta uma falha, o sistema operacional informa ao Sqlservr.exe que ocorreu um erro grave.  
  
 Alguns componentes, como componentes de rede e alguns subsistemas de E/S, têm seus próprios tempos limite para determinar falhas. Esses tempos limite são independentes do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], que não tem conhecimento sobre eles e não sabe absolutamente nada sobre seu comportamento. Nesses casos, o atraso do tempo limite aumenta o tempo entre uma falha e o momento em que a réplica de disponibilidade recebe o erro de hardware resultante.  
  
> [!NOTE]  
>  A única verificação de erros ativa executada para réplicas de disponibilidade ocorre nos casos de erros de software. Para obter mais informações, consulte "Falhas devido a erros de software", mais adiante neste tópico.  
  
 Para ajudar o usuário a interpretar as condições de erro que ocorrem na rede, pergunte a um engenheiro de rede quais são as mensagens de erro enviadas a uma porta quando os seguintes eventos ocorrem em uma conexão TCP:  
  
-   DNS não está funcionando.  
  
-   Cabos estão desconectados.  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] O Windows tem um firewall que bloqueia uma porta específica.  
  
-   Falha no aplicativo que está monitorando uma porta.  
  
-   Um servidor baseado no Windows é renomeado.  
  
-   Um servidor baseado no Windows é reinicializado.  
  
> [!NOTE]  
>  O [!INCLUDE[ssHADRc](../../../includes/sshadrc-md.md)] não protege contra problemas específicos para clientes que acessam os servidores. Considere, por exemplo, um caso em que um adaptador de rede pública controla as conexões de cliente com a réplica primária, enquanto uma placa de interface de rede privada controla todo o tráfego entre as instâncias do servidor que estão hospedando as réplicas de um grupo de disponibilidade. Nesse caso, uma falha do adaptador de rede pública impediria os clientes de acessarem os bancos de dados.  
  
## <a name="failures-due-to-soft-errors"></a>Falhas devido a erros recuperáveis  
 As condições que poderiam provocar expirações do tempo limite de sessão (mas não apenas estas) incluem as seguintes:  
  
-   Erros de rede, como tempos-limite de link de TCP, pacotes descartados ou corrompidos ou pacotes que estão em ordem incorreta.  
  
-   Um sistema operacional pendente, servidor ou estado de banco de dados.  
  
-   Um servidor Windows que atingiu o tempo limite.  
  
-   Recursos computacionais insuficientes, tais como sobrecarga de uma CPU ou disco, filling up do log de transações ou o sistema está sendo executado sem memória ou threads. Nesses casos, é preciso aumentar o período de tempo limite, reduzir a carga de trabalho ou alterar o hardware para controlar a carga de trabalho.  
  
### <a name="the-session-timeout-mechanism"></a>O mecanismo de tempo-limite de sessão  
 Como erros recuperáveis não são detectáveis diretamente por uma instância de servidor, esse tipo de erro pode fazer com que uma réplica de disponibilidade espere indefinidamente uma resposta da outra réplica de disponibilidade em uma sessão. Para evitar isso, o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] implementa um mecanismo de tempo limite de sessão com base nas réplicas de disponibilidade conectadas, enviando um ping em cada conexão aberta em um intervalo fixo. A recepção de um ping durante o período de tempo-limite indica que a conexão ainda está aberta e que as instâncias do servidor estão se comunicando por ela. Ao receber um ping, uma réplica reajusta seu contador de tempo limite naquela conexão. Para obter informações sobre a relação de tempos limite de sessão e modo de disponibilidade, veja [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
  
 As réplicas primárias e secundárias executam ping uma da outra para sinalizar que ainda estão ativas e um tempo limite de sessão impede que as réplicas esperem indefinidamente para receber um ping da outra réplica. O tempo limite de sessão é uma propriedade de réplica configurável pelo usuário com um valor padrão de 10 segundos. A recepção de um ping durante o período de tempo-limite indica que a conexão ainda está aberta e que as instâncias do servidor estão se comunicando por ela. Durante o recebimento de um ping, uma réplica de disponibilidade redefine seu contador de tempo limite nessa conexão.  
  
 Se nenhum ping for recebido da outra réplica dentro do período de tempo limite da sessão, ocorrerá o tempo limite da conexão. A conexão é fechada e a réplica de tempo limite entra no estado DISCONNECTED. Até mesmo se uma réplica desconectada estiver configurada para o modo de confirmação assíncrona, as transações não esperarão que a réplica se reconecte e seja sincronizada novamente.  
  
## <a name="responding-to-an-error"></a>Respondendo a um erro  
 Independentemente do tipo de erro, uma instância do servidor que detecta um erro responde adequadamente com base na função da instância, no modo de disponibilidade da sessão e no estado de qualquer outra conexão na sessão. Para obter informações sobre o que ocorre na perda de um parceiro, veja [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 **Para alterar o valor de tempo limite (apenas no modo de disponibilidade de confirmação síncrona)**  
  
-   [Alterar o período de tempo limite da sessão de uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Exibir o valor atual de tempo-limite**  
  
-   Consulte **session_timeout** em [sys.availability_replicas &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
