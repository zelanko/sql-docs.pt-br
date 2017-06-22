---
title: "Solução de problemas de cluster de failover | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/21/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- troublshooting, failover clustering
- failover clustering, troubleshooting
- cluster troubleshooting
ms.assetid: 84012320-5a7b-45b0-8feb-325bf0e21324
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0cc4118a2cfc722ad89ca4b66a6afe403c2967d4
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="failover-cluster-troubleshooting"></a>Diagnóstico e solução de problemas do cluster de failover
  Este tópico contém informações sobre os seguintes problemas:  
  
-   Etapas básicas da solução de problemas.  
  
-   Recuperando-se de uma falha no cluster de failover.  
  
-   Resolvendo os problemas mais comuns de clustering de failover.  
  
-   Usando procedimentos armazenados estendidos e objetos COM.  
  
## <a name="basic-troubleshooting-steps"></a>Etapas básicas da solução de problemas  
 A primeira etapa de diagnóstico é executar uma verificação da validação de cluster atualizado. Para obter detalhes sobre a validação, confira [Guia passo a passo do cluster de failover: validando o hardware para um cluster de failover](https://technet.microsoft.com/library/cc732035.aspx).  Isso pode ser concluído sem qualquer interrupção do serviço, pois não afeta nenhum recurso de cluster online. A validação pode ser executada a qualquer momento após a instalação do recurso de Clustering de Failover, incluindo antes da implantação do cluster, durante a criação do cluster e enquanto o cluster está em execução. Na verdade, outros testes são executados enquanto o cluster estiver em uso, verificando se as práticas recomendadas estão sendo seguidas para cargas de trabalho altamente disponíveis. Entre esses dezenas de testes, apenas alguns deles afetarão as cargas de trabalho de cluster em execução, e todos estão dentro da categoria de armazenamento, portanto, ignorar esta categoria inteira é uma maneira fácil de evitar interrupções de testes.  
O Clustering de Failover vem com uma proteção interna para evitar o tempo de inatividade acidental durante a execução de testes de armazenamento durante a validação. Se o cluster tiver grupos online quando a validação for iniciada, e os testes de armazenamento permanecerem selecionados, ele solicitará a confirmação do usuário para a execução de todos os testes (e causar o tempo de inatividade), ou para ignorar o teste nos discos de quaisquer grupos online a fim de evitar o tempo de inatividade. Se a categoria de armazenamento inteira foi excluída do teste, esse prompt não será exibido. Isso permitirá a validação do cluster sem tempo de inatividade.  
  
#### <a name="how-to-revalidate-your-cluster"></a>Como revalidar o cluster  
  
1.  No snap-in de Cluster de Failover, na árvore do console, verifique se **Gerenciamento de Cluster de Failover** está selecionado e, em **Gerenciamento**, clique em **Validar uma Configuração**.  
  
2.  Siga as instruções no Assistente para especificar os servidores e os testes, e execute os testes. A página **Resumo** aparecerá após a execução dos testes.  
  
3.  Ainda na página **Resumo** , clique em **Exibir Relatório** para exibir os resultados do teste.  
  
     Para exibir os resultados dos testes depois de fechar o assistente, confira **%SystemRoot%\Cluster\Reports\Validation Report date and time.html** em que **%SystemRoot%** é a pasta na qual o sistema operacional está instalado (por exemplo, **C:\Windows**).  
  
4.  Para exibir os tópicos de ajuda que auxiliarão você a interpretar os resultados, clique em **Mais sobre os testes de validação de cluster**.  
  
 Para exibir os tópicos de ajuda sobre a validação de cluster depois de fechar o assistente, no snap-in de Cluster de Failover, clique em **Ajuda**, clique em **Tópicos da Ajuda**, clique na guia **Conteúdo** , expanda o conteúdo da ajuda do cluster de failover e clique em **Validando uma Configuração de Cluster de Failover**.  Após a conclusão do assistente de validação, o **Relatório de Resumo** exibirá os resultados. Todos os testes devem passar com uma marca de seleção verde ou, em alguns casos, um triângulo amarelo (aviso). Ao procurar áreas problemáticas (Xs vermelhos ou pontos de interrogação amarelos), na parte do relatório que resume os resultados do teste, clique em um teste individual para revisar os detalhes. Todos os problemas marcados com X vermelho precisarão ser resolvidos antes de solucionar os problemas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **Instalar atualizações**  
  
 A instalação de atualizações é uma parte importante para evitar problemas com seu sistema. Links úteis:  
  
-   [Hotfixes e atualizações recomendados para clusters de failover com base no Windows Server 2012 R2](https://support.microsoft.com/kb/2920151)  
  
-   [Hotfixes e atualizações recomendados para clusters de failover com base no Windows Server 2012](https://support.microsoft.com/kb/278426)  
  
-   [Hotfixes e atualizações recomendados para clusters de failover com base no Windows Server 2008 R2](https://support.microsoft.com/kb/980054)  
  
-   [Hotfixes e atualizações recomendados para clusters de failover com base no Windows Server 2008](https://support.microsoft.com/kb/957311)  
  
## <a name="recovering-from-failover-cluster-failure"></a>Recuperando-se de uma falha no cluster de failover  
 Normalmente, uma falha no cluster de failover resulta de uma destas duas causas:  
  
-   Falha de hardware em um nó de um cluster que tem dois nós. Essa falha de hardware pode ter sido causada por uma falha na placa SCSI ou no sistema operacional.  
  
     Para se recuperar dela, remova o nó com falha do cluster de failover usando o programa de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], corrija a falha de hardware com o computador offline, coloque-o online novamente e adicione o nó reparado de volta à instância de cluster de failover.  
  
     Para obter mais informações, consulte [Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md) e [Recuperar-se de uma falha na Instância de Cluster de Failover](../../../sql-server/failover-clusters/windows/recover-from-failover-cluster-instance-failure.md).  
  
-   Falha do sistema operacional. Neste caso, o nó está offline, mas o dano não é irreparável.  
  
     Para se recuperar de uma falha do sistema operacional, recupere o nó e teste o failover. Se a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não executar o failover corretamente, você deverá usar o programa de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para remover o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do cluster de failover, fazer os reparos necessários, colocar o computador online novamente e adicionar o nó reparado de volta à instância de cluster de failover.  
  
     A recuperação de uma falha do sistema operacional dessa maneira pode ser demorada. Se a falha do sistema operacional puder ser recuperada facilmente, evite usar esta técnica.  
  
     Para obter mais informações, consulte [Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md) e [Como se recuperar de falhas no cluster de failover no cenário 2](https://msdn.microsoft.com/library/ms181075\(v=sql.105\).aspx).  
  
## <a name="resolving-common-problems"></a>Resolvendo problemas comuns  
 A lista a seguir descreve problemas de uso comum e explica como resolvê-los.  
  
### <a name="problem-incorrect-use-of-command-prompt-syntax-to-install-sql-server"></a>Problema: uso incorreto da sintaxe de prompt de comando para instalar o SQL Server  
 **Problema 1:** é difícil diagnosticar problemas de instalação quando se usa a opção **/qn** no prompt de comando, pois a opção **/qn** suprime todas as caixas de diálogo e mensagens de erro da instalação. Se a opção **/qn** for especificada, todas as mensagens da instalação, inclusive as mensagens de erro, serão gravadas nos arquivos de log da instalação. Para obter mais informações sobre arquivos de log, consulte [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
 **Resolução 1**: use a opção **/qb** em vez da opção **/qn** . Se você usar a opção **/qb** , a interface do usuário básica de cada etapa será exibida, incluindo as mensagens de erro.  
  
### <a name="problem-sql-server-cannot-log-on-to-the-network-after-it-migrates-to-another-node"></a>Problema: o SQL Server não pode fazer logon na rede depois que migra para outro nó  
 **Problema 1:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não conseguem fazer contato com um controlador de domínio.  
  
 **Resolução 1**: verifique nos logs de eventos se existem sinais de problemas de rede, como falhas de adaptador ou problemas de DNS. Verifique se você consegue executar ping no controlador de domínio.  
  
 **Problema 2:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não são idênticas em todos os nós do cluster ou o nó não reinicia um serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que foi migrado de um nó com problema.  
  
 **Resolução 2:** altere as senhas das contas de serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager. Se você não fizer isso e alterar as senhas de contas de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um nó, também deverá alterar as senhas em todos os outros nós. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager faz isso automaticamente.  
  
### <a name="problem-sql-server-cannot-access-the-cluster-disks"></a>Problema: o SQL Server não consegue acessar discos do cluster  
 **Problema 1: firmware ou drivers do** não são atualizados em todos os nós.  
  
 **Resolução 1:** verifique se todos os nós estão usando versões de firmware corretas e as mesmas versões de driver.  
  
 **Problema 2:** um nó não consegue recuperar discos do cluster que migraram de um nó com falha em um disco de cluster compartilhado com outra letra de unidade.  
  
 **Resolução 2:** as letras de unidade de disco dos discos de cluster devem ser iguais em ambos os servidores. Se não forem, verifique a instalação original do sistema operacional e do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Cluster Service (MSCS).  
  
### <a name="problem-failure-of-a-sql-server-service-causes-failover"></a>Problema: falha de um serviço do SQL Server provoca failover  
 **Resolução:** para impedir que a falha de serviços específicos cause o failover do grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , configure esses serviços usando o Administrador de Cluster do Windows, da seguinte forma:  
  
-   Desmarque a caixa de seleção **Afetar o Grupo** na guia **Avançado** da caixa de diálogo **Propriedades de Texto Completo** . Porém, se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerar um failover, o serviço de pesquisa de texto completo será reiniciado.  
  
### <a name="problem-sql-server-does-not-start-automatically"></a>Problema: o SQL Server não inicia automaticamente  
 **Resolução:** use o Administrador de Cluster do MSCS para iniciar um cluster de failover automaticamente. O serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser definido para ser iniciado manualmente; o Administrador de Cluster deve ser configurado no MSCS para iniciar o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para saber mais, confira [Gerenciando serviços](https://msdn.microsoft.com/library/ms178096\(v=sql.105\).aspx).  
  
### <a name="problem-the-network-name-is-offline-and-you-cannot-connect-to-sql-server-using-tcpip"></a>Problema: o Nome de Rede está offline e você não pode se conectar ao SQL Server usando TCP/IP  
 **Problema 1:** o DNS falha quando o recurso de cluster está configurado para exigir DNS.  
  
 **Resolução 1:** corrija os problemas de DNS.  
  
 **Problema 2:** há um nome duplicado na rede.  
  
 **Resolução 2:** use NBTSTAT para localizar o nome duplicado e corrigir o problema.  
  
 **Problema 3:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não está se conectando usando Pipes Nomeados.  
  
 **Resolução 3:** para se conectar usando Pipes Nomeados, crie um alias usando o SQL Server Configuration Manager para se conectar ao computador apropriado. Por exemplo, se você tiver um cluster com dois nós (**Nó A** e **Nó B**) e uma instância do cluster de failover (**Virtsql**) com uma instância padrão, poderá se conectar ao servidor que está com o recurso de Nome de Rede offline seguindo estas etapas:  
  
1.  Determine em qual nó o grupo que contém a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está sendo executado usando o Administrador de Cluster. Neste exemplo, é o **Nó A**.  
  
2.  Inicie o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse computador usando **net start**. Para saber mais sobre como usar **net start**, confira [Iniciando o SQL Server manualmente](https://msdn.microsoft.com/library/ms191193\(v=sql.105\).aspx).  
  
3.  Inicie o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL Server Configuration Manager no **Nó A**. Veja o nome do pipe em que o servidor está escutando. Deve ser algo semelhante a \\\\.\\$$\VIRTSQL\pipe\sql\query.  
  
4.  No computador cliente, inicie o SQL Server Configuration Manager.  
  
5.  Crie um alias SQLTEST1 para se conectar a este nome de pipe através de Pipes Nomeados. Para isso, insira **Nó A** como o nome do servidor e edite o nome de pipe para que seja \\\\.\pipe\\$$\VIRTSQL\sql\query.  
  
6.  Conecte-se a esta instância usando o alias SQLTEST1 como o nome de servidor.  
  
### <a name="problem-sql-server-setup-fails-on-a-cluster-with-error-11001"></a>Problema: falha da instalação do SQL Server em um cluster com o erro 11001  
 **Problema:** uma chave do Registro órfã em [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.X\Cluster]  
  
 **Resolução:** verifique se o hive do Registro MSSQL.X não está sendo usado e exclua a chave do cluster.  
  
### <a name="problem-cluster-setup-error-the-installer-has-insufficient-privileges-to-access-this-directory-drivemicrosoft-sql-server-the-installation-cannot-continue-log-on-as-an-administrator-or-contact-your-system-administrator"></a>Problema: Erro de instalação do cluster: “O instalador não tem privilégios suficientes para acessar este diretório: \<drive>\Microsoft SQL Server. A instalação não pode continuar. Efetue logon como administrador ou contate o administrador do sistema"  
 **Problema:** este erro é causado por uma unidade SCSI compartilhada que não foi particionada corretamente.  
  
 **Resolução:** recrie uma única partição no disco compartilhado seguindo estas etapas:  
  
1.  Exclua o recurso de disco do cluster.  
  
2.  Exclua todas as partições do disco.  
  
3.  Verifique nas propriedades do disco se o disco é um disco básico.  
  
4.  Crie uma partição no disco compartilhado, formate o disco e atribua a ele uma letra de unidade.  
  
5.  Adicione o disco ao cluster usando o Administrador de Cluster (cluadmin).  
  
6.  Execute a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
### <a name="problem-applications-fail-to-enlist-sql-server-resources-in-a-distributed-transaction"></a>Problema: aplicativos não inscrevem recursos do SQL Server em uma transação distribuída  
 **Problema:** como o MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ) não está totalmente configurado no Windows, os aplicativos que não inscrevam recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma transação distribuída poderão falhar. Esse problema pode afetar servidores vinculados, consultas distribuídas e procedimentos armazenados remotos que usam transações distribuídas. Para obter mais informações sobre como configurar o MS DTC, consulte [Antes de instalar o Clustering de Failover](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md).  
  
 **Resolução:** para evitar problemas desse tipo, você deve habilitar totalmente os serviços MS DTC nos servidores em que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está instalado e o MS DTC está configurado.  
  
 Para habilitar completamente o MS DTC, use as seguintes etapas:  
  
1.  No Painel de Controle, abra **Ferramentas Administrativas**e **Gerenciamento do Computador**.  
  
2.  No painel da esquerda do Gerenciamento do Computador, expanda **Serviços e Aplicativos**e clique em **Serviços**.  
  
3.  No painel direito do Gerenciamento do Computador, clique com o botão direito do mouse em **Coordenador de Transações Distribuídas**e selecione **Propriedades**.  
  
4.  Na janela **Coordenador de Transações Distribuídas** , clique na guia **Geral** e clique em **Parar** para interromper o serviço.  
  
5.  Na janela **Coordenador de Transações Distribuídas** , clique na guia **Logon** e defina a conta de logon como NT AUTHORITY\NetworkService.  
  
6.  Clique em **Aplicar** e em **OK** para fechar a janela **Coordenador de Transações Distribuídas** . Feche a janela **Gerenciamento do Computador** . Feche a janela **Ferramentas Administrativas** .  
  
## <a name="using-extended-stored-procedures-and-com-objects"></a>Usando procedimentos armazenados estendidos e objetos COM  
 Quando você usa procedimentos armazenados estendidos com uma configuração de clustering de failover, todos os procedimentos armazenados estendidos devem ser instalados em um disco de cluster dependente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Isso garante que, quando um nó executar failover, os procedimentos armazenados estendidos ainda poderão ser usados.  
  
 Se os procedimentos armazenados estendidos usam componentes COM, o administrador deve registrar esses componentes em cada nó do cluster. As informações para carregar e executar componentes COM devem estar no Registro do nó ativo para que os componentes sejam criados. Caso contrário, as informações permanecerão no Registro do computador em que os componentes COM foram registrados primeiro.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Como funcionam os procedimentos armazenados estendidos](../../../relational-databases/extended-stored-procedures-programming/how-extended-stored-procedures-work.md)   
 [Características de execução de procedimentos armazenados estendidos](../../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
  
  

