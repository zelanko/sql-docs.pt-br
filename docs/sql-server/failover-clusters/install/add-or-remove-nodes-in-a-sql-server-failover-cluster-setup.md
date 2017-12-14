---
title: "Adicionar ou remover nós em um cluster de failover do SQL Server (instalação) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: failover-clusters
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding nodes
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- failover clustering [SQL Server], nodes
- deleting nodes
- cluster maintenance [SQL Server]
- removing nodes
ms.assetid: fe20dca9-a4c1-4d32-813d-42f1782dfdd3
caps.latest.revision: "49"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ad5dbfd8ad4774d1b8877f3699157908bb449592
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="add-or-remove-nodes-in-a-sql-server-failover-cluster-setup"></a>Adicionar ou remover nós em um cluster de failover do SQL Server (instalação)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use este procedimento para gerenciar nós em uma instância de cluster de failover existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Para atualizar ou remover um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , você deve ter privilégios de administrador local com permissão para fazer logon como um serviço em todos os nós do cluster de failover. Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.  
  
 Para adicionar um nó a um cluster de failover existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , é necessário executar a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no nó a ser adicionado à instância do cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Não execute a instalação no nó ativo.  
  
 Para remover um nó de um cluster de failover existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , é necessário executar a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no nó a ser removido da instância do cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Para exibir as etapas de procedimentos para adicionar ou remover nós, selecione uma das seguintes operações:  
  
-   [Adicionar um nó a um cluster de failover existente do SQL Server](#Add)  
  
-   [Remover um nó de um cluster de failover existente do SQL Server](#Remove)  
  
> [!IMPORTANT]  
>  A letra da unidade do sistema operacional para locais de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser igual em todos os nós adicionados ao cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
##  <a name="Add"></a> Adicionar nó  
  
#### <a name="to-add-a-node-to-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>Para adicionar um nó a um cluster de failover existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, na pasta raiz, clique duas vezes em Setup.exe. Para instalar a partir de um compartilhamento de rede, navegue para a pasta raiz no compartilhamento e clique duas vezes em Setup.exe.  
  
2.  O Assistente de Instalação iniciará o Centro de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para adicionar um nó a uma instância de cluster de failover existente, clique em **Instalação** no painel esquerdo. Em seguida, selecione **Adicionar nó a um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**.  
  
3.  O Verificador de Configuração do Sistema executará uma operação de descoberta no computador. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
4.  Na página de Seleção de Idioma, você pode especificar o idioma da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , se estiver instalando em um sistema operacional localizado, e se a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional. Para obter mais informações sobre suporte em qualquer idioma e considerações sobre instalação, veja [Versões de Idiomas Locais no SQL Server](../../../sql-server/install/local-language-versions-in-sql-server.md).  
  
     Para continuar, clique em **Avançar**.  
  
5.  Na página Chave do produto, especifique a chave do PID de uma versão de produção do produto. Observe que a chave do produto digitada para esta instalação deve ser para a mesma da edição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o que está instalada no nó ativo.  
  
6.  Na página Termos de Licença, leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições de licença. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Para continuar, clique em **Avançar**. Para finalizar a Instalação, clique em **Cancelar**.  
  
7.  O Verificador de Configuração do Sistema verificará o estado do sistema do computador antes da continuação da instalação. Depois de concluir a verificação, clique em **Avançar** para continuar.  
  
8.  Na página Configuração do Nó do Cluster, use a caixa suspensa para especificar o nome da instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que será modificada durante esta operação de Instalação.  
  
9. Na página Configuração do Servidor — Contas de Serviço, especifique as contas de logon para os serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Os serviços reais configurados nessa página dependem dos recursos selecionados para instalação. Para instalações de cluster de failover, as informações de nome da conta e de tipo de inicialização serão pré-populadas nesta página com base nas configurações fornecidas para o nó ativo. Você deve fornecer senhas para cada conta. Para obter mais informações, consulte [Configuração do servidor — Contas de serviço](http://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) e [Configurar contas de serviço e permissões do Windows](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     **Observação sobre segurança** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     Depois de concluir a especificação de informações de logon para serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Avançar**.  
  
10. Na página Relatório, especifique as informações que deseja enviar à [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para aperfeiçoar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por padrão, a opção de relatório de erros está habilitada.  
  
11. O Verificador de Configuração do Sistema executará mais um conjunto de regras para validar a configuração do computador com os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] especificados.  
  
12. A página Pronto para Adicionar Nó mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação.  
  
13. A página Andamento de Adicionar Nó fornece o status para que você possa monitorar o andamento da instalação à medida que ela avança.  
  
14. Após a instalação, a página Concluída fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Fechar**.  
  
15. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
##  <a name="Remove"></a> Remover nó  
  
#### <a name="to-remove-a-node-from-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>Para remover um nó de um cluster de failover existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Na pasta raiz, clique duas vezes em setup.exe. Para instalar a partir de um compartilhamento de rede, navegue para a pasta raiz no compartilhamento e clique duas vezes em Setup.exe.  
  
2.  O Assistente de Instalação inicia a Central de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para remover um nó de uma instância de cluster de failover existente, clique em **Manutenção** no painel esquerdo e selecione **Remover nó de um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**.  
  
3.  O Verificador de Configuração do Sistema executará uma operação de descoberta no computador. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
4.  Depois que você clicar na página Arquivos de Suporte à Instalação, o Verificador de Configuração do Sistema verificará o estado do sistema do seu computador antes de continuar a instalação. Depois de concluir a verificação, clique em **Avançar** para continuar.  
  
5.  Na página Configuração do Nó do Cluster, use a caixa suspensa para especificar o nome da instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que será modificada durante esta operação de Instalação. O nó que será removido será listado no campo **Nome deste nó** .  
  
6.  A página Pronto para Remover Nó exibe uma exibição de árvore das opções que foram especificadas durante a Instalação. Para continuar, clique em **Remover**.  
  
7.  Durante a operação de remoção, a página Andamento da Remoção de Nó fornece o status.  
  
8.  A página Concluída fornece um link para o arquivo de log de resumo da operação de remoção de nó e outras observações importantes. Para concluir a remoção de nó do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Fechar**. Para obter mais informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
