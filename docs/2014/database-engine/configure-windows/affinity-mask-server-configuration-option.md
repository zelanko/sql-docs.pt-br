---
title: Opção de configuração de servidor affinity mask | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- default affinity mask option
- reloading processor cache
- processor cache [SQL Server]
- CPU [SQL Server], licensing
- deferred process call
- affinity mask option
- processor affinity [SQL Server]
- SMP
- DPC
ms.assetid: 5823ba29-a75d-4b3e-ba7b-421c07ab3ac1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5bd866520fbace51ee9ef06a547bb528f46b9435
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156136"
---
# <a name="affinity-mask-server-configuration-option"></a>Opção affinity mask de configuração de servidor
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql).  
  
 Para realizar multitarefas, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] , às vezes, movem threads de processos entre processadores diferentes. Embora eficiente de um ponto de vista de sistema operacional, essa atividade pode reduzir o desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sob cargas de sistema pesadas, à medida que cada cache de processador é recarregado repetidamente com dados. Atribuir processadores a threads específicos poderá melhorar o desempenho nessas condições eliminando recargas de processador e reduzindo a migração de thread entre processadores (reduzindo portanto a alternância de contexto); tal associação entre um thread e um processador é chamada de afinidade do processador.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à afinidade de processador por meio de duas opções de máscara de afinidade: máscara de afinidade (também conhecida como **máscara de afinidade de CPU**) e máscara de E/S de afinidade. Para obter mais informações sobre a opção de máscara de opção de E/S de afinidade, veja [Opção de configuração de servidor de máscara de entrada/saída de afinidade](affinity-input-output-mask-server-configuration-option.md). O suporte para afinidade de CPU e E/S em servidores com 33 a 64 processadores exige o uso adicional da [Opção de configuração de servidor de máscara affinity64](affinity64-mask-server-configuration-option.md) e [Opção de configuração de servidor de máscara de entrada/saída affinity64](affinity64-input-output-mask-server-configuration-option.md), respectivamente.  
  
> [!NOTE]  
>  O suporte à afinidade para servidores com 33 a 64 processadores só está disponível em sistemas operacionais de 64 bits.  
  
 A opção de máscara de afinidade, que existia nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], controla dinamicamente a afinidade de CPU.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a opção de máscara de afinidade pode ser configurada sem a necessidade de reiniciar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao usar sp_configure, você deve executar RECONFIGURE ou RECONFIGURE WITH OVERRIDE depois de definir uma opção de configuração. Quando você estiver usando o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], e a opção de máscara de afinidade for alterada, isso não exigirá uma reinicialização.  
  
 As alterações nas máscaras de afinidade ocorrem dinamicamente, permitindo a inicialização e o encerramento sob demanda dos agendadores de CPU que associam threads de processo ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso pode ocorrer enquanto são feitas alterações nas condições do servidor. Por exemplo, se uma instância nova do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for adicionada ao servidor, talvez seja necessário fazer ajustes na opção de máscara de afinidade para redistribuição da carga do processador.  
  
 Modificações em bitmasks de afinidade requerem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar um novo agendador de CPU e desabilitar o agendador de CPU existente. Novos lotes podem então ser processados nos agendadores novos ou restantes.  
  
 Para iniciar um novo agendador de CPU, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um novo agendador e o adiciona à lista de agendadores padrão. O novo agendador só é considerado para os novos lotes de entrada. Os lotes atuais continuam sendo executados no mesmo agendador. Os trabalhadores migram para o agendador novo à medida que ficam livres, ou enquanto os novos trabalhadores são criados.  
  
 Desligar um agendador requer que todos os lotes no agendador tenham concluído suas atividades e sejam encerrados. Um agendador que foi encerrado é marcado como offline, de forma que nenhum lote novo seja agendado nele.  
  
 Se um agendador novo for adicionado ou removido, as tarefas permanentes do sistema, como lockmonitor, ponto de verificação, thread de tarefa de sistema (processando DTC) e processo de sinal continuarão sendo executadas no agendador enquanto o servidor estiver em operação. Essas tarefas permanentes de sistema não são migradas dinamicamente. Para redistribuir a carga de processador para essas tarefas de sistema pelos agendadores, será necessário reinicializar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentar encerrar um agendador associado a uma tarefa permanente de sistema, a tarefa continuará sendo executada no agendador offline (sem migração). Esse agendador é associado aos processadores na máscara de afinidade modificada e não deverá colocar nenhuma carga no processador com o qual tinha afinidade antes da alteração. A presença de agendadores offline adicionais não deve afetar de forma significativa a carga do sistema. Se isso não acontecer, o servidor de banco de dados deverá ser reinicializado para reconfigurar essas tarefas.  
  
 As tarefas de afinidade de E/S (como lazywriter e logwriter) são afetadas diretamente pela máscara de afinidade de E/S. Se as tarefas lazywriter e logwriter não tiverem afinidade, elas seguirão as mesmas regras definidas para as outras tarefas permanentes, como lockmonitor ou ponto de verificação.  
  
 Para assegurar que a nova máscara de afinidade seja válida, o comando RECONFIGURE verifica se as afinidades de CPU e E/S normais são mutuamente exclusivas. Se esse não for o caso, uma mensagem de erro será reportada à sessão do cliente e ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , indicando que essa configuração não é recomendada. A execução das opções RECONFIGURE WITH OVERRIDE permite afinidades de CPU e E/S que não sejam mutuamente exclusivas.  
  
 Se você especificar uma máscara de afinidade que tenta fazer mapeamento para uma CPU inexistente, o comando RECONFIGURE reportará uma mensagem de erro à sessão do cliente e ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O uso da opção RECONFIGURE WITH OVERRIDE não tem nenhum efeito nesse caso, e o mesmo erro de configuração é reportado novamente.  
  
 Você também pode excluir atividade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de processadores com atribuições de carga de trabalho específicas aos sistemas operacionais Windows 2000 ou Windows Server 2003. Se você definir um bit representando um processador como 1, esse processador será selecionado pelo Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atribuição de thread. Quando você define `affinity mask` como 0 (o padrão), o Microsoft Windows 2000 ou Windows Server 2003, algoritmos de agendamento definem a afinidade do thread. Quando você define a `affinity mask` como qualquer valor diferente de zero, a afinidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta o valor como um bitmask que especifica esses processadores qualificados para seleção.  
  
 Ao isolar threads do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da execução em determinados processadores, o Microsoft Windows 2000 ou o Windows Server 2003 pode avaliar melhor como o sistema está controlando os processos específicos do Windows. Por exemplo, em um servidor de 8 CPUs que executa duas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (instâncias A e B), o administrador do sistema poderia usar a opção de máscara de afinidade para atribuir o primeiro conjunto de 4 CPUs à instância A e o segundo conjunto de 4 CPUs à instância B. Para configurar mais de 32 processadores, defina a máscara de afinidade e a máscara de afinidade64. Os valores para `affinity mask` são da seguinte maneira:  
  
-   Uma `affinity mask` de 1 byte abrange até 8 CPUs em um computador multiprocessador.  
  
-   Uma `affinity mask` de 2 bytes abrange até 16 CPUs em um computador multiprocessador.  
  
-   Uma `affinity mask` de 3 bytes abrange até 24 CPUs em um computador multiprocessador.  
  
-   Uma `affinity mask` de 4 bytes abrange até 32 CPUs em um computador multiprocessador.  
  
-   Para incluir mais de 32 CPUs, configure uma máscara de afinidade de 4 bytes para as primeiras 32 CPUs e uma máscara de afinidade64 de quatro bytes para as demais CPUs.  
  
 Como definir a opção de afinidade de processador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é uma operação especializada, recomenda-se que ela só seja usada quando necessário. Na maioria dos casos, a afinidade padrão do Microsoft Windows 2000 ou Windows Server 2003 proporciona o melhor desempenho. Você também deve considerar os requisitos de CPU para outros aplicativos quando definir as máscaras de afinidade. Para obter mais informações, consulte a documentação do sistema operacional Windows.  
  
> [!NOTE]  
>  Você pode usar o Windows System Monitor para exibir e analisar o uso individual de processador.  
  
 Ao especificar a opção de máscara de afinidade de E/S, você deverá usá-la em conjunto com a opção de configuração de máscara de afinidade. Não habilite a mesma CPU na opção de `affinity mask` e na opção de máscara de E/S de afinidade. Os bits correspondentes em cada CPU devem estar em um destes três estados:  
  
-   0 na opção de máscara de afinidade e na opção de máscara de afinidade de E/S.  
  
-   1 na opção de máscara de afinidade e 0 na opção de máscara de E/S de afinidade.  
  
-   0 na opção de máscara de afinidade e 1 na opção de máscara de E/S de afinidade.  
  
> [!CAUTION]  
>  Não configure afinidade de CPU no sistema operacional Windows e também configure a máscara de afinidade em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas definições estão tentando alcançar o mesmo resultado e se as configurações forem inconsistentes, você poderá ter resultados imprevisíveis. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Você poderá configurar melhor a afinidade de CPU no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]com a opção sp_configure.  
  
## <a name="example"></a>Exemplo  
 Como exemplo de configuração da opção de máscara de afinidade, se os processadores 1, 2 e 5 forem selecionados como disponíveis com os bits 1, 2 e 5 definidos como 1 e os bits 0, 3, 4, 6 e 7 definidos como 0, um valor hexadecimal de 0x26 ou o decimal equivalente de `38` será especificado. Numere os bits da direita para a esquerda. A opção de máscara de afinidade inicia a contagem de processadores de 0 a 31, de forma que no exemplo a seguir o contador `1` represente o segundo processador no servidor.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'affinity mask', 38;  
RECONFIGURE;  
GO  
```  
  
 Estes são valores da `affinity mask` para um sistema de 8 CPUs.  
  
|Valor decimal|Máscara de bit binário|Permite threads do SQL Server em processadores|  
|-------------------|---------------------|--------------------------------------------|  
|1|00000001|0|  
|3|00000011|0 e 1|  
|7|00000111|0, 1 e 2|  
|15|00001111|0, 1, 2 e 3|  
|31|00011111|0, 1, 2, 3 e 4|  
|63|00111111|0, 1, 2, 3, 4 e 5|  
|127|01111111|0, 1, 2, 3, 4, 5 e 6|  
|255|11111111|0, 1, 2, 3, 4, 5, 6 e 7|  
  
 A opção de máscara de afinidade é uma opção avançada. Se você estiver usando o procedimento armazenado do sistema sp_configure para alterar a configuração, você poderá alterar `affinity mask` apenas quando **Mostrar opções avançadas** é definido como 1. Após executar o comando RECONFIGURE de [!INCLUDE[tsql](../../includes/tsql-md.md)] , a nova configuração terá efeito imediatamente sem a necessidade de reiniciar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="non-uniform-memory-access-numa"></a>Acesso de memória não uniforme (NUMA)  
 Ao usar hardware baseado em NUMA com a máscara de afinidade definida, todo agendador em um nó terá uma afinidade com sua própria CPU. Quando a máscara de afinidade não estiver definida, cada agendador terá uma afinidade com o grupo de CPUs dentro do nó NUMA e um agendador mapeado para o nó NUMA N1 poderá agendar trabalho em qualquer CPU no nó, mas não em CPUs associadas a outro nó.  
  
 Qualquer operação sendo executada em um único nó NUMA só poderá usar páginas de buffer daquele nó. Quando uma operação é executada paralelamente nas CPUs a partir de vários nós, a memória poderá ser usada a partir de qualquer nó envolvido.  
  
## <a name="licensing-issues"></a>Problemas de licenciamento  
 A afinidade dinâmica é restrita com rigor pelo licenciamento de CPU. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite nenhuma configuração de opções de máscara de afinidade que viole a política de licenciamento.  
  
### <a name="startup"></a>Inicialização  
 Se uma máscara de afinidade especificada violar a política de licenciamento durante a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou durante a anexação do banco de dados, a camada do mecanismo concluirá o processo de inicialização ou a operação de anexação/restauração do banco de dados e depois redefinirá o valor de execução de sp_configure da máscara de afinidade como zero, emitindo uma mensagem de erro para o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="reconfigure"></a>Reconfiguração  
 Se uma máscara de afinidade especificada violar a política de licenciamento ao executar o comando RECONFIGURE de [!INCLUDE[tsql](../../includes/tsql-md.md)] , uma mensagem de erro será reportada à sessão do cliente e ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o administrador do banco de dados terá que reconfigurar a máscara de afinidade. Nenhum comando RECONFIGURE WITH OVERRIDE é aceito nesse caso.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
