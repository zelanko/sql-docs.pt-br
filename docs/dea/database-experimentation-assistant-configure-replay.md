---
title: Configurar a reprodução para atualizações de SQL Server
description: Configurar reprodução em Assistente para Experimentos de Banco de Dados
ms.custom: seo-lt-2019
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: b58233e40e27908f0bc8b03a95455216de2c119c
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056720"
---
# <a name="configure-replay-in-database-experimentation-assistant"></a>Configurar reprodução em Assistente para Experimentos de Banco de Dados

Assistente para Experimentos de Banco de Dados (DEA) usa as ferramentas de Distributed Replay da instalação do SQL Server para reproduzir um rastreamento capturado em um ambiente de teste atualizado. É recomendável fazer uma execução de teste usando um pequeno arquivo de rastreamento antes de fazer uma repetição completa para garantir a reprodução adequada de consultas.

## <a name="distributed-replay-requirements"></a>Requisitos de Distributed Replay

- Um adicional de 78% do espaço na unidade de disco rígido é necessário para criar arquivos IRF no computador do controlador de Distributed Replay.
- 200 MB ou 512 MB é o tamanho de substituição de rastreamento ideal a ser usado para capturar rastreamentos de produção ou de desempenho.   
- Os requisitos mínimos de CPU e RAM para o controlador de Distributed Replay e os computadores cliente são uma CPU de núcleo único com 3,5 GB de RAM.
- O tempo de reprodução leva aproximadamente 1,55 vezes mais do que o tempo de captura porque um controlador e quatro computadores filho são usados para reproduzir o rastreamento de produção.
- Se você usar nossas versões "publicadas" dos arquivos de definição de rastreamento de desempenho e de produção e a definição de rastreamento de desempenho filtrar os rastreamentos de um banco de dados de interesse, a análise mostrará que o tamanho do **rastreamento de desempenho** é de aproximadamente 15 vezes maior do que o tamanho do **rastreamento de produção** .

## <a name="set-up-a-virtual-network-or-domain"></a>Configurar uma rede virtual ou um domínio

Distributed Replay exige que você use contas comuns entre computadores. Por causa desse requisito e por motivos de segurança, é recomendável executar Distributed Replay em uma rede virtual ou em uma rede controlada por domínio:

- Crie o controlador e os computadores cliente no ambiente.
- Verifique se o controlador e os computadores cliente podem executar ping uns aos outros pela rede.
- Distributed Replay computadores cliente devem ter conectividade com o computador de destino de reprodução em execução SQL Server.

## <a name="set-up-the-controller-service"></a>Configurar o serviço do controlador

Para configurar o serviço do controlador:

1. Instale o controlador de Distributed Replay usando o instalador do SQL Server. Se você tiver ignorado a etapa do assistente do SQL Server Installer que configura o controlador de Distributed Replay, poderá configurar o controlador por meio do arquivo de configuração. Em uma instalação típica, o arquivo de configuração está localizado em C:\Arquivos de programas (x86) \Microsoft SQL Server\<versão\>\Tools\DReplayController\DReplayController.config.
1. Os logs do controlador Distributed Replay estão localizados em C:\Program Files (x86) \Microsoft SQL Server\<versão\>\Tools\DReplayController\Log.
1. Abra Services. msc e vá para o **SQL Server Distributed Replay** serviço do controlador.
1. Clique com o botão direito do mouse no serviço e selecione **Propriedades**. Defina a conta de serviço como uma conta que seja comum para o controlador e os computadores cliente na rede.
1. Selecione **OK** para fechar a janela **Propriedades** .
1. Reinicie o **SQL Server Distributed Replay** serviço do controlador a partir de Services. msc. Você também pode executar os seguintes comandos na linha de comando para reiniciar o serviço:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`
1. Para obter mais opções de configuração, consulte [configurar Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="configure-dcom"></a>Configurar DCOM

Essa configuração é necessária somente no computador do controlador.

1. Abra dcomcnfg. exe.
1. Expanda **serviços de componentes** > **computadores** > **meu computador** > **Configuração DCOM**.
1. Em **configuração do DCOM**, clique com o botão direito do mouse em **DReplayController**e selecione **Propriedades**.
1. Selecione a guia **Segurança** .
1. Em **permissões de inicialização e ativação**, selecione **Personalizar**e, em seguida, selecione **Editar**.
1. Adicione o usuário que iniciará a reprodução. Forneça as permissões de inicialização local do usuário e ativação local. Se o usuário planeja iniciar ou ativar remotamente, conceda ao usuário permissões de inicialização remota e ativação remota.
1. Selecione **OK** para confirmar as alterações e retornar à guia **segurança** .
1. Em **permissões de acesso**, selecione **Personalizar**e, em seguida, selecione **Editar**.
1. Adicione o usuário que iniciará a reprodução. Conceda permissões de acesso local ao usuário. Se o usuário planeja acessar o serviço do controlador remotamente, conceda ao usuário permissões de acesso remoto.
1. Selecione **OK** para confirmar as alterações e retornar à guia **segurança** .
1. Selecione **OK** para confirmar as alterações.
1. Reinicie o SQL Server Distributed Replay serviço do controlador a partir de Services. msc. Você também pode executar os seguintes comandos na linha de comando para reiniciar o serviço:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>Configurar o serviço do cliente

Antes de configurar o serviço do cliente, use as ferramentas de rede como ping para verificar se os computadores do controlador e do cliente podem se comunicar.

1. Instale o cliente do Distributed Replay usando o instalador do SQL Server.
1. Abra Services. msc e vá para o SQL Server Distributed Replay serviço de cliente.
1. Clique com o botão direito do mouse no serviço e selecione **Propriedades**. Defina a conta de serviço para uma conta que seja comum tanto para os computadores do controlador quanto do cliente na rede.
1. Selecione **OK** para fechar a janela **Propriedades** . Se você tiver ignorado a etapa do assistente do SQL Server Installer para configurar o cliente do Distributed Replay, você poderá configurá-lo por meio do arquivo de configuração. Em uma instalação típica, o arquivo de configuração está localizado em C:\Arquivos de programas (x86) \Microsoft SQL Server\<versão\>\Tools\DReplayClient\DReplayClient.config.
1. Verifique se o arquivo DReplayClient. config contém o nome do computador do controlador como seu controlador para registro.
1.  Reinicie o SQL Server Distributed Replay serviço de cliente do Services. msc. Você também pode executar os seguintes comandos na linha de comando para reiniciar o serviço:<br/>
    `NET STOP "SQL Server Distributed Replay Client"`<br/>
    `NET START "SQL Server Distributed Replay Client"`
1. Os logs do controlador Distributed Replay estão localizados em C:\Program Files (x86) \Microsoft SQL Server\<versão\>\Tools\DReplayClient\Log. Os logs indicam se o cliente pode se registrar no controlador.
1. Se a configuração for bem-sucedida, o log exibirá a mensagem "registrado com o nome do controlador de < do controlador\>".
1. Para obter mais opções de configuração, consulte [configurar Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="set-up-distributed-replay-administration-tools"></a>Configurar ferramentas de administração de Distributed Replay

Você pode usar as ferramentas de administração do Distributed Replay para testar rapidamente se Distributed Replay está funcionando corretamente no ambiente. O teste da configuração pode ser especialmente útil em um ambiente no qual vários computadores cliente são registrados com um controlador. Talvez seja necessário instalar o SQL Server Management Studio (SSMS) para obter as ferramentas de administração.

1. Vá para o local de instalação do SSMS e procure a ferramenta de administração do Distributed Replay dreplay. exe e seus componentes dependentes.
1. Abra uma janela de prompt de comando e execute `dreplay.exe status -f 1`.
1. Se todas as etapas anteriores forem bem-sucedidas, a saída do console indicará que o controlador pode ver seus clientes em um estado de `READY`.

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>Configurar o firewall para acesso de Distributed Replay remoto

O acesso remoto Distributed Replay requer a abertura de portas visíveis no domínio ou na rede virtual.

1. Abra o **Firewall do Windows** com **segurança avançada**.
1. Vá para **regras de entrada**.
1. Crie uma nova regra de firewall de entrada para o programa C:\Program Files (x86) \Microsoft SQL Server\<versão\>\Tools\DReplayController\DReplayController.exe.
1. Permita o acesso em nível de domínio a todas as portas para que o DReplayController. exe possa se comunicar com o serviço do controlador remotamente.
1. Salve a regra.

## <a name="set-up-target-computers"></a>Configurar computadores de destino

Duas repetições são necessárias para executar um teste A/B ou um experimento. Ou seja, você pode precisar de duas instâncias separadas de instalações de SQL Server para um cenário de migração. 

Você também pode instalar as duas versões do SQL Server instâncias no mesmo computador. Uma limitação é garantir que as instâncias sejam completamente isoladas quando uma reprodução estiver em andamento.

As etapas a seguir devem ser executadas para cada repetição:

1. Restaure o backup do banco de dados.
1. Forneça permissões para que o usuário da conta de serviço do cliente acesse os bancos de dados na instância do SQL Server. As permissões são necessárias para que as consultas sejam executadas na instância de SQL Server.
1. Inicie a reprodução.

## <a name="next-steps"></a>Próximas etapas

- Para saber como reproduzir um rastreamento capturado em um ambiente de teste atualizado, consulte [reproduzir rastreamento](database-experimentation-assistant-replay-trace.md).

- Para uma introdução de 19 minutos ao DEA e à demonstração, Assista ao vídeo a seguir:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
