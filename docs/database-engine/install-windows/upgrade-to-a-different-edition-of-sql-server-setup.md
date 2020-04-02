---
title: Fazer upgrade para outra edição
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 31d16820-d126-4c57-82cc-27701e4091bc
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: c3de07aaa65e2dac2859aaf5c0be3e63e0f22dcf
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79434123"
---
# <a name="upgrade-to-a-different-edition-of-sql-server-setup"></a>Fazer upgrade para outra edição do SQL Server (Instalação)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à atualização de edição entre várias edições do [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)]. Para obter informações sobre os caminhos de atualização de edição com suporte, consulte [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades-2017.md). Antes de você iniciar a atualização de edição de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], examine os seguintes artigos:  

- [Edições e recursos com suporte do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)  
- [Edições e recursos com suporte do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)  
- [Computar limites de capacidade por edição do SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
- [Requisitos de Hardware e Software para a Instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
> [!NOTE]  
> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância de cluster de failover:** executar a atualização da edição em um de nós da instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é suficiente. Esse nó pode ser ativo ou passivo e o mecanismo não coloca os recursos offline durante o upgrade da edição. Após a atualização da edição, será necessário reiniciar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou executar o failover em um nó diferente.  
  
## <a name="prerequisites"></a>Pré-requisitos  
Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura no compartilhamento remoto.  
  
> [!IMPORTANT]  
> Para que a alteração de edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja ativada, você deve reiniciar os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso resulta em tempo de inatividade do aplicativo enquanto os serviços estiverem offline.  
  
## <a name="procedure"></a>Procedimento  
  
### <a name="to-upgrade-to-a-different-edition-of-ssnoversion"></a>Para atualizar para outra edição do [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)]  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Na pasta raiz, clique duas vezes em setup.exe ou inicie a Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em Ferramentas de Configuração. Para instalar a partir de um compartilhamento de rede, localize a pasta raiz no compartilhamento e clique duas vezes em Setup.exe.  
  
2.  Para atualizar uma instância existente do [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] para uma edição diferente, na Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Manutenção**e selecione **Atualização de Edição**.  
  
3.  Se os arquivos de suporte à Instalação forem necessários, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os instalará. Se você for instruído a reiniciar o computador, reinicie-o antes de continuar.  
  
4.  O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, clique em **OK**.  
  
5.  Na página Chave do Produto, selecione um botão de opção para indicar se você está atualizando para uma edição gratuita do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou se tem uma chave de PID para uma versão de produção do produto. Para obter mais informações, consulte [Edições e componentes do SQL Server](../../sql-server/editions-and-components-of-sql-server-2017.md) e [Upgrades de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
6.  Na página Termos de Licença, leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições de licença. Para continuar, clique em **Avançar**. Para finalizar a Instalação, clique em **Cancelar**.  
  
7.  Na página Selecionar Instância, especifique a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser atualizada.  
  
8.  A página Regras de Atualização de Edição valida a configuração do computador antes da operação de atualização de edição começar.  
  
9. A página Pronto para Atualizar a Edição mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Atualizar**.  
  
10. Durante o processo de atualização de edição, os serviços precisam ser reiniciados para selecionar a nova configuração. Depois da atualização de edição, a página Concluída fornece um link para o arquivo de log de resumo da atualização de edição. Para fechar o assistente, clique em **Fechar**.  
  
11. A página Concluída fornece um link para o arquivo de log de resumo da instalação e outras observações importantes.  
  
12. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
13. Se você atualizou a partir do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], deverá executar etapas adicionais antes de usar a instância atualizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   Habilite o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Windows SCM.  
  
    -   Provisione a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
 Além das etapas anteriores, pode ser necessário fazer o seguinte se você atualizou a partir do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]:  
  
-   Os usuários que foram provisionados no [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] permanecem provisionados após a atualização. Especificamente, o grupo BUILTIN\Users permanece provisionado. Desabilite, remova ou provisione essas contas novamente, conforme necessário. Para obter mais informações, consulte [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
-   Os tamanhos e o modo de recuperação para os bancos de dados de sistemas model e tempdb permanecem inalterados após a atualização. Reconfigure essas configurações, conforme necessário. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
-   Os bancos de dados modelo permanecem no computador após a atualização.  

> [!NOTE]  
> Se o procedimento falhar na regra Engine_SqlEngineHealthCheck, você poderá usar a opção de instalação de linha de comando para ignorar essa regra específica e permitir que o processo de atualização seja concluído com êxito. Para ignorar a verificação desta regra, abra um prompt de comando e altere para o caminho que contém a Configuração do SQL Server (Setup.exe). Em seguida, digite o seguinte comando: 

```console
setup.exe /q /ACTION=editionupgrade /InstanceName=MSSQLSERVER /PID=<appropriatePid> /SkipRules=Engine_SqlEngineHealthCheck
```


## <a name="see-also"></a>Consulte Também  
 [Fazer upgrade do SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)   
 [Compatibilidade com versões anteriores_excluída](https://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)  
  
  
