---
title: Atualizar para outra edição do SQL Server 2014 (instalação) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 31d16820-d126-4c57-82cc-27701e4091bc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6b0b77ad5bb11b659e9f68eb7ff219b7844ad252
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774570"
---
# <a name="upgrade-to-a-different-edition-of-sql-server-2014-setup"></a>Atualizar para outra edição do SQL Server 2014 (instalação)
  A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à atualização de edição entre várias edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter informações sobre os caminhos de atualização de edição com suporte, consulte [Atualizações de versão e edição com suporte](supported-version-and-edition-upgrades.md). Antes de você iniciar a atualização de edição de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], revise os tópicos seguintes:  
  
-   [Recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
-   [Edições e componentes do SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md)  
  
-   [Computar limites de capacidade por edição do SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
-   [Requisitos de hardware e software para a instalação do SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
> [!NOTE]  
>  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente clusterizado:** Executar a atualização de edição em um de nós do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cluster é suficiente. Esse nó pode ser ativo ou passivo, e o mecanismo não aciona os recursos offline durante a atualização da edição. Após a atualização da edição, será necessário reiniciar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou executar o failover em um nó diferente.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura no compartilhamento remoto.  
  
> [!IMPORTANT]  
>  Para que a alteração de edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja ativada, você deve reiniciar os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso resulta em tempo de inatividade do aplicativo enquanto os serviços estiverem offline.  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="to-upgrade-to-a-different-edition-of-includesscurrentincludessscurrent-mdmd"></a>Para atualizar para outra edição do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Na pasta raiz, clique duas vezes em setup.exe ou inicie a Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em Ferramentas de Configuração. Para instalar a partir de um compartilhamento de rede, localize a pasta raiz no compartilhamento e clique duas vezes em Setup.exe.  
  
2.  Para atualizar uma instância existente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para uma edição diferente, na Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Manutenção**e selecione **Atualização de Edição**.  
  
3.  Se os arquivos de suporte à Instalação forem necessários, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os instalará. Se você for instruído a reiniciar o computador, reinicie-o antes de continuar.  
  
4.  O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, clique em **OK**.  
  
5.  Na página Chave do Produto, selecione um botão de opção para indicar se você está atualizando para uma edição gratuita do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou se tem uma chave de PID para uma versão de produção do produto. Para obter mais informações, consulte [edições e componentes do SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) e [Supported Version and Edition Upgrades](supported-version-and-edition-upgrades.md).  
  
6.  Na página Termos de Licença, leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições de licença. Para continuar, clique em **Avançar**. Para finalizar a Instalação, clique em **Cancelar**.  
  
7.  Na página Selecionar Instância, especifique a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser atualizada.  
  
8.  A página Regras de Atualização de Edição valida a configuração do computador antes da operação de atualização de edição começar.  
  
9. A página Pronto para Atualizar a Edição mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Atualizar**.  
  
10. Durante o processo de atualização de edição, os serviços precisam ser reiniciados para selecionar a nova configuração. Depois da atualização de edição, a página Concluída fornece um link para o arquivo de log de resumo da atualização de edição. Para fechar o assistente, clique em **Fechar**.  
  
11. A página Concluída fornece um link para o arquivo de log de resumo da instalação e outras observações importantes.  
  
12. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](view-and-read-sql-server-setup-log-files.md).  
  
13. Se você atualizou a partir do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], deverá executar etapas adicionais antes de usar a instância atualizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   Habilite o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Windows SCM.  
  
    -   Provisione a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
 Além das etapas anteriores, pode ser necessário fazer o seguinte se você atualizou a partir do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]:  
  
-   Os usuários que foram provisionados no [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] permanecem provisionados após a atualização. Especificamente, o grupo BUILTIN\Users permanece provisionado. Desabilite, remova ou provisione essas contas novamente, conforme necessário. Para obter mais informações, veja [Configurar contas de serviço e permissões do Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
-   Os tamanhos e o modo de recuperação para os bancos de dados de sistemas model e tempdb permanecem inalterados após a atualização. Reconfigure essas configurações, conforme necessário. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
-   Os bancos de dados modelo permanecem no computador após a atualização.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar para o SQL Server 2014](upgrade-sql-server.md)   
 [Compatibilidade com versões anteriores](../../getting-started/backward-compatibility.md)  
  
  
