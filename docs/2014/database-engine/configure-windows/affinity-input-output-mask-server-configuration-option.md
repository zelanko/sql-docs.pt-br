---
title: Opção de configuração de servidor affinity Input-Output mask | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- affinity I/O mask option
- processor affinity [SQL Server]
- binding processors [SQL Server]
- CPU affinity mask option
ms.assetid: 9950a8c9-9fe0-4003-95df-6f0d1becb0e7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 65e412a3dfdfc71931e6af4d449c5be88ae351b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62813674"
---
# <a name="affinity-input-output-mask-server-configuration-option"></a>Opção de configuração do servidor de máscara de Entrada-Saída de afinidade
  Para realizar multitarefa, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 e o Windows Server 2003 às vezes movem threads de processos entre processadores diferentes. Embora eficiente de um ponto de vista de sistema operacional, essa atividade pode reduzir o desempenho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sob cargas de sistema pesadas, à medida que cada cache de processador é recarregado repetidamente com dados. Atribuir processadores a threads específicos poderá melhorar o desempenho sob estas condições eliminando recargas de processador; tal associação entre um thread e um processador é chamada de afinidade de processador.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dá suporte à afinidade de processador por meio de duas opções de máscara de afinidade: **máscara de afinidade** (também conhecida como máscara de **afinidade de CPU**) e **máscara de e/s de afinidade**. Para obter mais informações sobre a opção **affinity mask** , veja [Opção affinity mask de configuração de servidor](affinity-mask-server-configuration-option.md). O suporte à afinidade de CPU e e/s para servidores com 33 a 64 processadores exige o uso adicional da [opção de configuração de servidor affinity64 mask](affinity64-mask-server-configuration-option.md) e da [opção de configuração de servidor affinity64 de entrada/saída de máscara,](affinity64-input-output-mask-server-configuration-option.md) respectivamente.  
  
> [!NOTE]  
>  O suporte à afinidade para servidores com 33 a 64 processadores só está disponível em sistemas operacionais de 64 bits.  
  
 A opção **Affinity i/o Mask** associa a e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /s de disco a um subconjunto especificado de CPUs. Em ambientes OLTP (online transactional processing) avançados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , esta extensão pode aumentar o desempenho de threads [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que emitem E/S. Este aprimoramento não aceita afinidade de hardware para discos individuais ou controladores de disco.  
  
 O valor de **affinity I/O mask** especifica que CPUs em um computador multiprocessador são qualificadas para processar operações E/S de disco do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A máscara é um bitmap no qual o bit mais à direita especifica a CPU de ordem mais inferior (0), o bit a sua esquerda imediata especifica a CPU de ordem inferior mais próxima (1) e assim por diante. Para configurar mais de 32 processadores, defina **affinity I/O mask** e **affinity64 I/O mask**.  
  
 Os valores de **affinity I/O mask** são os seguintes:  
  
-   Uma **affinity I/O mask** de 1 byte abrange até 8 CPUs em um computador multiprocessador.  
  
-   Uma **affinity I/O mask** de 2 bytes abrange até 16 CPUs em um computador multiprocessador.  
  
-   Uma **affinity I/O mask** de 3 bytes abrange até 24 CPUs em um computador multiprocessador.  
  
-   Uma **affinity I/O mask** de 4 bytes abrange até 32 CPUs em um computador multiprocessador.  
  
-   Para abranger mais de 32 CPUs, configure uma **affinity I/O mask** de quatro bytes para as primeiras 32 CPUs e uma **affinity64 I/O mask** de até quatro bytes para as CPUs restantes.  
  
 1 bit no padrão de Afinidade E/S especifica que a CPU correspondente é elegível para executar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operações E/S de disco; um 0 bit especifica que nenhuma operação E/S de disco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deveria ser programada para a CPU correspondente. Quando todos os bits são definidos para zero ou a **affinity I/O mask** não é especificada, a E/S de disco do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é agendada para quaisquer das CPUs qualificadas para processar threads do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Como a configuração da opção máscara de E/S de afinidade[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ** do ** é uma operação especializada, deverá ser usada apenas quando necessário. Na maioria dos casos, a afinidade padrão de Windows 2000 ou Windows Server 2003 provê o melhor desempenho.  
  
 Ao especificar a opção **affinity I/O mask** , você deve usá-la com a opção de configuração **affinity mask** . Não habilite a mesma CPU nas opções **affinity I/O mask** e **affinity mask** . Os bits que correspondem a cada CPU deveriam estar em um dos três estados seguintes:  
  
-   0 nas opções **affinity I/O mask** e **affinity mask** .  
  
-   1 na opção **affinity I/O mask** e 0 na opção **affinity mask** .  
  
-   0 na opção **affinity I/O mask** e 1 na opção **affinity mask** .  
  
 
  **affinity I/O mask** é uma opção avançada. Se você estiver usando o `sp_configure` procedimento armazenado do sistema para alterar a configuração, poderá alterar a **máscara de e/s de afinidade** somente quando a **opção Mostrar opções avançadas** estiver definida como 1. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], reconfigurar a opção **affinity I/O mask** exige uma reinicialização da instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!CAUTION]  
>  Não configure afinidade de CPU no sistema operacional Windows e também configure a máscara de afinidade em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas definições estão tentando alcançar o mesmo resultado e se as configurações forem inconsistentes, você poderá ter resultados imprevisíveis. A afinidade da CPU [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é mais bem configurada usando a opção `sp_configure` em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
