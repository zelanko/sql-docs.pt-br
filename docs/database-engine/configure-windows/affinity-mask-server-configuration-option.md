---
title: Opção affinity mask de configuração de servidor
description: Saiba mais sobre a opção affinity mask no SQL Server. Veja um exemplo que a usa para associar processadores a threads específicos.
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
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
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: ''
ms.date: 06/11/2020
ms.openlocfilehash: 94f8406af013bc0720bc16063d1a9881eda94c5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715587"
---
# <a name="affinity-mask-server-configuration-option"></a>Opção affinity mask de configuração de servidor

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

> [!NOTE]
> [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md).

Para realizar multitarefas, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] , às vezes, movem threads de processos entre processadores diferentes. Embora seja eficiente de um ponto de vista de sistema operacional, essa atividade pode reduzir o desempenho do SQL Server sob cargas de sistema pesadas, à medida que cada cache do processador é recarregado repetidamente com os dados. Atribuir processadores a threads específicos poderá aprimorar o desempenho sob estas condições eliminando recargas de processador e reduzindo a migração de threads entre processadores, o que reduz a alternância de contexto. Essa associação entre um thread e um processador é chamada de afinidade de processador.

O SQL Server dá suporte à afinidade de processador por meio de duas opções de máscara de afinidade: affinity mask (também conhecida como **máscara de afinidade de CPU**) e affinity I/O mask. Para obter mais informações sobre a opção affinity I/O mask, veja [Opção de configuração de servidor de máscara de entrada/saída de afinidade](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md). O suporte para afinidade de CPU e E/S em servidores com 33 a 64 processadores exige o uso adicional da [Opção de configuração de servidor de máscara affinity64](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) e [Opção de configuração de servidor de máscara de entrada/saída affinity64](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md), respectivamente.

> [!NOTE]  
> O suporte à afinidade para servidores com 33 a 64 processadores só está disponível em sistemas operacionais de 64 bits.

A opção de máscara de afinidade, que existia nas versões anteriores do SQL Server, controla dinamicamente a afinidade de CPU.

No SQL Server, a opção de máscara de afinidade pode ser configurada sem a necessidade de reiniciar a instância do SQL Server. Ao usar sp_configure, você deve executar RECONFIGURE ou RECONFIGURE WITH OVERRIDE depois de definir uma opção de configuração. Quando você estiver usando o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], alterar a opção de máscara de afinidade não exigirá uma reinicialização.

As alterações nas máscaras de afinidade ocorrem dinamicamente, permitindo a inicialização e o encerramento sob demanda dos agendadores de CPU que associam threads de processo ao SQL Server. Isso pode ocorrer enquanto são feitas alterações nas condições do servidor. Por exemplo, se uma instância nova do SQL Server for adicionada ao servidor, talvez seja necessário fazer ajustes na opção de máscara de afinidade para redistribuição da carga do processador.

Modificações em bitmasks de afinidade requerem o SQL Server para habilitar um novo agendador de CPU e desabilitar o agendador de CPU existente. Novos lotes podem então ser processados nos agendadores novos ou restantes.

Para iniciar um novo agendador de CPU, o SQL Server cria um agendador e o adiciona à lista de agendadores padrão. O novo agendador só é considerado para os novos lotes de entrada. Os lotes atuais continuam sendo executados no mesmo agendador. Os trabalhadores migram para o agendador novo à medida que ficam livres, ou enquanto os novos trabalhadores são criados.

Desligar um agendador requer que todos os lotes no agendador tenham concluído suas atividades e sejam encerrados. Um agendador que foi encerrado é marcado como offline, de forma que nenhum lote novo seja agendado nele.

Se um agendador novo for adicionado ou removido, as tarefas permanentes do sistema, como monitor de bloqueio, ponto de verificação, thread de tarefa de sistema (processando DTC) e processo de sinal continuarão sendo executadas no agendador enquanto o servidor estiver em operação. Essas tarefas permanentes de sistema não são migradas dinamicamente. Para redistribuir a carga de processador para essas tarefas de sistema pelos agendadores, será necessário reinicializar a instância do SQL Server. Se o SQL Server tentar encerrar um agendador associado a uma tarefa permanente de sistema, a tarefa continuará sendo executada no agendador offline (sem migração). Esse agendador é associado aos processadores na máscara de afinidade modificada e não coloca nenhuma carga no processador com o qual estava associado antes da alteração. A presença de agendadores offline adicionais não deve afetar significativamente a carga do sistema. Se afetar, uma reinicialização do servidor de banco de dados será necessária para reconfigurar essas tarefas nos agendadores disponíveis com a máscara de afinidade modificada.

Não defina os valores de configuração 'affinity mask' e 'affinity I/O mask' do SQL Server para usar as mesmas CPUs. O desempenho poderá ser afetado se você optar por associar um processador para o agendamento de threads de trabalho do SQL Server e para o processamento de E/S. É necessário que os valores de configuração não sejam definidos para o mesmo processador. A mesma recomendação se aplica à 'affinity64 mask' e à 'affinity64 I/O mask'.  Para assegurar que a máscara de afinidade não se sobreponha à máscara de E/S de afinidade, o comando [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) verifica se as afinidades de CPU e E/S normais são mutuamente exclusivas. Se não forem, uma mensagem de erro será reportada à sessão do cliente e ao log de erros do SQL Server, indicando que essa configuração não é recomendada.

```sql
 Msg 5834, Level 16, State 1, Line 1
 The affinity mask specified conflicts with the IO affinity mask specified. Use the override option to force this configuration
```

A execução das opções RECONFIGURE WITH OVERRIDE permite que as afinidades de CPU e de E/S não se sobreponham e não sejam mutuamente exclusivas.  

As tarefas de afinidade de E/S (como lazy writer e log writer) são afetadas diretamente pela máscara de afinidade de E/S. Se as tarefas lazy writer e log writer não tiverem afinidade, elas seguirão as mesmas regras definidas para as outras tarefas permanentes, como lock monitor ou checkpoint.
Se você especificar uma máscara de afinidade que tenta fazer mapeamento para uma CPU inexistente, o comando RECONFIGURE reportará uma mensagem de erro à sessão do cliente e ao log de erros do SQL Server. O uso da opção RECONFIGURE WITH OVERRIDE não tem nenhum efeito nesse caso, e o mesmo erro de configuração é reportado novamente.

Você também pode excluir a atividade do SQL Server de atribuições de carga de trabalho específicas pelo sistema operacional Windows. Se você definir um bit representando um processador como 1, esse processador será selecionado pelo Mecanismo de Banco de Dados do SQL Server para atribuição de thread. Quando você define **affinity mask** como 0 (o padrão), os algoritmos de agendamento do Microsoft Windows definem a afinidade do thread. Quando você define **affinity mask** como qualquer valor diferente de zero, a afinidade do SQL Server interpreta o valor como um bitmask que especifica esses processadores qualificados para seleção.  

Ao isolar threads do SQL Server da execução em determinados processadores, o Microsoft Windows pode avaliar melhor como o sistema está controlando os processos específicos do Windows. Por exemplo, em um servidor de 8 CPUs que executa duas instâncias do SQL Server (instâncias A e B), o administrador do sistema poderia usar a opção affinity mask para atribuir o primeiro conjunto de 4 CPUs à instância A e o segundo conjunto de 4 CPUs à instância B. Para configurar mais de 32 processadores, defina affinity mask e affinity64 mask. Os valores para **máscara de afinidade** são os seguintes:

- Uma **máscara de afinidade** de um byte abrange até oito CPUs em um computador multiprocessador.

- Uma **máscara de afinidade** de dois bytes abrange até 16 CPUs em um computador multiprocessador.

- Uma **máscara de afinidade** de três bytes abrange até 24 CPUs em um computador multiprocessador.

- Uma **máscara de afinidade** de quatro bytes abrange até 32 CPUs em um computador multiprocessador.

- Para incluir mais de 32 CPUs, configure uma máscara de afinidade de 4 bytes para as primeiras 32 CPUs e uma máscara de afinidade64 de quatro bytes para as demais CPUs.

Como definir a opção de afinidade de processador do SQL Server é uma operação especializada, recomenda-se que ela só seja usada quando necessário. Na maioria dos casos, a afinidade padrão do Microsoft Windows proporciona o melhor desempenho. Considere os requisitos de CPU para outros aplicativos quando definir as máscaras de afinidade. Para obter mais informações, consulte a documentação do sistema operacional Windows.

> [!NOTE]
> Você pode usar o Windows System Monitor para exibir e analisar o uso individual de processador.

Ao especificar a opção affinity I/O mask, você precisa usá-la com a opção de configuração affinity mask. No entanto, conforme mencionado anteriormente, não habilite a mesma CPU nas opções **affinity mask** e affinity I/O mask. Os bits correspondentes em cada CPU devem estar em um destes três estados:

- 0 na opção de máscara de afinidade e na opção de máscara de afinidade de E/S.

- 1 na opção de máscara de afinidade e 0 na opção de máscara de E/S de afinidade.

- 0 na opção de máscara de afinidade e 1 na opção de máscara de E/S de afinidade.

> [!CAUTION]
> Não configure afinidade de CPU no sistema operacional Windows e também configure a máscara de afinidade no SQL Server. Essas definições estão tentando alcançar o mesmo resultado e se as configurações forem inconsistentes, você poderá ter resultados imprevisíveis. No SQL Server, a afinidade de CPU é melhor configurada com a opção sp_configure.

## <a name="example"></a>Exemplo

Como exemplo de configuração da opção de máscara de afinidade, se os processadores 1, 2 e 5 forem selecionados como disponíveis com os bits nas posições 1, 2 e 5 definidos como 1 e os bits 0, 3, 4, 6 e 7 definidos como 0, será necessário usar um valor hexadecimal de 0x26 ou o decimal equivalente de 38. Numere as posições de bits da direita para a esquerda.

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'affinity mask', 38;
RECONFIGURE;
GO
```

Esses são valores de **máscara de afinidade** para um sistema com oito CPUs.  

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

A opção de máscara de afinidade é uma opção avançada. Se você estiver usando o procedimento armazenado no sistema sp_configure para alterar a configuração, será possível alterar **affinity mask** apenas quando **show advanced options** estiver definido como 1. Após executar o comando RECONFIGURE de [!INCLUDE[tsql](../../includes/tsql-md.md)], a nova configuração terá efeito imediatamente sem a necessidade de reiniciar a instância do SQL Server.  

## <a name="non-uniform-memory-access-numa"></a>NUMA (acesso não uniforme à memória)

Ao usar hardware baseado em NUMA (acesso não uniforme à memória) com a máscara de afinidade definida, todo agendador em um nó é associado à respectiva CPU. Quando a máscara de afinidade não estiver definida, cada agendador será associado ao grupo de CPUs dentro do nó NUMA e um agendador mapeado para o nó NUMA N1 poderá agendar trabalho em qualquer CPU no nó, mas não em CPUs associadas a outro nó.  

Qualquer operação sendo executada em um único nó NUMA só poderá usar páginas de buffer daquele nó. Quando uma operação é executada paralelamente nas CPUs a partir de vários nós, a memória poderá ser usada a partir de qualquer nó envolvido.  
  
## <a name="licensing-issues"></a>Problemas de licenciamento

A afinidade dinâmica é restrita com rigor pelo licenciamento de CPU. O SQL Server não permite nenhuma configuração de opções de máscara de afinidade que viole a política de licenciamento.  

### <a name="startup"></a>Inicialização

Se uma máscara de afinidade especificada violar a política de licenciamento durante a inicialização do SQL Server ou durante a anexação do banco de dados, a camada do mecanismo concluirá o processo de inicialização ou a operação de anexação/restauração do banco de dados e depois redefinirá o valor de execução de sp_configure da máscara de afinidade como zero, emitindo uma mensagem de erro para o log de erros do SQL Server.  
  
### <a name="reconfigure"></a>Reconfigurar

Se uma máscara de afinidade especificada violar a política de licenciamento ao executar o comando RECONFIGURE do [!INCLUDE[tsql](../../includes/tsql-md.md)], uma mensagem de erro será reportada à sessão do cliente e ao log de erros do SQL Server e o administrador do banco de dados precisará reconfigurar a máscara de afinidade. Nenhum comando RECONFIGURE WITH OVERRIDE é aceito nesse caso.  

## <a name="next-steps"></a>Próximas etapas

- [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
- [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
- [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)
