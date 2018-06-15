---
title: Noções básicas de disponibilidade do SQL Server para implantações do Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: f311d9c3116083120b97fa78486242939a438de9
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34324057"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Noções básicas de disponibilidade do SQL Server para implantações do Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Começando com [!INCLUDE[sssql17-md](../includes/sssql17-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] tem suporte no Linux e Windows. Baseado no Windows, como [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instâncias e bancos de dados precisam ser altamente disponível em Linux. Este artigo aborda os aspectos técnicos de planejamento e implantação altamente disponível com base em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] bancos de dados e instâncias, bem como algumas das diferenças de instalações baseadas em Windows. Porque [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] podem ser novos para profissionais de Linux e Linux podem ser novos para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] profissionais, o artigo às vezes apresenta conceitos que podem ser familiar a algumas e não familiar para outras pessoas.

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Opções de disponibilidade para implantações do Linux
Além de backup e restauração, os mesmos recursos de disponibilidade de três estão disponíveis no Linux para implantações com base no Windows:
-   Grupos de disponibilidade AlwaysOn (grupos de disponibilidade)
-   Sempre em instâncias de Cluster de Failover (FCIs)
-   [Envio de log](sql-server-linux-use-log-shipping.md)

No Windows, FCIs sempre requerem um cluster de failover subjacente do Windows Server (WSFC). Dependendo do cenário de implantação, um grupo de disponibilidade geralmente não requer um WSFC subjacente, com a exceção que está sendo a nova variante em [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Um WSFC não existe no Linux. Clustering de implementação no Linux é discutida na seção [Pacemaker para cluster de failover e grupos de disponibilidade AlwaysOn instâncias no Linux](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux).

## <a name="a-quick-linux-primer"></a>Uma rápida introdução do Linux
Embora algumas instalações Linux podem ser instaladas com uma interface, a maioria não é, que significa que quase tudo na camada de sistema operacional é feito por meio da linha de comando. O termo comuns para esta linha de comando no mundo Linux é um *bash shell*.

No Linux, muitos comandos precisam ser executado com privilégios elevados, bem como muitas coisas que precisam ser executadas no Windows Server como um administrador. Há dois métodos principais para executar com privilégios elevados:
1. Execute no contexto do usuário apropriado. Para alterar para um usuário diferente, use o comando `su`. Se `su` é executado em seu próprio sem um nome de usuário, desde que você sabe a senha, você agora estará em um shell como *raiz*.
   
2. O mais comum e segurança consciente maneira executar coisas é usar `sudo` antes de executar qualquer coisa. Muitos dos exemplos neste artigo use `sudo`.

Alguns comandos comuns, cada um deles tem várias opções que podem ser pesquisadas on-line e opções:
-   `cd` – Altere o diretório
-   `chmod` – alterar as permissões de um arquivo ou diretório
-   `chown` – alterar a propriedade de um arquivo ou diretório
-   `ls` – Mostrar o conteúdo de um diretório
-   `mkdir` – Crie uma pasta (diretório) em uma unidade
-   `mv` – Mover um arquivo de um local para outro
-   `ps` – Mostrar todos os processos de trabalho
-   `rm` – Excluir um arquivo localmente em um servidor
-   `rmdir` – Excluir uma pasta (diretório)
-   `systemctl` – Iniciar, interromper ou habilitar os serviços
-   Comandos do editor de texto. No Linux, há várias opções de editor de texto, como vi e emacs.

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>Tarefas comuns para configurações de disponibilidade de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux
Esta seção aborda as tarefas que são comuns a todos os baseados em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações.

### <a name="ensure-that-files-can-be-copied"></a>Certifique-se de que os arquivos podem ser copiados
Copiar arquivos de um servidor para outro é uma tarefa que qualquer pessoa usando [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux deve ser capaz de fazer. Essa tarefa é muito importante para as configurações do grupo de disponibilidade.

Coisas como problemas de permissão podem existir no Linux, bem como em instalações baseadas em Windows. No entanto, aqueles que estão familiarizados com a cópia de servidor para servidor no Windows podem não estar familiarizados com como é feito no Linux. Um método comum é usar o utilitário de linha de comando `scp`, que significa de cópia seguro. Nos bastidores, `scp` usa OpenSSH. SSH significa do secure shell. Dependendo da distribuição de Linux, OpenSSH em si não pode ser instalado. Se não estiver, OpenSSH precisa ser instalado primeiro. Para obter mais informações sobre como configurar OpenSSH, consulte as informações nos seguintes links para cada distribuição:
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-OpenSSH.html)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Ao usar `scp`, você deve fornecer as credenciais do servidor se ele não é a origem ou destino. Por exemplo, usando

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

Copia o arquivo MyAGCert.cer para a pasta especificada no outro servidor. Observe que você deve ter permissões – e, possivelmente, a propriedade – do arquivo para copiá-lo, portanto `chown` também precisa ser empregada antes de copiar. Da mesma forma, no lado de recepção, o usuário precisa de acesso para manipular o arquivo. Por exemplo, para restaurar esse arquivo de certificado, o `mssql` usuário deve ser capaz de acessá-lo.

Samba, que é a variante de Linux do bloco de mensagens de servidor (SMB), também pode ser usado para criar compartilhamentos acessados por caminhos UNC, como `\\SERVERNAME\SHARE`. Para obter mais informações sobre como configurar Samba, consulte as informações nos seguintes links para cada distribuição:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

Com base em Windows compartilhamentos SMB também podem ser usados; Compartilhamentos SMB não precisam ser baseada em Linux, como a parte cliente de Samba está configurada corretamente no servidor Linux que hospeda [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e o compartilhamento tem o acesso correto. Para aqueles em um ambiente misto, deve ser uma maneira de aproveitar a infraestrutura existente para baseados em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações.

Uma coisa importante é que a versão do Samba implantada deve ser compatível com o SMB 3.0. Quando o suporte ao SMB foi adicionado no [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], ela exigia a todos os compartilhamentos para dar suporte a SMB 3.0. Se usar Samba para o compartilhamento e não o Windows Server, deve usar o compartilhamento de Samba Samba 4.0 ou posterior e idealmente 4.3 ou posterior, que dá suporte ao SMB 3.1.1. É uma boa fonte de informações sobre o SMB e Linux [SMB3 em Samba](http://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf).

Por fim, usando um compartilhamento de NFS (sistema) de arquivos de rede é uma opção. Usar o NFS não for uma opção em implantações com base em Windows de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]e só pode ser usado para implantações com base em Linux.

### <a name="configure-the-firewall"></a>Configurar o firewall
Semelhante ao Windows, distribuições do Linux tem um firewall interno. Se sua empresa estiver usando um firewall externo para os servidores, desabilitar os firewalls no Linux pode ser aceitável. No entanto, independentemente de onde o firewall estiver habilitado, portas precisam ser abertas. A tabela a seguir documenta as portas comuns necessárias para alta disponibilidade [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações no Linux.

| Número da Porta | Tipo     | Description                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS – `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (se usado) – mapeador de ponto de extremidade                                                                                          |
| 137         | UDP      | Samba (se usado) – serviço de nomes NetBIOS                                                                                      |
| 138         | UDP      | Samba (se usado) – datagrama NetBIOS                                                                                          |
| 139         | TCP      | Samba (se usado) – sessão NetBIOS                                                                                           |
| 445         | TCP      | Samba (se usado) – SMB sobre TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] – porta; padrão Se desejar, pode alterar com `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP, UDP | NFS (se usado)                                                                                                               |
| 2224        | TCP      | Pacemaker – usada pelo `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker – necessário se houver nós remotos Pacemaker                                                                    |
| 3260        | TCP      | iSCSI Initiator (se usado) – pode ser alterado em `/etc/iscsi/iscsid.config` (RHEL), mas deve coincidir com a porta de destino iSCSI |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -padrão a porta usada para um ponto de extremidade do grupo de disponibilidade; pode ser alterado durante a criação de ponto de extremidade                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker – necessário por Corosync se estiver usando multicast UDP                                                                     |
| 5405        | UDP      | Pacemaker – exigido pelo Corosync                                                                                            |
| 21064       | TCP      | Pacemaker – exigido por recursos usando DLM                                                                                 |
| Variável    | TCP      | Porta de ponto de extremidade do grupo de disponibilidade; o padrão é 5022                                                                                           |
| Variável    | TCP      | Porta de NFS – para `LOCKD_TCPPORT` (encontrado no `/etc/sysconfig/nfs` em RHEL)                                              |
| Variável    | UDP      | Porta de NFS – para `LOCKD_UDPPORT` (encontrado no `/etc/sysconfig/nfs` em RHEL)                                              |
| Variável    | TCP/UDP  | Porta de NFS – para `MOUNTD_PORT` (encontrado no `/etc/sysconfig/nfs` em RHEL)                                                |
| Variável    | TCP/UDP  | Porta de NFS – para `STATD_PORT` (encontrado no `/etc/sysconfig/nfs` em RHEL)                                                 |

Para portas adicionais que podem ser usadas por Samba, consulte [uso da porta Samba](https://wiki.samba.org/index.php/Samba_Port_Usage).

Por outro lado, o nome do serviço no Linux também pode ser adicionado como uma exceção em vez da porta; Por exemplo, `high-availability` para Pacemaker. Consulte a distribuição para os nomes se esta é a direção em que você deseja realizar. Por exemplo, em RHEL o comando Adicionar em Pacemaker é

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**Documentação do firewall:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>Instalar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pacotes para disponibilidade
Em um Windows [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instalação, alguns componentes são instalados mesmo em uma instalação básica do mecanismo, enquanto outros não são. No Linux, somente o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] mecanismo é instalado como parte do processo de instalação. Todo o resto é opcional. Para alta disponibilidade [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instâncias no Linux, dois pacotes devem ser instalados com [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente (*mssql-server-agent*) e o pacote de alta disponibilidade (HA) ( *MSSQL-server-ha*). Enquanto [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent é tecnicamente opcional, é [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]do Agendador de trabalhos e é exigido pelo envio de logs, então, é recomendável a instalação. Em instalações baseadas em Windows, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente não é opcional.

>[!NOTE]
>Para os iniciantes em [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]do Agendador de trabalho internas. É uma maneira comum para DBAs agendar coisas como backups e outros [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] manutenção. Ao contrário de uma instalação baseada em Windows de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] onde [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent é um serviço completamente diferente, no Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent é executado no contexto de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] em si.

Quando grupos de disponibilidade ou FCIs são configuradas em uma configuração baseada em Windows, eles têm reconhecimento de cluster. Reconhecimento de cluster significa que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] tem o recurso específico DLLs que conhece um WSFC (sqagtres.dll e sqsrvres.dll para FCIs, hadrres.dll para grupos de disponibilidade) e são usados pelo WSFC para garantir que o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] funcionalidade em cluster é, em execução, e funcionando corretamente. Porque o cluster externo não é apenas para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] mas Linux em si, Microsoft codificar o equivalente de uma DLL de recurso para implantações com base em Linux AG e FCI. Este é o *mssql-server-ha* de pacote, também conhecido como o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente de recurso para Pacemaker. Para instalar o *mssql-server-ha* do pacote, consulte [instalar os pacotes de alta disponibilidade e o SQL Server Agent](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages).

Os pacotes opcionais para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pesquisa de texto completo (*fts do mssql server*) e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql servidor é*), não são necessário para alta disponibilidade, para uma FCI ou um grupo de disponibilidade.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Pacemaker para grupos de disponibilidade AlwaysOn e instâncias de cluster de failover no Linux
Anterior como observado, o único mecanismo de clustering com suporte no momento pela Microsoft para grupos de disponibilidade e FCIs é Pacemaker com Corosync. Esta seção aborda as informações básicas para entender a solução, bem como planejar e implantá-lo para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] configurações.

### <a name="ha-add-onextension-basics"></a>Noções básicas de add-on/extensão de alta disponibilidade
Todas as distribuições com suporte no momento enviar uma alta disponibilidade add-on/extensão, que se baseia o Pacemaker clustering pilha. Esta pilha incorpora dois componentes principais: Pacemaker e Corosync. Todos os componentes da pilha são:
-   Pacemaker – o núcleo de clustering de componente, que faz as coisas como coordenada nos computadores do cluster.
-   Corosync – uma estrutura e um conjunto de APIs que fornece coisas como o quorum, a capacidade de falha ao reiniciar processos e assim por diante.
-   libQB – fornece coisas como o registro em log.
-   Agente de recursos – fornecida para que um aplicativo pode se integrar com Pacemaker de funcionalidade específica.
-   Cerca de agente – Scripts/funcionalidade que ajuda a isolar nós e lidar com eles, se eles estão com problemas.
    
> [!NOTE]
> A pilha de cluster é conhecida como Pacemaker no mundo Linux.

Essa solução é de alguma forma semelhante ao, mas em muitas maneiras diferentes de implantar configurações em cluster usando o Windows. No Windows, a forma de disponibilidade de cluster, chamado de um cluster de failover do Windows Server (WSFC), é criada para o sistema operacional e o recurso que permite a criação de um WSFC, o clustering de failover, é desabilitada por padrão. No Windows, grupos de disponibilidade e FCIs criadas sobre um WSFC em compartilhar integração total devido o recursos específicos DLL que é fornecido pelo [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Essa solução firmemente acoplada é possível de modo geral porque tudo a partir de um fornecedor.

![](./media/sql-server-linux-ha-basics/image1.png)

No Linux, enquanto cada distribuição com suporte tem Pacemaker disponível, cada distribuição pode personalizar e possuem versões e implementações ligeiramente diferentes. Algumas das diferenças se refletirão as instruções neste artigo. A camada de clustering é o código-fonte aberto, portanto, embora ele acompanha as distribuições, ele não integra-se da mesma forma um WSFC no Windows. Este é o motivo pelo qual a Microsoft fornece *mssql-server-ha*, de modo que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e a pilha de Pacemaker pode fornecer Fechar para, mas não exatamente a mesma experiência de grupos de disponibilidade e FCIs no Windows.

Para a documentação completa sobre Pacemaker, incluindo uma explicação mais detalhada do que tudo é com informações de referência completa, para RHEL e SLES:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu não tem um guia para disponibilidade.

Para obter mais informações sobre a pilha inteira, consulte também o oficial [página de documentação Pacemaker](http://clusterlabs.org/doc/) no site Clusterlabs.

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker conceitos e terminologia
Esta seção documenta os conceitos e a terminologia de uma implementação de Pacemaker comuns.

#### <a name="node"></a>Nó
Um nó é um servidor que participam no cluster. Um cluster Pacemaker nativamente dá suporte a até 16 nós. Esse número pode ser excedido se Corosync não está em execução em nós adicionais, mas Corosync é necessária para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Portanto, o número máximo de nós de um cluster pode ter para qualquer [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-com base de configuração é 16; esse é o limite de Pacemaker e tem nada a ver com limitações máximo para grupos de disponibilidade ou FCIs impostas pelo [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. 

#### <a name="resource"></a>Recurso
Um WSFC e um cluster Pacemaker tem o conceito de um recurso. Um recurso é uma funcionalidade específica que é executado no contexto do cluster, como um disco ou um endereço IP. Por exemplo, em Pacemaker FCI e o grupo de disponibilidade de recursos podem ser criados. Isso não é parecido com o que é feito em um WSFC, onde você pode ver um [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] recursos para a uma FCI ou um recurso de grupo de disponibilidade ao configurar um grupo de disponibilidade, mas é não exatamente o mesmo deve a diferenças subjacente como [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] integra Pacemaker.

Pacemaker tem os recursos padrão e o clone. Recursos de clone são aqueles que são executados simultaneamente em todos os nós. Um exemplo seria um endereço IP que é executado em vários nós para fins de balanceamento de carga. Qualquer recurso que é criado para FCIs usa um recurso padrão, já que somente um nó pode hospedar uma FCI a qualquer momento.

Quando um grupo de disponibilidade é criado, ele requer uma forma especializada de um recurso de clone chamado um recurso de vários estado. Enquanto um grupo de disponibilidade tiver apenas uma réplica primária, o grupo de disponibilidade em si está em execução em todos os nós que ele está configurado para funcionar em e pode permitir a coisas como acesso somente leitura. Como esse é um uso "ativo" do nó, os recursos têm o conceito de dois estados: mestre e subordinado. Para obter mais informações, consulte [recursos de vários estados: recursos que têm vários modos](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html).

#### <a name="resource-groupssets"></a>Define/grupos de recursos
Semelhante às funções em um WSFC, um cluster Pacemaker tem o conceito de um grupo de recursos. Um grupo de recursos (chamado de um conjunto em SLES) é uma coleção de recursos que funcionam em conjunto e failover de um nó para outro como uma única unidade. Grupos de recursos não podem conter recursos que são configurados como primário/secundário Portanto, não pode ser usados para grupos de disponibilidade. Embora um grupo de recursos pode ser usado para FCIs, não é geralmente uma configuração recomendada.

#### <a name="constraints"></a>Restrições
WSFCs tem vários parâmetros para recursos, bem como dependências, o que dizer o WSFC de uma relação pai/filho entre dois recursos diferentes. Uma dependência é apenas uma regra informando o WSFC qual recurso deve ser on-line pela primeira vez.

Um cluster Pacemaker não tem o conceito de dependências, mas há restrições. Há três tipos de restrições: colocação, o local e a ordenação.
-   Uma restrição de colocação impõe se dois recursos devem estar em execução no mesmo nó ou não.
-   Uma restrição de local informa o cluster Pacemaker em que um recurso pode (ou não) ser executado.
-   Uma restrição de ordenação informa o cluster Pacemaker a ordem na qual os recursos devem começar.

> [!NOTE]
> Restrições de colocação não são necessárias para recursos em um grupo de recursos, pois todas essas são consideradas como uma única unidade.

#### <a name="quorum-fence-agents-and-stonith"></a>Quorum, agentes de limite e STONITH
Quorum em Pacemaker é semelhante a um WSFC em conceito. É o único propósito do mecanismo de quorum do cluster garantir que o cluster esteja ativo e em execução. Um WSFC e os complementos de alta disponibilidade para as distribuições do Linux tem o conceito de votação, onde cada nó contabilizará de quorum. Desejar que a maioria dos votos, caso contrário, na pior das hipóteses, o cluster será encerrado.

Ao contrário de um WSFC, não há nenhum recurso de testemunha para trabalhar com o quorum. Como um WSFC, o objetivo é manter o número dos votantes ímpares. Configuração de quorum tem considerações diferentes para grupos de disponibilidade que FCIs.

WSFCs monitorar o status de nós participantes e tratá-los quando ocorre um problema. Em versões posteriores do WSFCs oferecem recursos como colocar em quarentena um nó que está indisponível ou com comportamento inadequado (nó não está ativado, a comunicação de rede é para baixo, etc.). No lado do Linux, esse tipo de funcionalidade é fornecido por um agente de limite. Às vezes, o conceito é conhecido como isolamento. No entanto, esses agentes limite geralmente especificam para a implantação e geralmente é fornecido por fornecedores de hardware e alguns fornecedores de software, como aqueles que fornecem os hipervisores. Por exemplo, o VMware fornece um agente de limite que pode ser usado para VMs do Linux virtualizado usando vSphere.

Quorum e cercamento vínculos em outro conceito chamado STONITH ou solucionar a outro nó no cabeçalho. STONITH deve ter um cluster Pacemaker com suporte em todas as distribuições do Linux. Para obter mais informações, consulte [Cercamento em um Cluster de disponibilidade alta do Red Hat](https://access.redhat.com/solutions/15575) (RHEL).

#### <a name="corosyncconf"></a>corosync.conf
O `corosync.conf` arquivo contém a configuração do cluster. Ele está localizado em `/etc/corosync`. No curso normais operações diárias, esse arquivo não é necessário ser editado se o cluster está configurado corretamente.

#### <a name="cluster-log-location"></a>Local do log de cluster
Locais de log para clusters de Pacemaker diferem dependendo da distribuição.
-   RHEL e SLES- `/var/log/cluster/corosync.log`
-   Ubuntu – `/var/log/corosync/corosync.log`

Para alterar o local de log padrão, modifique `corosync.conf`.

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Clusters de Pacemaker de plano para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Esta seção discute os pontos importantes de planejamento para um cluster Pacemaker.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Clusters de virtualização Pacemaker baseados em Linux para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Usar máquinas virtuais para implantar com base em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações de grupos de disponibilidade e FCIs é coberto pelas mesmas regras de suas contrapartes baseados no Windows. Há um conjunto básico de regras para dar suporte de virtualizado [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implantações fornecidas pela Microsoft em [Microsoft suporte KB 956893](https://support.microsoft.com/en-us/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment). Hipervisores diferentes, como Hyper-V do Microsoft e ESXi do VMware podem ter diferentes variações em cima dessa, devido a diferenças nas plataformas próprios.

Quando se trata de grupos de disponibilidade e FCIs em virtualização, certifique-se de que antiafinidade está definida para os nós de um determinado cluster Pacemaker. Quando configurado para alta disponibilidade em uma configuração de grupo de disponibilidade ou FCI, as VMs hospedando [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] nunca deve estar em execução no mesmo host de hipervisor. Por exemplo, se uma FCI de dois nós for implantada, precisaria ser *pelo menos* três hosts de hipervisor para o que há em algum lugar para uma das VMs hospedando um nó para ir em caso de falha do host, especialmente se o uso de recursos, como ao vivo A migração ou vMotion.

Para obter informações mais específicas, consulte:
-   Documentação do Hyper-V – [usando Clustering convidado para alta disponibilidade](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   White paper (gravado para implantações com base no Windows, mas a maioria dos conceitos ainda se aplicam) – [planejamento altamente disponível e missão crítica implantações do SQL Server com VMware vSphere](http://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>RHEL com um cluster Pacemaker com STONITH ainda não é suportado pelo Hyper-V. Até que tenha suporte, para obter mais informações e atualizações, consulte [políticas de suporte para Clusters de disponibilidade alta RHEL](https://access.redhat.com/articles/29440#3physical_host_mixing).

### <a name="networking"></a>Rede
Ao contrário de um WSFC Pacemaker não exige um nome dedicado ou pelo menos um endereço IP dedicado para o próprio cluster Pacemaker. Grupos de disponibilidade e FCIs exigirá endereços IP (consulte a documentação de cada para obter mais informações), mas não nomes, porque não há nenhum recurso de nome de rede. SLES permitir a configuração de um endereço IP para fins de administração, mas não é necessária, como pode ser visto no [criar o cluster Pacemaker](sql-server-linux-deploy-pacemaker-cluster.md#create).

Como um WSFC Pacemaker prefere rede redundante, que significa placas de rede distintos (NICs ou pNICs para física) com endereços IP individuais. Em termos de configuração de cluster, cada endereço IP teria que é conhecido como seu próprio toque. No entanto, como com WSFCs hoje, muitas implementações virtualizadas ou na nuvem pública em que há realmente apenas um único virtualizado NIC (vNIC) apresentado para o servidor. Se todos os pNICs e vNICs estão conectados ao mesmo comutador físico ou virtual, não existe true redundância na camada de rede, para que configurar várias NICs é um pouco de uma ilusão à máquina virtual. Redundância de rede é normalmente criada no hipervisor para implantações virtualizadas e definitivamente é integrada na nuvem pública.

Uma diferença com várias NICs e Pacemaker versus um WSFC é Pacemaker permite que vários endereços IP na mesma sub-rede, e não um WSFC. Para obter mais informações sobre várias sub-redes e clusters do Linux, consulte o artigo [configurar várias sub-redes](sql-server-linux-configure-multiple-subnet.md).

### <a name="quorum-and-stonith"></a>Quorum e STONITH
Configuração de quorum e requisitos relacionados ao grupo de disponibilidade ou FCI específicos em implantações de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

STONITH é necessário para um cluster Pacemaker com suporte. Use a documentação da distribuição para configurar STONITH. Um exemplo é em [isolamento com base em armazenamento](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) para SLES. Também há um agente STONITH do VMware vCenter para soluções baseadas em ESXI. Para obter mais informações, consulte [Stonith plug-in do agente para VMWare VM VCenter SOAP de Cercamento (Unofficial)](https://github.com/olafrv/fence_vmware_soap).

> [!NOTE]
> A partir da redação deste artigo, o Hyper-V não tem uma solução para STONITH. Isso é verdadeiro para implantações de local e também afeta implantações Pacemaker baseados no Azure usando determinadas distribuições como RHEL.

### <a name="interoperability"></a>Interoperabilidade
Esta seção documenta como um cluster baseado em Linux pode interagir com um WSFC ou com outras distribuições do Linux.

#### <a name="wsfc"></a>WSFC
Atualmente, não há nenhuma maneira direta de um WSFC e um cluster Pacemaker para trabalhar juntos. Isso significa que não há nenhuma maneira de criar um grupo de disponibilidade ou FCI funciona através de um WSFC e Pacemaker. No entanto, há duas soluções de interoperabilidade, que são projetados para grupos de disponibilidade. A única maneira de que uma FCI pode participar de uma configuração de plataforma cruzada é se ela participa como uma instância em um dos dois cenários:
-   Um grupo de disponibilidade com um tipo de cluster de None. Para obter mais informações, consulte o Windows [documentação dos grupos de disponibilidade](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).
-   Um AG distribuída, que é um tipo especial de grupo de disponibilidade que permite que dois grupos de disponibilidade diferentes a ser configurado como seu próprio grupo de disponibilidade. Para obter mais informações sobre grupos de disponibilidade distribuídas, consulte a documentação [grupos de disponibilidade distribuída](../database-engine/availability-groups/windows/distributed-availability-groups.md).

#### <a name="other-linux-distributions"></a>Outras distribuições do Linux
No Linux, todos os nós de um cluster de Pacemaker devem ser no mesmo de distribuição. Por exemplo, isso significa que um nó RHEL não pode ser parte de um cluster de Pacemaker que tem um nó SLES. O principal motivo para isso foi mencionado anteriormente: as distribuições podem ter diferentes versões e funcionalidades, então as coisas podem não funcionar corretamente. Combinação de distribuições tem o mesmo texto como misturar WSFCs e Linux: usar nenhum ou distribuído grupos de disponibilidade.

## <a name="next-steps"></a>Próximas etapas
[Implantar um cluster de Pacemaker para o SQL Server no Linux](sql-server-linux-deploy-pacemaker-cluster.md)
