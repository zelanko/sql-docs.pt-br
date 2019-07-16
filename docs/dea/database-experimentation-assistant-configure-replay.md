---
title: Configurar reprodução no Assistente de experimentação do banco de dados para upgrades do SQL Server
description: Configurar a reprodução no Assistente de experimentação do banco de dados
ms.custom: ''
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
ms.openlocfilehash: 9166265dad077d4a3e83cc300868607d001ef233
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058968"
---
# <a name="configure-replay-in-database-experimentation-assistant"></a>Configurar a reprodução no Assistente de experimentação do banco de dados

Assistente de experimentação de banco de dados (DEA) usa as ferramentas de instalação do SQL Server Distributed Replay para reproduzir um rastreamento capturado em um ambiente de teste atualizado. É recomendável fazer um teste usando um arquivo de rastreamento pequenos antes de fazer uma reprodução completa para garantir que reprodução adequada das consultas.

## <a name="distributed-replay-requirements"></a>Requisitos de reprodução distribuídos

- Um adicional 78% de espaço em disco rígido é necessário para criar arquivos IRF no computador do controlador do Distributed Replay.
- 200 MB ou 512 MB é o tamanho de substituição de rastreamento ideal para usar para capturar rastreamentos de desempenho ou de produção.   
- Os requisitos mínimos de CPU e RAM para as máquinas de controlador e cliente do Distributed Replay são uma CPU de núcleo único com 3,5 GB de RAM.
- A hora da reprodução leva aproximadamente 1.55 vezes mais do que o tempo de captura, como um controlador e quatro máquinas filho são usadas para reproduzir o rastreamento de produção.
- Se você usar nossas versões "publicadas" de produção e arquivos de definição de rastreamento de desempenho e os filtros de definição de rastreamento de desempenho horizontalmente os rastreamentos para um banco de dados de interesse, análise mostra que o **rastreamento de desempenho** é de tamanho cerca de 15 vezes maior do que o **rastreamento de produção** tamanho.

## <a name="set-up-a-virtual-network-or-domain"></a>Configurar uma rede virtual ou o domínio

Distributed Replay exige que você use contas comuns entre as máquinas. Devido a esse requisito e por motivos de segurança, recomendamos a execução de Distributed Replay em uma rede virtual ou em uma rede controlado por domínio:

- Crie o controlador e cliente máquinas no ambiente.
- Certifique-se de que as máquinas de controlador e cliente podem executar ping entre si pela rede.
- Máquinas de clientes de reprodução distribuídas devem ter conectividade com o computador de destino da reprodução executando o SQL Server.

## <a name="set-up-the-controller-service"></a>Configurar o serviço do controlador

Para configurar o serviço do controlador:

1. Instale o controlador do Distributed Replay usando o instalador do SQL Server. Se você tiver ignorado a etapa do Assistente de instalador do SQL Server que configura o controlador do Distributed Replay, você pode configurar o controlador por meio do arquivo de configuração. Em uma instalação típica, o arquivo de configuração está localizado em C:\Program Files (x86) \Microsoft SQL Server\<versão\>\Tools\DReplayController\DReplayController.config.
1. Logs do controlador de reprodução distribuídos estão localizados em \Microsoft SQL Server do C:\Program Files (x86)\<versão\>\Tools\DReplayController\Log.
1. Abra Services. msc e vá para o **SQL Server Distributed Replay Controller** service.
1. Clique com botão direito no serviço e, em seguida, selecione **propriedades**. Defina a conta de serviço para uma conta que é comum para as máquinas de controlador e cliente na rede.
1. Selecione **Okey** para fechar o **propriedades** janela.
1. Reinicie o **SQL Server Distributed Replay Controller** serviço em Services. msc. Você também pode executar os comandos a seguir na linha de comando para reiniciar o serviço:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`
1. Para obter mais opções de configuração, consulte [configurar o Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="configure-dcom"></a>Configurar o DCOM

Essa configuração é necessária apenas no computador controlador.

1. Abra dcomcnfg.exe.
1. Expandir **serviços de componentes** > **computadores** > **meu computador** > **DCOM Config**.
1. Sob **configuração de DCOM**, clique com botão direito **DReplayController**e, em seguida, selecione **propriedades**.
1. Selecione a guia **Segurança** .
1. Sob **permissões de inicialização e ativação**, selecione **personalizar**e, em seguida, selecione **editar**.
1. Adicione o usuário que será iniciar a reprodução. Dar ao usuário permissões de inicialização Local e Ativação Local. Se o usuário planeja iniciar ou ativar remotamente, dê ao usuário permissões de inicialização remota e ativação remota.
1. Selecione **Okey** para confirmar as alterações e retornar para o **segurança** guia.
1. Sob **permissões de acesso**, selecione **personalizar**e, em seguida, selecione **editar**.
1. Adicione o usuário que será iniciar a reprodução. Conceda ao usuário permissões de acesso Local. Se o usuário planos para acessar o serviço de controlador remotamente, dar ao usuário permissões de acesso remoto.
1. Selecione **Okey** para confirmar as alterações e retornar para o **segurança** guia.
1. Selecione **Okey** para confirmar as alterações.
1. Reinicie o serviço SQL Server Distributed Replay Controller em Services. msc. Você também pode executar os comandos a seguir na linha de comando para reiniciar o serviço:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>Configurar o serviço de cliente

Antes de configurar o serviço do cliente, use as ferramentas de rede, como o ping para verificar se as máquinas de controlador e cliente podem se comunicar.

1. Instale o cliente do Distributed Replay usando o instalador do SQL Server.
1. Abra Services. msc e vá para o serviço do SQL Server Distributed Replay Client.
1. Clique com botão direito no serviço e, em seguida, selecione **propriedades**. Defina a conta de serviço para uma conta que é comum para máquinas de controlador e o cliente na rede.
1. Selecione **Okey** para fechar o **propriedades** janela. Se você tiver ignorado a etapa do Assistente do instalador do SQL Server para configurar o cliente do Distributed Replay, você pode configurá-lo por meio do arquivo de configuração. Em uma instalação típica, o arquivo de configuração está localizado em C:\Program Files (x86) \Microsoft SQL Server\<versão\>\Tools\DReplayClient\DReplayClient.config.
1. Certifique-se de que o arquivo dreplayclient. config contém o nome do computador do controlador de como seu controlador para o registro.
1.  Reinicie o serviço SQL Server Distributed Replay Client em Services. msc. Você também pode executar os comandos a seguir na linha de comando para reiniciar o serviço:<br/>
    `NET STOP "SQL Server Distributed Replay Client"`<br/>
    `NET START "SQL Server Distributed Replay Client"`
1. Logs do controlador de reprodução distribuídos estão localizados em \Microsoft SQL Server do C:\Program Files (x86)\<versão\>\Tools\DReplayClient\Log. Os logs indicam se o cliente pode se registrar com o controlador.
1. Se a configuração for bem-sucedida, o log exibirá a mensagem "registrado com o controlador de < nome do controlador\>".
1. Para obter mais opções de configuração, consulte [configurar o Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="set-up-distributed-replay-administration-tools"></a>Configurar ferramentas de administração do Distributed Replay

Você pode usar as ferramentas de administração do Distributed Replay para testar rapidamente se o Distributed Replay está funcionando corretamente no ambiente. Testando a configuração pode ser especialmente útil em um ambiente em que várias máquinas de cliente são registradas em um controlador. Talvez você precise instalar o SQL Server Management Studio (SSMS) para obter as ferramentas de administração.

1. Vá para o SSMS local de instalação e procure o Distributed Replay administration ferramenta dreplay.exe e seus componentes dependentes.
1. Abra uma janela de Prompt de comando e execute `dreplay.exe status -f 1`.
1. Se todas as etapas anteriores forem bem-sucedidas, a saída do console indica que o controlador pode ver seus clientes em um `READY` estado.

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>Configurar o firewall para acesso remoto do Distributed Replay

Acessar remotamente o Distributed Replay requer a abertura de portas que são visíveis no domínio ou na rede virtual.

1. Abra **Firewall do Windows** com **segurança avançada**.
1. Vá para **regras de entrada**.
1. Criar uma nova regra de firewall de entrada para o programa C:\Program Files (x86) \Microsoft SQL Server\<versão\>\Tools\DReplayController\DReplayController.exe.
1. Permita o acesso de nível de domínio para todas as portas para DReplayController.exe ser capaz de se comunicar com o serviço de controlador remotamente.
1. Salve a regra.

## <a name="set-up-target-computers"></a>Configurar os computadores de destino

Reprodução dois dos é necessários para executar um A / teste de B ou de um experimento. Ou seja, duas instâncias separadas de instalações do SQL Server talvez seja necessário para um cenário de migração. 

Você também pode instalar as duas versões das instâncias do SQL Server no mesmo computador. Uma advertência é certificar-se de que as instâncias são completamente isoladas quando uma reprodução está em andamento.

As etapas a seguir devem ser executadas para cada reprodução:

1. Restaure o backup do banco de dados.
1. Forneça permissões para o usuário de conta de serviço do cliente acessar os bancos de dados na instância do SQL Server. Permissões são necessárias para as consultas para ser executado na instância do SQL Server.
1. Inicie a reprodução.

## <a name="next-steps"></a>Próximas etapas

- Para saber como repetir um rastreamento capturado em um ambiente de teste atualizada, consulte [repetir rastreamento](database-experimentation-assistant-replay-trace.md).

- Para obter uma introdução 19 minutos DEA e demonstração, assista ao vídeo a seguir:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
