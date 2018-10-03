---
title: Instalar o Distributed Replay (instalação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 64479cdc-661a-4e32-a381-8f8b5a238337
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0f9d81920e9e14dc745813795bcf98eb1d9ebdf9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051387"
---
# <a name="install-distributed-replay-setup"></a>Instalar o Distributed Replay (instalação)
  Instale os recursos do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay com o Assistente de Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Ao planejar onde instalar os recursos, considere o seguinte:  
  
-   Você pode instalar a ferramenta de administração no mesmo computador que o controlador do Distributed Replay ou em computadores diferentes.  
  
-   Pode haver apenas um controlador em cada ambiente do Distributed Replay.  
  
-   Você pode instalar o serviço de cliente em até 16 computadores (físicos ou virtuais).  
  
-   Apenas uma instância do serviço de cliente pode ser instalada no computador do controlador do Distributed Replay. Se o ambiente do seu Distributed Replay tiver mais de um cliente, não é recomendável instalar o serviço de cliente no mesmo computador que o controlador. Fazer assim pode reduzir a velocidade global de Distributed Replay.  
  
-   Para cenários de teste de desempenho, não é recomendável instalar a ferramenta de administração, o serviço de controlador do Distributed Replay ou serviço de cliente na instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A instalação de todos esses recursos no servidor de destino deve ser limitada a testes funcionais de compatibilidade de aplicativos.  
  
-   Depois da instalação, o serviço de controlador, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller, deve estar em execução antes de você iniciar o serviço de cliente do Distributed Replay nos clientes.  
  
> [!NOTE]  
>  Para remover ou alterar os recursos do Distributed Replay, use a janela **Programas e Recursos** do Windows no **Painel de Controle**. Selecione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] na janela **Desinstalar ou alterar um programa** e clique em **Remover** para abrir o Assistente de Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Na página **Selecionar Recursos** , marque os recursos do Distributed Replay que você deseja remover.  
  
 **Pré-requisitos:**  
  
-   Verifique se os computadores que você deseja usar atendem aos requisitos descritos no tópico [Requisitos do Distributed Replay](../../tools/sql-server-profiler/replay-requirements.md).  
  
-   Antes de começar este procedimento, você cria as contas de usuário de domínio com as quais os serviços de controlador e de cliente serão executados. É recomendável que essas contas não sejam membros do grupo Administradores do Windows. Para obter mais informações, veja a seção Contas de usuário e serviço no tópico [Segurança do Distributed Replay](../../tools/distributed-replay/distributed-replay-security.md) .  
  
    > [!NOTE]  
    >  É possível usar contas de usuários locais se você estiver executando a ferramenta de administração, o serviço de controlador e o serviço de cliente no mesmo computador.  
  
 **Locais de instalação:**  
  
 Supondo que você use os locais de arquivo padrão e uma instalação padrão, o diretório base estará localizado em C:\Arquivos de Programas\Microsoft SQL Server. Dentro dele, os binários e assemblies são instalados nos seguintes locais:  
  
-   Em um sistema de 32 bits:  
  
     [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Ferramentas  
  
     \- OU –  
  
     \<Diretório de Recursos Compartilhados>\Tools\\(diretório de recursos compartilhados alternativo fornecido pelo usuário)  
  
-   Em um sistema de 64 bits:  
  
     C:\Program Files\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86) \120\Tools  
  
     \- OU –  
  
     \<Diretório de Recursos Compartilhados (x86)>\Tools\\(diretório de recursos compartilhados [x86] alternativo fornecido pelo usuário)  
  
### <a name="to-install-distributed-replay-features"></a>Para instalar recursos do Distributed Replay  
  
1.  Para iniciar a instalação de qualquer um dos recursos do Distributed Replay, inicie o Assistente de Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
2.  A página **Regras de Suporte à Instalação** identifica problemas que podem ocorrer ao instalar os arquivos de suporte da Instalação do SQL Server. Você deve corrigir qualquer falha de suporte à Instalação antes de continuá-la.  
  
3.  Na página **Chave do Produto (Product Key)** , selecione um botão de opção para indicar se você está instalando uma edição gratuita do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou uma versão de produção do produto que tem uma chave de PID. Para obter mais informações, consulte [edições e componentes do SQL Server 2014](../editions-and-components-of-sql-server-2016.md).  
  
4.  Na página **Termos de Licença** , leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições da licença. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  Na página **Arquivos de Suporte à Instalação**, clique em **Instalar** para instalar ou atualizar os arquivos de Suporte à Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
6.  Na página **Função de Instalação**, selecione **Instalação de Recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** e clique em **Avançar** para continuar para a página **Seleção de Recursos**.  
  
7.  Na página **Seleção de Recursos**, configure quais recursos você deseja instalar.  
  
    -   Para instalar a ferramenta de administração, selecione **Ferramentas de Gerenciamento – Básicas**.  
  
    -   Para instalar o serviço do controlador, selecione **Distributed Replay Controller**.  
  
    -   Para instalar o serviço do cliente, selecione **Distributed Replay Client**.  
  
     **Importante**: Quando você configura o controlador Distributed Replay, pode especificar uma ou mais contas de usuário que serão usadas para executar os serviços de cliente do Distributed Replay. Esta é a lista das contas com suporte:  
  
    -   Conta de usuário do domínio  
  
    -   Conta de usuário local criada pelo usuário  
  
    -   Administrador  
  
    -   Conta virtual e MSA (Conta de Serviço Gerenciada)  
  
    -   Serviços de rede, serviços locais e sistema  
  
     Não são aceitas contas de grupo (local ou domínio) e outras contas internas (como Todos).  
  
8.  Opcionalmente, clique no botão de reticências (...) para alterar o caminho do diretório de recursos compartilhados.  
  
    1.  Em computadores de 32 bits, o caminho de instalação padrão é **C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
    2.  Em computadores de 64 bits, o caminho de instalação padrão é **C:\Arquivos de Programas (x86)\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
9. Ao concluir, clique em **Avançar**.  
  
10. Na página **Regras de Instalação** , a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida sua configuração de computador. Quando o processo de validação for concluído, clique em **Avançar**.  
  
11. A página **Requisitos de Espaço em Disco** calcula o espaço em disco necessário para os recursos especificados. Em seguida, ele compara o espaço necessário com o espaço em disco disponível.  
  
12. Na página **Relatório de Erros** , especifique as informações que deseja enviar à [!INCLUDE[msCoName](../../includes/msconame-md.md)] para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, a opção de relatório de erros está habilitada.  
  
13. Na página **Regras de Configuração da Instalação** , o Verificador de Configuração do Sistema executará mais um conjunto de regras para validar a configuração do seu computador com os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você especificou.  
  
14. Na página **Pronto para Instalar o Programa** , clique em **Instalar**.  
  
    > [!IMPORTANT]  
    >  Depois de instalar o Distributed Replay, crie regras de firewall no controlador e nos computadores cliente e conceda permissões a cada computador cliente no servidor de destino. Para obter mais informações, veja [Concluir as etapas de pós-instalação](../../tools/distributed-replay/complete-the-post-installation-steps.md).  
  
 Estes tópicos adicionais documentam outras maneiras de instalar o Distributed Replay:  
  
-   [Instalar o Distributed Replay usando o prompt de comando](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
-   [Instalar o Distributed Replay usando um arquivo de configuração](../../../2014/sql-server/install/install-distributed-replay-using-a-configuration-file.md)  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Você deve ter permissões administrativas para instalar qualquer recurso do Distributed Replay. Apenas um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenha permissões sysadmin pode adicionar as contas de serviço de cliente à função de servidor sysadmin do servidor de teste. Para obter mais informações sobre as considerações de segurança do Distributed Replay, veja [Segurança do Distributed Replay](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Requisitos do Distributed Replay](../../tools/sql-server-profiler/replay-requirements.md)   
 [Opções de linha de comando da ferramenta de administração &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [Configurar o Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
