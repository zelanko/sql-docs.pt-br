---
title: Noções básicas de disponibilidade do SQL Server para implantações do Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4e42088227e22f6368426b9c4e8dc8134dbb49d7
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719364"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Noções básicas de disponibilidade do SQL Server para implantações do Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Começando com [!INCLUDE[sssql17-md](../includes/sssql17-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] tem suporte no Linux e Windows. Com base em Windows, como [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instâncias e bancos de dados precisam estar altamente disponível no Linux. Este artigo aborda os aspectos técnicos de planejamento e implantação altamente disponível com base em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] bancos de dados e instâncias, bem como algumas das diferenças de instalações baseadas em Windows. Porque [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] podem ser novos para os profissionais de Linux e no Linux podem ser novos para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] profissionais, o artigo às vezes apresenta os conceitos que podem estar a algumas familiar e a outras pessoas.

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Opções de disponibilidade para implantações do Linux
Além de backup e restauração, os mesmos três recursos de disponibilidade estão disponíveis no Linux, como para implantações com base no Windows:
-   Grupos de disponibilidade (grupos de disponibilidade) Always On
-   Sempre em instâncias de Cluster de Failover (FCIs)
-   [Envio de log](sql-server-linux-use-log-shipping.md)

No Windows, as FCIs exigem sempre um cluster de failover subjacente do Windows Server (WSFC). Dependendo do cenário de implantação, um grupo de disponibilidade normalmente exige um WSFC subjacente, com a exceção que está sendo a nova variante em nenhum [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Um WSFC não existe no Linux. Clustering de implementação no Linux é abordado na seção [instâncias do Pacemaker para grupos de disponibilidade AlwaysOn e o failover de cluster do Linux](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux).

## <a name="a-quick-linux-primer"></a>Uma rápida introdução do Linux
Embora algumas instalações do Linux podem ser instaladas com uma interface, a maioria não é, que significa que quase tudo na camada do sistema operacional é feito por meio da linha de comando. O termo comum para essa linha de comando no mundo Linux é uma *shell bash*.

No Linux, muitos comandos precisam ser executados com privilégios elevados, assim como muitas coisas que precisa ser feitas no Windows Server como um administrador. Há dois métodos principais para executar com privilégios elevados:
1. Execute no contexto do usuário apropriado. Para alterar para um usuário diferente, use o comando `su`. Se `su` é executada por conta própria sem um nome de usuário, desde que você sabe a senha, você agora deverá estar no como se fosse *raiz*.
   
2. O mais comum e segurança consciente maneira de executar as coisas é usar `sudo` antes de executar qualquer coisa. Muitos dos exemplos neste artigo usam `sudo`.

Alguns comandos comuns, cada um deles tem vários parâmetros e opções que podem ser pesquisadas online:
-   `cd` -Altere o diretório
-   `chmod` -alterar as permissões de um arquivo ou diretório
-   `chown` -alterar a propriedade de um arquivo ou diretório
-   `ls` -Mostrar o conteúdo de um diretório
-   `mkdir` -criar uma pasta (diretório) em uma unidade
-   `mv` -Mover um arquivo de um local para outro
-   `ps` -Mostrar todos os processos de trabalho
-   `rm` -Excluir um arquivo localmente em um servidor
-   `rmdir` -Excluir uma pasta (diretório)
-   `systemctl` -Iniciar, parar ou habilitar os serviços
-   Comandos do editor de texto. No Linux, há várias opções de editor de texto, como vi e emacs.

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>Tarefas comuns para as configurações de disponibilidade de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux
Esta seção aborda as tarefas que são comuns a todos os baseados em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações.

### <a name="ensure-that-files-can-be-copied"></a>Certifique-se de que os arquivos podem ser copiados
Copiar arquivos de um servidor para outro é uma tarefa que qualquer pessoa usando [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux deve ser capaz de fazer. Essa tarefa é muito importante para as configurações de grupo de disponibilidade.

Coisas como problemas de permissão podem existir no Linux, bem como em instalações baseadas em Windows. No entanto, quem está familiarizado com como copiar de um servidor no Windows podem não estar familiarizados com como isso é feito no Linux. Um método comum é usar o utilitário de linha de comando `scp`, que significa de cópia seguro. Nos bastidores, `scp` usa OpenSSH. SSH significa um shell seguro. Dependendo da distribuição do Linux, OpenSSH propriamente dito não pode ser instalado. Se não for, o OpenSSH precisa ser instalado primeiro. Para obter mais informações sobre como configurar o OpenSSH, consulte as informações nos seguintes links para cada distribuição:
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/ch-openssh)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Ao usar `scp`, você deve fornecer as credenciais do servidor, se não for a origem ou destino. Por exemplo, usando

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

Copia o arquivo MyAGCert.cer para a pasta especificada no outro servidor. Observe que você deve ter permissões – e, possivelmente, a propriedade - do arquivo para copiá-lo, portanto, `chown` talvez precise ser empregado antes de copiar. Da mesma forma, no lado de recepção, o usuário correto precisa de acesso para manipular o arquivo. Por exemplo, para restaurar esse arquivo de certificado, o `mssql` usuário deve ser capaz de acessá-lo.

O Samba, que é a variante do Linux do protocolo SMB (protocolo SMB), também pode ser usado para criar compartilhamentos acessados por caminhos UNC, como `\\SERVERNAME\SHARE`. Para obter mais informações sobre como configurar o Samba, consulte as informações nos seguintes links para cada distribuição:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

Compartilhamentos do SMB baseados no Windows também podem ser usados; Compartilhamentos SMB não precisa ser baseado em Linux, desde que a parte do cliente do Samba está configurada corretamente no servidor Linux que hospeda [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e o compartilhamento tem o acesso correto. Para aqueles em um ambiente misto, isso seria uma maneira de aproveitar a infra-estrutura existente para baseado em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações.

Uma coisa que é importante é que a versão do Samba implantado deve ser compatível com o SMB 3.0. Quando o suporte ao SMB foi adicionado no [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], ela exigia que todos os compartilhamentos para dar suporte a SMB 3.0. Se usando o Samba para o compartilhamento e não o Windows Server, deverá usar o compartilhamento de Samba Samba 4.0 ou posterior e idealmente 4.3 ou posterior, que dá suporte a SMB 3.1.1. É uma boa fonte de informações sobre o Linux e do SMB [SMB3 em Samba](https://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf).

Por fim, usar um compartilhamento de NFS (sistema) de arquivos de rede é uma opção. Usar o NFS não for uma opção em implantações com base em Windows de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]e só pode ser usado para implantações com base em Linux.

### <a name="configure-the-firewall"></a>Configurar o firewall
Semelhante ao Windows, distribuições do Linux tem um firewall interno. Se sua empresa está usando um firewall externo para os servidores, desabilitar os firewalls no Linux pode ser aceitável. No entanto, independentemente de onde o firewall estiver habilitado, portas precisam ser abertas. A tabela a seguir documenta as portas comuns necessárias para altamente disponível [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações no Linux.

| Número da Porta | Tipo     | Descrição                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS - `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (se usado) - mapeador de ponto de extremidade                                                                                          |
| 137         | UDP      | Samba (se usado) - serviço de nomes NetBIOS                                                                                      |
| 138         | UDP      | Samba (se usado) - datagrama NetBIOS                                                                                          |
| 139         | TCP      | Samba (se usado) - sessão NetBIOS                                                                                           |
| 445         | TCP      | Samba (se usado) - SMB sobre TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -porta; padrão Se desejar, pode alterar com `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP, UDP | NFS (se usado)                                                                                                               |
| 2224        | TCP      | Pacemaker – usado por `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker – necessário se houver nós remotos do Pacemaker                                                                    |
| 3260        | TCP      | iSCSI Initiator (se usado) – pode ser alterado em `/etc/iscsi/iscsid.config` (RHEL), mas deve corresponder à porta de destino iSCSI |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -padrão a porta usada para um ponto de extremidade do grupo de disponibilidade; pode ser alterado durante a criação de ponto de extremidade                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker – necessário por Corosync, se estiver usando o UDP multicast                                                                     |
| 5405        | UDP      | Pacemaker – exigido pelo Corosync                                                                                            |
| 21064       | TCP      | Pacemaker – exigido por recursos usando DLM                                                                                 |
| Variável    | TCP      | Porta de ponto de extremidade do grupo de disponibilidade; o padrão é 5022                                                                                           |
| Variável    | TCP      | A porta para NFS - `LOCKD_TCPPORT` (encontrado no `/etc/sysconfig/nfs` no RHEL)                                              |
| Variável    | UDP      | A porta para NFS - `LOCKD_UDPPORT` (encontrado no `/etc/sysconfig/nfs` no RHEL)                                              |
| Variável    | TCP/UDP  | A porta para NFS - `MOUNTD_PORT` (encontrado no `/etc/sysconfig/nfs` no RHEL)                                                |
| Variável    | TCP/UDP  | A porta para NFS - `STATD_PORT` (encontrado no `/etc/sysconfig/nfs` no RHEL)                                                 |

Para portas adicionais que podem ser usadas por Samba, consulte [uso da porta do Samba](https://wiki.samba.org/index.php/Samba_Port_Usage).

Por outro lado, o nome do serviço no Linux também pode ser adicionado como uma exceção em vez da porta; Por exemplo, `high-availability` para Pacemaker. Consulte sua distribuição para os nomes se essa é a direção em que você deseja buscar. Por exemplo, no RHEL o comando para adicionar no Pacemaker é

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**Documentação do firewall:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>Instalar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pacotes para disponibilidade
Em um Windows baseado em [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instalação, alguns componentes são instalados, mesmo em uma instalação do mecanismo básico, enquanto outros não são. No Linux, apenas o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] mecanismo é instalado como parte do processo de instalação. Todo o resto é opcional. Para alta disponibilidade [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instâncias no Linux, dois pacotes devem ser instalados com [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agente (*mssql-server-agent*) e o pacote de alta disponibilidade (HA) (*mssql-server-ha*). Embora [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent é tecnicamente opcional, ele é [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]do Agendador de trabalhos e é exigido pelo envio de logs, portanto, é recomendável a instalação. Em instalações baseadas em Windows, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente não é opcional.

>[!NOTE]
>Para os iniciantes em [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente é [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]do Agendador de trabalho internas. É uma maneira comum de DBAs agendar a coisas como backups e outras [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] manutenção. Ao contrário de uma instalação baseada em Windows de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] onde [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente é um serviço completamente diferente, no Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente é executado no contexto do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] em si.

Quando grupos de disponibilidade ou FCIs são configuradas em uma configuração baseada em Windows, eles são com suporte a cluster. Significa que, reconhecimento de cluster [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] tem o recurso específico DLLs que conhece um WSFC (sqagtres. dll e sqsrvres.dll sobre as FCIs, hadrres. dll para grupos de disponibilidade) e são usados pelo WSFC para garantir que o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] funcionalidade clusterizada está ativo, em execução, e funcionando corretamente. Porque o clustering externo não é apenas para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] mas Linux em si, a Microsoft tinha codificar o equivalente de uma DLL de recursos para implantações de AG baseado em Linux e a FCI. Esse é o *mssql-server-ha* de pacote, também conhecido como o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente de recursos do Pacemaker. Para instalar o *mssql-server-ha* do pacote, consulte [instalar os pacotes de alta disponibilidade e o SQL Server Agent](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages).

Os pacotes opcionais para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pesquisa de texto completo (*mssql-server-fts*) e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-está*), não são necessária para alta disponibilidade, para uma FCI ou um grupo de disponibilidade.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Pacemaker para grupos de disponibilidade AlwaysOn e instâncias de cluster de failover no Linux
Anterior como observado, o único mecanismo de clustering atualmente com suporte pela Microsoft para grupos de disponibilidade e FCIs é Pacemaker com Corosync. Esta seção aborda as informações básicas para entender a solução, bem como planejar e implantá-lo para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] configurações.

### <a name="ha-add-onextension-basics"></a>Noções básicas de add-on/extensão de alta disponibilidade
Todas as distribuições com suporte no momento, envie um add-on/extensão de alta disponibilidade, que se baseia o Pacemaker cluster pilha. Essa pilha incorpora dois componentes principais: Pacemaker e do Corosync. Todos os componentes da pilha são:
-   Pacemaker – o núcleo do clustering de componente, que faz coisas como coordenada entre as máquinas em cluster.
-   Corosync - uma estrutura e um conjunto de APIs que fornece coisas como o quorum, a capacidade de falha ao reiniciar processos e assim por diante.
-   libQB - fornece coisas como o registro em log.
-   Agente de recursos - funcionalidade específica fornecida para que um aplicativo pode integrar com o Pacemaker.
-   De cerca de agente - Scripts/funcionalidade que ajuda a isolar nós e lidar com eles, se eles estão tendo problemas.
    
> [!NOTE]
> A pilha do cluster é conhecida como Pacemaker no mundo Linux.

Essa solução é de certa forma semelhante ao, mas de várias maneiras diferentes de implantar configurações em cluster usando o Windows. Em Windows, o formulário de disponibilidade de clustering, chamado de um cluster de failover do Windows Server (WSFC), é integrado ao sistema operacional e o recurso que permite a criação de um WSFC, cluster de failover, é desabilitada por padrão. No Windows, grupos de disponibilidade e FCIs são criadas sobre um WSFC em compartilhar uma forte integração devido ao recurso específico DLL que é fornecido pelo [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Essa solução firmemente acoplada é possível geral porque se trata tudo a partir de um fornecedor.

![](./media/sql-server-linux-ha-basics/image1.png)

No Linux, enquanto cada distribuição com suporte tem o Pacemaker disponível, cada distribuição pode personalizar e têm versões e implementações ligeiramente diferentes. Algumas das diferenças serão refletidas nas instruções neste artigo. A camada de clustering é um software livre, portanto, mesmo que ele seja fornecido com as distribuições, ele não integra-se da mesma forma um WSFC no Windows. Isso é por isso que a Microsoft fornece *mssql-server-ha*, de modo que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e a pilha do Pacemaker pode fornecer proximidade, mas não exatamente a mesma experiência de grupos de disponibilidade e FCIs no Windows.

Para obter a documentação completa no Pacemaker, incluindo uma explicação mais detalhada do que tudo o que é com informações de referência completa, para RHEL e SLES:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu não tem um guia para disponibilidade.

Para obter mais informações sobre a pilha inteira, consulte também a oficial [página de documentação do Pacemaker](https://clusterlabs.org/doc/) no site Clusterlabs.

### <a name="pacemaker-concepts-and-terminology"></a>Terminologia e conceitos do pacemaker
Esta seção documenta os conceitos e terminologia para uma implementação do Pacemaker comuns.

#### <a name="node"></a>Nó
Um nó é um servidor que participam no cluster. Um cluster Pacemaker nativamente dá suporte a até 16 nós. Esse número pode ser excedido se Corosync não está em execução em nós adicionais, mas Corosync é necessária para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Portanto, o número máximo de nós de um cluster pode ter qualquer [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-com base de configuração é 16; esse é o limite do Pacemaker e não tem nada a ver com as limitações máximas para grupos de disponibilidade ou FCIs impostas pelo [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. 

#### <a name="resource"></a>Resource
Um WSFC e um cluster Pacemaker tem o conceito de um recurso. Um recurso é uma funcionalidade específica que é executado no contexto do cluster, como um disco ou um endereço IP. Por exemplo, sob o Pacemaker FCI e o grupo de disponibilidade de recursos podem ser criados. Isso não é parecido com o que é feito em um WSFC, onde você vê uma [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] recursos para a uma FCI ou em um recurso de grupo de disponibilidade ao configurar um grupo de disponibilidade, mas é não exatamente o mesmo devido a diferenças subjacente como [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] integra-se com o Pacemaker.

Pacemaker tem recursos standard e clone. Recursos de clonagem são aqueles que são executados simultaneamente em todos os nós. Um exemplo seria um endereço IP que é executado em vários nós para fins de balanceamento de carga. Qualquer recurso que é criado sobre as FCIs usa um recurso padrão, uma vez que apenas um nó pode hospedar uma FCI a qualquer momento.

Quando um grupo de disponibilidade é criado, ele requer uma forma especializada de um recurso de clone chamado um recurso de vários estado. Embora um grupo de disponibilidade tiver apenas uma réplica primária, o grupo de disponibilidade em si está em execução em todos os nós que ele está configurado para funcionar em e potencialmente pode permitir que as coisas, como o acesso somente leitura. Como esse é um uso "ao vivo" do nó, os recursos têm o conceito de dois estados: mestre e subordinado. Para obter mais informações, consulte [recursos de vários estados: Recursos que têm vários modos de](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html).

#### <a name="resource-groupssets"></a>Grupos de recursos/conjuntos
Semelhante às funções em um WSFC, um cluster Pacemaker tem o conceito de um grupo de recursos. Um grupo de recursos (chamado de um conjunto no SLES) é uma coleção de recursos que funcionam em conjunto e pode fazer failover de um nó para outro como uma única unidade. Grupos de recursos não podem conter recursos que são configurados como primário/secundário Portanto, não pode ser usados para grupos de disponibilidade. Embora um grupo de recursos pode ser usado para FCIs, não é geralmente uma configuração recomendada.

#### <a name="constraints"></a>Restrições
WSFCs tem vários parâmetros de recursos, bem como coisas como dependências, que informam o WSFC de uma relação de pai/filho entre dois recursos diferentes. Uma dependência é apenas uma regra informando o WSFC qual recurso precisa estar online pela primeira vez.

Um cluster Pacemaker não tem o conceito de dependências, mas há restrições. Há três tipos de restrições: colocação, o local e a ordenação.
-   Uma restrição de colocação impõe se dois recursos devem estar em execução no mesmo nó.
-   Uma restrição de local informa ao cluster do Pacemaker em que um recurso pode (ou não) ser executado.
-   Uma restrição de ordenação informa ao cluster do Pacemaker a ordem na qual os recursos devem começar.

> [!NOTE]
> Restrições de colocação não são necessárias para recursos em um grupo de recursos, já que todas essas são vistas como uma única unidade.

#### <a name="quorum-fence-agents-and-stonith"></a>Quorum, agentes de limite e STONITH
Quorum sob o Pacemaker é um pouco semelhante a um WSFC em conceito. É o único propósito do mecanismo de quorum do cluster garantir que o cluster permaneça em funcionamento. Um WSFC e os complementos de alta disponibilidade para as distribuições do Linux tem o conceito de votação, em que cada nó de conta para o quorum. Você deseja que a maioria dos votos, caso contrário, na pior das hipóteses, o cluster será desligado.

Ao contrário de um WSFC, não há nenhum recurso de testemunha para trabalhar com o quorum. Como um WSFC, o objetivo é manter o número de eleitores ímpares. Configuração de quorum tem diferentes considerações para grupos de disponibilidade que FCIs.

WSFCs monitoram o status de nós participantes e tratarão-los quando ocorre um problema. Em versões posteriores do WSFCs oferecem recursos como colocar em quarentena um nó que está com comportamento inadequado ou não disponível (o nó não está ativada, comunicação de rede é para baixo, etc.). No lado do Linux, esse tipo de funcionalidade é fornecido por um agente de isolamento. O conceito, às vezes é chamado de isolamento. No entanto, esses agentes de limite são geralmente específicas para a implantação e geralmente são fornecidos por fornecedores de hardware e fornecedores de software, como aqueles que fornecem os hipervisores. Por exemplo, o VMware fornece um agente de isolamento que pode ser usado para VMs do Linux virtualizados usando vSphere.

Quorum e vínculos de isolamento em outro conceito chamado STONITH, ou envie outro nó no cabeçalho. STONITH é necessário ter um cluster Pacemaker com suporte em todas as distribuições do Linux. Para obter mais informações, consulte [de isolamento em um Cluster de disponibilidade alta do Red Hat](https://access.redhat.com/solutions/15575) (RHEL).

#### <a name="corosyncconf"></a>corosync.conf
O `corosync.conf` arquivo contém a configuração do cluster. Ele está localizado em `/etc/corosync`. No decorrer de suas operações diárias normais, esse arquivo nunca deve ter que ser editado se o cluster está configurado corretamente.

#### <a name="cluster-log-location"></a>Local do log de cluster
Locais de log para clusters do Pacemaker diferem dependendo da distribuição.
-   RHEL e SLES- `/var/log/cluster/corosync.log`
-   Ubuntu - `/var/log/corosync/corosync.log`

Para alterar o local de registro em log padrão, modifique `corosync.conf`.

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Planejar clusters Pacemaker para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Esta seção discute os pontos importantes de planejamento para um cluster do Pacemaker.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Para clusters do Pacemaker virtualização baseado em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Usando máquinas virtuais para implantar com base em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações de grupos de disponibilidade e FCIs é coberto pelas mesmas regras de suas contrapartes baseado em Windows. Há um conjunto básico de regras para dar suporte a de virtualizados [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações fornecidas pela Microsoft no [956893 de KB de suporte do Microsoft](https://support.microsoft.com/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment). Os hipervisores diferentes, como o Microsoft Hyper-V e ESXi do VMware podem ter diferentes variações disso, devido a diferenças nas plataformas em si.

Quando se trata de grupos de disponibilidade e FCIs em virtualização, certifique-se de que a antiafinidade está definida para os nós de um determinado cluster Pacemaker. Quando configurado para alta disponibilidade em uma configuração de grupo de disponibilidade ou FCI, VMs que hospedam [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] nunca deve estar em execução no mesmo host do hipervisor. Por exemplo, se uma FCI de dois nós for implantada, precisaria ser *pelo menos* três hosts de hipervisor, portanto, o que há em algum lugar para uma das VMs que hospedam um nó de ir em caso de falha do host, especialmente se o uso de recursos, como ao vivo A migração ou vMotion.

Para obter informações mais específicas, consulte:
-   Documentação do Hyper-V - [Using Guest Clustering for High Availability](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   White paper (escrito para implantações com base no Windows, mas a maioria dos conceitos ainda se aplicam) - [planejamento altamente disponível, o SQL Server implantações críticas com VMware vSphere](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>RHEL com um cluster Pacemaker com STONITH ainda não é suportado pelo Hyper-V. Até que tenha suporte, para obter mais informações e atualizações, consulte [políticas de suporte para os Clusters de alta disponibilidade RHEL](https://access.redhat.com/articles/29440#3physical_host_mixing).

### <a name="networking"></a>Rede
Ao contrário de um WSFC, o Pacemaker não requer um nome dedicado ou pelo menos um endereço IP dedicado para o cluster do Pacemaker em si. Grupos de disponibilidade e FCIs exigem endereços IP (consulte a documentação para cada um para obter mais informações), mas não nomes, já que não há nenhum recurso de nome de rede. SLES permite a configuração de um endereço IP para fins de administração, mas não é necessário, como pode ser visto na [criar o cluster do Pacemaker](sql-server-linux-deploy-pacemaker-cluster.md#create).

Como um WSFC, Pacemaker prefere rede redundante, ou seja, placas de rede distintas (pNICs para máquina física ou NICs) ter endereços IP individuais. Em termos de configuração de cluster, cada endereço IP teria que é conhecido como seu próprio token de autenticação. No entanto, como com e de WSFCs hoje em dia, muitas implementações são virtualizadas ou na nuvem pública em que há realmente apenas uma única virtualizado vNIC (NIC) apresentado ao servidor. Não se todos os pNICs e vNICs estão conectadas ao mesmo comutador físico ou virtual, há nenhuma redundância real na camada de rede, então configurar várias NICs é um pouco de uma ilusão à máquina virtual. Redundância de rede normalmente é compilada em um hipervisor para implantações virtualizadas e definitivamente é criada para a nuvem pública.

Uma diferença com várias NICs e Pacemaker versus um WSFC é que o Pacemaker permite vários endereços IP na mesma sub-rede, enquanto um WSFC não. Para obter mais informações em várias sub-redes e clusters do Linux, consulte o artigo [configurar múltiplas sub-redes](sql-server-linux-configure-multiple-subnet.md).

### <a name="quorum-and-stonith"></a>Quorum e STONITH
Configuração de quorum e os requisitos são relacionados às implantações de grupo de disponibilidade ou FCI específicos do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

STONITH é necessária para um cluster Pacemaker com suporte. Use a documentação da distribuição para configurar o STONITH. Um exemplo é em [isolamento baseado em armazenamento](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) para SLES. Também há um agente STONITH para o VMware vCenter para soluções baseadas em ESXI. Para obter mais informações, consulte [Stonith plug-in do agente para VMWare VM VCenter SOAP de isolamento (Unofficial)](https://github.com/olafrv/fence_vmware_soap).

> [!NOTE]
> No momento da elaboração deste artigo, o Hyper-V não tem uma solução para STONITH. Isso é verdadeiro para implantações locais e também afeta as implantações do Pacemaker baseado no Azure usando determinadas distribuições como RHEL.

### <a name="interoperability"></a>Interoperabilidade
Esta seção documenta como um cluster baseado em Linux pode interagir com um WSFC ou com outras distribuições do Linux.

#### <a name="wsfc"></a>WSFC
Atualmente, não há nenhuma maneira direta de um WSFC e um cluster Pacemaker para trabalharem juntos. Isso significa que não há nenhuma maneira de criar um grupo de disponibilidade ou FCI que funciona em um WSFC e o Pacemaker. No entanto, há duas soluções de interoperabilidade, sendo que ambos são projetados para grupos de disponibilidade. A única maneira de que uma FCI pode participar de uma configuração de plataforma cruzada é se ela está participando como uma instância em um desses dois cenários:
-   Um grupo de disponibilidade com um tipo de cluster nenhum. Para obter mais informações, consulte o Windows [documentação dos grupos de disponibilidade](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).
-   Um grupo de disponibilidade distribuído, que é um tipo especial de grupo de disponibilidade que permite que dois grupos de disponibilidade diferentes a ser configurado como seu próprio grupo de disponibilidade. Para obter mais informações sobre grupos de disponibilidade distribuídos, consulte a documentação [grupos de disponibilidade distribuída](../database-engine/availability-groups/windows/distributed-availability-groups.md).

#### <a name="other-linux-distributions"></a>Outras distribuições do Linux
No Linux, todos os nós de um cluster Pacemaker devem ser a mesma distribuição. Por exemplo, isso significa que um nó RHEL não pode ser parte de um cluster Pacemaker que tem um nó SLES. O principal motivo para isso foi mencionado anteriormente: as distribuições podem ter diferentes versões e funcionalidades, então as coisas não poderiam funcionar corretamente. Combinação de distribuições tem a mesma história que misturar WSFCs e Linux: usar nenhum ou distribuído grupos de disponibilidade.

## <a name="next-steps"></a>Próximas etapas
[Implantar um cluster de Pacemaker para o SQL Server no Linux](sql-server-linux-deploy-pacemaker-cluster.md)
