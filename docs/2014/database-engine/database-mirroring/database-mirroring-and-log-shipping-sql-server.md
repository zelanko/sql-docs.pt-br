---
title: Espelhamento de banco de dados e envio de logs (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- log shipping [SQL Server], database mirroring
ms.assetid: 53e98134-e274-4dfd-8b72-0cc0fd5c800e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ca584a81b8ba70073ee833d8033cd5f664747741
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62807444"
---
# <a name="database-mirroring-and-log-shipping-sql-server"></a>Espelhamento de banco de dados e envio de logs (SQL Server)
  Um determinado banco de dados pode ser espelhado ou ter o log enviado; ou ter os dois processos realizados simultaneamente. Para escolher o método a ser usado, considere o seguinte:  
  
-   Você precisa de quantos servidores de destino?  
  
     Se você precisar de um único banco de dados de destino, o espelhamento de banco de dados será a solução indicada.  
  
     Se você precisar de mais de um banco de dados de destino, deverá usar o envio de logs, sozinho ou com o espelhamento de banco de dados. A combinação dos dois métodos traz os benefícios de um espelhamento de banco de dados com o suporte de vários destinos fornecido pelo envio de logs.  
  
-   Caso precise adiar a restauração do log no banco de dados de destino (geralmente, para se proteger contra erros lógicos), use o envio de logs, sozinho ou com o espelhamento de banco de dados.  
  
 Este tópico aborda as considerações sobre como combinar o envio de logs com o espelhamento de banco de dados.  
  
> [!NOTE]  
>  Para introduções a essas tecnologias, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md) e [Sobre o envio de Log &#40;SQL Server&#41;](../log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="combining-log-shipping-and-database-mirroring"></a>Combinando o envio de logs e o espelhamento de banco de dados  
 O banco de dados principal em uma sessão de espelhamento também pode agir como o banco de dados primário em uma configuração de envio de logs, ou vice-versa; uma vez que o compartilhamento de backup do envio de logs está intacto. A sessão de espelhamento de banco de dados é executada em qualquer modo operacional, síncrono (com a segurança de transação definida como FULL) ou assíncrono (com a segurança de transação definida como OFF).  
  
> [!NOTE]  
>  Para usar o espelhamento de banco de dados em um banco de dados, será sempre necessário o modelo de recuperação completa.  
  
 Geralmente, ao combinar o envio de logs e o espelhamento de banco de dados, a sessão de espelhamento é estabelecida antes do envio de logs, embora isso não seja um exigência. O banco de dados principal atual é configurado como envio de logs primário (o *banco de dados principal/primário*), junto com um ou mais bancos de dados secundários remotos. Além disso, o banco de dados espelho deve ser configurado como envio de logs primário (o *banco de dados espelho/primário*). Os bancos de dados secundários de envio de logs devem ocupar instâncias de servidor diferentes do servidor principal/primário ou servidor espelho/primário.  
  
> [!NOTE]  
>  As configurações de diferenciação de maiúsculas e minúsculas dos servidores envolvidos no envio de logs devem corresponder.  
  
 Durante uma sessão de envio de logs, os trabalhos de backup no banco de dados primário criam backups de log em uma pasta de backup. Nessa pasta, os backups são copiados por trabalhos de cópia dos servidores secundários. Para obterem êxito, os trabalhos de backup e de cópia devem ter acesso à pasta de backup de envio de logs. Para maximizar a disponibilidade do servidor primário, recomendamos que a pasta de backup seja estabelecida em um local de backup compartilhado em um computador host separado. Assegure de que todos os servidores de envio de logs, inclusive o servidor espelho/primário, possam acessar o local de backup compartilhado (conhecido como um *compartilhamento de backup*).  
  
 Para permitir que o envio de logs continue depois que houver falha no espelhamento de banco de dados, você também deverá configurar o servidor espelho como um servidor primário, usando a mesma configuração utilizada para o primário, no banco de dados principal. O banco de dados espelho está no estado de restauração, o que impede que os trabalhos de backup façam o backup do log no banco de dados espelho. Isso assegura que o banco de dados espelho/primário não interfira no banco de dados principal/primário cujos backups de log estão sendo copiados atualmente por servidores secundários. Para evitar alertas falsos, depois que o trabalho de backup é executado no banco de dados espelho/primário, ele emite uma mensagem para a tabela**log_shipping_monitor_history_detail** e o trabalho de agente retorna um status de êxito.  
  
 O banco de dados espelho/primário está inativo na sessão de envio de logs. Porém, se houver falha no espelhamento, o banco de dados espelho anterior ficará online como o banco de dados principal. Nessa altura, aquele banco de dados também fica ativo como o banco de dados primário de envio de logs. Os trabalhos de backup de envio de logs que não puderam enviar previamente o log de envio naquele banco de dados, começam a enviar o log. Reciprocamente, um failover faz com que o banco de dados principal/primário anterior se torne o novo banco de dados espelho/primário e entre em estado de restauração, e os trabalhos de backup naquele banco de dados interrompam o backup de log.  
  
> [!NOTE]  
>  No caso de um failover automático, a alteração para a função espelho acontece quando o banco de dados principal/primário anterior volta à sessão de espelhamento.  
  
 Para executar em modo de segurança alta com failover automático a sessão de espelhamento está configurada com uma instância de servidor adicional conhecida como *testemunha*. Se o banco de dados principal estiver perdido por qualquer motivo, depois que o banco de dados for sincronizado e se o servidor espelho e a testemunha ainda conseguirem se comunicar, haverá um failover automático. Um failover automático faz com que o servidor espelho assuma a função principal e coloque seu banco de dados online como o banco de dados principal. Se o local de backup de envio de logs estiver acessível ao novo servidor principal/primário, seus trabalhos de backup começarão a enviar backups de log àquele local. O modo síncrono do espelhamento de banco de dados garante que a cadeia de logs não seja afetada por um failover de espelhamento, e que somente o log válido seja restaurado. Os servidores secundários continuam copiando backups de log sem saber que uma instância de servidor diferente se tornou o servidor primário.  
  
 Ao usar um monitor de envio de logs local, torna-se desnecessária qualquer consideração especial para acomodar esse cenário. Para obter informações sobre como usar uma instância de monitoramento remoto com esse cenário, consulte "O Impacto do espelhamento de banco de dados em uma instância de monitoramento remoto", mais adiante neste tópico.  
  
## <a name="failing-over-from-the-principal-to-the-mirror-database"></a>Failover do banco de dados principal para o banco de dados espelho  
 A figura a seguir mostra como o envio de logs e o espelhamento de banco dados trabalham juntos quando o espelhamento está sendo executado em modo de alta segurança com failover automático. Inicialmente, o **Server_A** é o servidor principal do espelhamento e o servidor primário do envio de logs. O**Server_B** é o servidor espelho, mas também está configurado como um servidor primário, só que inativo no momento. O**Server_C** e o **Server_D** são servidores de envio de logs secundários. Para maximizar a disponibilidade da sessão de envio de logs, o local de backup fica em um diretório de compartilhamento em um computador host separado.  
  
 ![Envio de logs e espelhamento de banco de dados](../media/logshipping-and-dbm-automatic-failover.gif "Envio de logs e espelhamento de banco de dados")  
  
 Depois de um failover de espelhamento, o nome do servidor primário definido no servidor secundário permanece inalterado. .  
  
## <a name="the-impact-of-database-mirroring-on-a-remote-monitoring-instance"></a>O impacto do espelhamento de banco de dados em uma instância de monitoramento remoto  
 Quando o envio de logs é usado com uma instância de monitoramento remoto, a combinação da sessão de envio de logs e de espelhamento de banco de dados afeta as informações nas tabelas de monitor. As informações sobre o primário formam uma combinação de um configurado no principal/primário e o monitor configurado em cada secundário.  
  
 Para continuar monitorando da maneira mais uniforme possível, ao usar um monitor remoto, recomendamos que você especifique o nome primário original ao configurar o primário no secundário. Essa abordagem também facilita a alteração da configuração de envio de logs do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações sobre o monitoramento, consulte [Monitorar o envio de logs &#40;Transact-SQL&#41;](../log-shipping/monitor-log-shipping-transact-sql.md).  
  
## <a name="setting-up-mirroring-and-log-shipping-together"></a>Configurando um espelhamento e um envio de logs em conjunto  
 Para configurar um espelhamento de banco de dados junto com um envio de logs, siga as seguintes etapas:  
  
1.  Restaure os backups do banco de dados principal/primário com NORECOVERY em outra instância de servidor a ser usada posteriormente como banco de dados espelho do espelhamento de banco de dados para o banco de dados principal/primário. Para obter mais informações, veja [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
2.  Configure um espelhamento de banco de dados. Para obter mais informações, veja [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md) ou [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](setting-up-database-mirroring-sql-server.md).  
  
3.  Restaure os backups do banco de dados principal/primário para outras instâncias do servidor a serem usadas posteriormente como bancos de dados secundários de envio de logs para o banco de dados primário.  
  
4.  Configure um envio de logs no banco de dados principal como o banco de dados primário para um ou mais bancos de dados secundários.  
  
     Você deveria configurar um único compartilhamento como parte como diretório de backup (um compartilhamento de backup). Isso garante que depois da troca de funções entre os servidores principal e espelho, os trabalhos de backup continuam gravando no mesmo diretório que antes. Uma prática recomendada é garantir que esse compartilhamento esteja localizado em um servidor físico diferente dos servidores que hospedam os bancos de dados envolvidos no espelhamento e no envio de logs.  
  
     Para obter mais informações, consulte [Configurar o envio de logs &#40;SQL Server&#41;](../log-shipping/configure-log-shipping-sql-server.md).  
  
5.  Execute o failover manualmente do principal para o espelho.  
  
     Para executar um failover manual:  
  
    -   [Executar failover manualmente de uma sessão de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [Executar failover manualmente em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](manually-fail-over-a-database-mirroring-session-transact-sql.md)  
  
6.  Configure um envio de logs no principal novo (antigo espelho) como sendo o banco de dados primário.  
  
    > [!IMPORTANT]  
    >  Não execute nenhuma configuração de um secundário.  
  
     É necessário usar o mesmo compartilhamento de backup usado na etapa 4.  
  
     A interface **Envio do Log de Transações** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oferece suporte apenas a um banco de dados primário por configuração de envio de logs. Portanto, é necessário usar os procedimentos armazenados para configurar o novo principal como primário.  
  
7.  Execute outro failover manual para failback da entidade original.  
  
  
