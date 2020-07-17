---
title: Alta disponibilidade do SQL Server para implantações do Linux
description: Saiba mais sobre as opções de alta disponibilidade para o SQL Server em Linux, como os grupos de disponibilidade Always On, as FCIs (instâncias de cluster de failover) e o envio de logs.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 67a5219e955ccd9d4b0303276823d8cafbce4963
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196835"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Noções básicas de disponibilidade do SQL Server para implantações do Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Começando com o [!INCLUDE[sssql17-md](../includes/sssql17-md.md)], o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] é compatível no Linux e no Windows. Como as implantações do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] baseadas no Windows, os bancos de dados e as instâncias do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] precisam estar altamente disponíveis no Linux. Este artigo aborda os aspectos técnicos do planejamento e da implantação de instâncias e bancos de dados do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] baseados no Linux altamente disponíveis, bem como algumas das diferenças das instalações baseadas no Windows. Como o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pode ser novo para profissionais do Linux e o Linux pode ser novo para profissionais do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], às vezes, o artigo apresenta conceitos que podem ser familiares para alguns e desconhecidos para outros.

## <a name="ssnoversion-md-availability-options-for-linux-deployments"></a>Opções de disponibilidade do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para implantações do Linux
Além de backup e restauração, os mesmos três recursos de disponibilidade estão disponíveis no Linux como nas implantações baseadas no Windows:
-   AGs (Grupos de Disponibilidade) Always On
-   FCIs (Instâncias do cluster de failover) do Always On
-   [Envio de log](sql-server-linux-use-log-shipping.md)

No Windows, as FCIs exigem sempre um WSFC (cluster de failover do Windows Server) subjacente. Dependendo do cenário de implantação, um AG geralmente exige um WSFC subjacente, com a exceção sendo a nova variante None no [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Um WSFC não existe no Linux. A implementação de clustering no Linux é discutida na seção [Pacemaker para Grupos de Disponibilidade Always On e instâncias de cluster de failover no Linux](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux).

## <a name="a-quick-linux-primer"></a>Um rápido manual do Linux
Embora algumas instalações do Linux possam ser realizadas com uma interface, a maioria não pode. Isso significa que quase tudo na camada do sistema operacional é feito por meio da linha de comando. O termo comum para essa linha de comando no mundo Linux é um *shell de Bash*.

No Linux, muitos comandos precisam ser executados com privilégios elevados, como muitas ações que precisam ser feitas no Windows Server como administrador. Há dois métodos principais a serem executados com privilégios elevados:
1. Execute no contexto do usuário apropriado. Para alterar para outro usuário, use o comando `su`. Se `su` for executado por conta própria sem um nome de usuário, desde que você saiba a senha, agora você estará em um shell como *raiz*.
   
2. A maneira mais comum e segura de executar ações é usar `sudo` antes de executar qualquer coisa. Muitos dos exemplos neste artigo usam `sudo`.

Alguns comandos comuns, cada um com vários comutadores e opções que podem ser pesquisados online:
-   `cd` – alterar o diretório
-   `chmod` – alterar as permissões de um arquivo ou diretório
-   `chown` – alterar as propriedade de um arquivo ou diretório
-   `ls` – mostrar o conteúdo de um diretório
-   `mkdir` – criar uma pasta (diretório) em uma unidade
-   `mv` – mover um arquivo de uma localização para outra
-   `ps` – mostrar todos os processos de trabalho
-   `rm` – excluir um arquivo localmente em um servidor
-   `rmdir` – excluir uma pasta (diretório)
-   `systemctl` – iniciar, parar ou habilitar serviços
-   Comandos do editor de texto. No Linux, há várias opções de editor de texto, como vi e emacs.

## <a name="common-tasks-for-availability-configurations-of-ssnoversion-md-on-linux"></a>Tarefas comuns de configurações de disponibilidade do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux
Esta seção aborda as tarefas comuns a todas as implantações do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] baseadas no Linux.

### <a name="ensure-that-files-can-be-copied"></a>Verifique se os arquivos podem ser copiados
Copiar arquivos de um servidor para outro é uma tarefa que qualquer pessoa que use o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux deve ser capaz de fazer. Essa tarefa é muito importante para as configurações do AG.

Aspectos como problemas de permissão podem existir no Linux, bem como em instalações baseadas no Windows. No entanto, aqueles familiarizados com a cópia do servidor para o servidor no Windows podem não saber como isso ele é feito no Linux. Um método comum é usar o utilitário `scp` de linha de comando, que representa a cópia segura. Nos bastidores, `scp` o usa o OpenSSH. SSH significa Secure Shell. Dependendo da distribuição do Linux, o OpenSSH pode não estar instalado. Se não estiver, o OpenSSH precisará ser instalado primeiro. Para obter mais informações sobre como configurar o OpenSSH, confira as informações nos links a seguir para cada distribuição:
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/ch-openssh)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Ao usar `scp`, você deverá fornecer as credenciais do servidor se ele não for a origem ou o destino. Por exemplo, usando

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

copia o arquivo MyAGCert.cer para a pasta especificada no outro servidor. Observe que você deve ter permissões e, possivelmente, a propriedade do arquivo para copiá-lo. Portanto, `chown` também pode precisar ser empregado antes da cópia. De modo semelhante, no lado de recebimento, o usuário certo precisa de acesso para manipular o arquivo. Por exemplo, para restaurar esse arquivo de certificado, o usuário `mssql` deve ser capaz de acessá-lo.

Samba, que é a variante do Linux do protocolo SMB, também pode ser usado para criar compartilhamentos acessados por caminhos UNC, como `\\SERVERNAME\SHARE`. Para obter mais informações sobre como configurar Samba, confira as informações nos links a seguir para cada distribuição:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

Os compartilhamentos SMB baseados no Windows também podem ser usados; os compartilhamentos SMB não precisam ser baseados no Linux, desde que a parte do cliente do Samba esteja configurada corretamente no servidor Linux que hospeda [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e o compartilhamento tenha o acesso certo. Para aqueles em um ambiente misto, essa seria uma maneira de aproveitar a infraestrutura existente para implantações do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] baseadas no Linux.

Um aspecto importante é que a versão do Samba implantada deve estar em conformidade com SMB 3.0. Quando o suporte a SMB foi adicionado no [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], ele exigia que todos os compartilhamentos fossem compatíveis com o SMB 3.0. Se estiver usando o Samba para o compartilhamento, e não para o Windows Server, o compartilhamento baseado no Samba deverá usar o Samba 4.0 ou posterior e, idealmente, 4.3 ou posterior, que é compatível com o SMB 3.1.1. Uma boa fonte de informações sobre SMB e Linux é [SMB3 in Samba](https://events.static.linuxfound.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf).

Por fim, o uso de um compartilhamento NFS (Network File System) é uma opção. Usar o NFS não é uma opção em implantações do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] baseadas no Windows e só pode ser usado para implantações baseadas no Linux.

### <a name="configure-the-firewall"></a>Configurar o firewall
Semelhantes ao Windows, as distribuições do Linux têm um firewall interno. Se a sua empresa estiver usando um firewall externo para os servidores, a desabilitação dos firewalls no Linux poderá ser aceitável. No entanto, independentemente de onde o firewall está habilitado, as portas precisam estar abertas. A tabela a seguir documenta as portas comuns necessárias para implantações do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] altamente disponíveis no Linux.

| Número da porta | Type     | Descrição                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS – `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (se usado) – Mapeador de ponto de extremidade                                                                                          |
| 137         | UDP      | Samba (se usado) – Serviço de nome NetBIOS                                                                                      |
| 138         | UDP      | Samba (se usado) – Datagrama NetBIOS                                                                                          |
| 139         | TCP      | Samba (se usado) – Sessão NetBIOS                                                                                           |
| 445         | TCP      | Samba (se usado) – SMB sobre TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] – porta padrão; se desejar, pode mudar com `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP, UDP | NFS (se usado)                                                                                                               |
| 2224        | TCP      | Pacemaker – usado por `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker – Obrigatório se houver nós remotos do Pacemaker                                                                    |
| 3260        | TCP      | Iniciador iSCSI (se usado) – Pode ser alterado em `/etc/iscsi/iscsid.config` (RHEL), mas deve corresponder à porta do destino iSCSI |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] – porta padrão usada para um ponto de extremidade do AG; pode ser alterada ao criar o ponto de extremidade                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker – Exigido por Corosync se estiver usando o UDP multicast                                                                     |
| 5405        | UDP      | Pacemaker – Exigido por Corosync                                                                                            |
| 21064       | TCP      | Pacemaker – Exigido pelos recursos que usam a DLM                                                                                 |
| Variável    | TCP      | Porta do ponto de extremidade do AG; o padrão é 5022                                                                                           |
| Variável    | TCP      | NFS – porta para `LOCKD_TCPPORT` (encontrada em `/etc/sysconfig/nfs` no RHEL)                                              |
| Variável    | UDP      | NFS – porta para `LOCKD_UDPPORT` (encontrada em `/etc/sysconfig/nfs` no RHEL)                                              |
| Variável    | TCP/UDP  | NFS – porta para `MOUNTD_PORT` (encontrada em `/etc/sysconfig/nfs` no RHEL)                                                |
| Variável    | TCP/UDP  | NFS – porta para `STATD_PORT` (encontrada em `/etc/sysconfig/nfs` no RHEL)                                                 |

Para portas adicionais que podem ser usadas pelo Samba, confira [Uso de porta do Samba](https://wiki.samba.org/index.php/Samba_Port_Usage).

Por outro lado, o nome do serviço no Linux também pode ser adicionado como uma exceção, em vez da porta; por exemplo, `high-availability` para Pacemaker. Confira sua distribuição para obter os nomes se essa for a direção que você deseja buscar. Por exemplo, no RHEL, o comando a ser adicionado no Pacemaker é

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**Documentação do firewall:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-ssnoversion-md-packages-for-availability"></a>Instalar pacotes do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para disponibilidade
Em uma instalação do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] baseada no Windows, alguns componentes são instalados mesmo em uma instalação básica do mecanismo, enquanto outros não são. No Linux, somente o mecanismo do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] é instalado como parte do processo de instalação. Tudo o mais é opcional. Para instâncias do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] altamente disponíveis no Linux, dois pacotes devem ser instalados com o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent (*mssql-server-agent*) e o pacote de HA (alta disponibilidade) (*mssql-server-ha*). Embora o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent seja tecnicamente opcional, ele é o agendador do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para trabalhos e é exigido pelo envio de logs, portanto, a instalação é recomendada. Em instalações baseadas no Windows, o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent não é opcional.

>[!NOTE]
>Para os iniciantes no [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent é o agendador de trabalho interno do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. É uma maneira comum de os DBAs agendarem ações como backups e outras manutenções do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Ao contrário de uma instalação do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] baseada no Windows, em que o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent é um serviço completamente diferente, no Linux, o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent é executado no contexto do próprio [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

Quando AGs ou FCIs são configurados em uma configuração baseada no Windows, eles têm reconhecimento de cluster. O reconhecimento de cluster significa que o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] tem DLLs de recurso específicas que um WSFC conhece (sqagtres.dll e sqsrvres.dll para FCIs, hadrres.dll para AGs) e são usadas pelo WSFC para garantir que a funcionalidade clusterizada do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] esteja ativa, em execução e funcionando corretamente. Como o clustering é externo não apenas ao [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] como ao próprio Linux, a Microsoft teve de codificar o equivalente a uma DLL de recurso para implantações de FCI e AG baseadas no Linux. Esse é o pacote *mssql-server-ha*, também conhecido como agente de recurso do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para o Pacemaker. Para instalar o pacote *mssql-server-ha*, confira [Instalar os pacotes de HA e do SQL Server Agent](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages).

Os outros pacotes opcionais para o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux, Pesquisa de Texto Completo do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] (*mssql-server-fts*) e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-is*), não são necessários para alta disponibilidade, seja para uma FCI ou um AG.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Pacemaker para Grupos de Disponibilidade Always On e instâncias de cluster de failover no Linux
Conforme observado anteriormente, o único mecanismo de clustering com suporte no momento pela Microsoft para AGs e FCIs é o Pacemaker com Corosync. Esta seção aborda as informações básicas para entender a solução, bem como planejar e implantá-la em configurações do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

### <a name="ha-add-onextension-basics"></a>Noções básicas de complemento/extensão de HA
Todas as distribuições com suporte no momento enviam um complemento/extensão de alta disponibilidade, que se baseia na pilha de clustering do Pacemaker. Essa pilha incorpora dois componentes principais: Pacemaker e Corosync. Todos os componentes da pilha são:
-   Pacemaker – O componente de clustering principal, que realiza ações como coordenar entre as máquinas clusterizadas.
-   Corosync – Uma estrutura e um conjunto de APIs que fornecem itens como quorum, a capacidade de reiniciar processos com falha e assim por diante.
-   libQB – Fornece itens como registro em log.
-   Agente de recursos – Funcionalidade específica fornecida para que um aplicativo possa ser integrado ao Pacemaker.
-   Agente de isolamento – Scripts/funcionalidade que ajudam a isolar nós e lidar com eles se estiverem tendo problemas.
    
> [!NOTE]
> A pilha de cluster é normalmente conhecida como Pacemaker no mundo Linux.

Essa solução é, de alguma forma, semelhante à implantação de configurações clusterizadas usando o Windows, mas diferente de várias maneiras. No Windows, a forma de disponibilidade de clustering, chamada de WSFC (cluster de failover do Windows Server), é incorporada ao sistema operacional e o recurso que permite a criação de um WSFC, clustering de failover, é desabilitado por padrão. No Windows, os AGs e as FCIs são criados sobre um WSFC e compartilham uma forte integração devido à DLL de recurso específica fornecida pelo [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Essa solução totalmente acoplada é possível, de modo geral, por ser toda de um único fornecedor.

![Noções básicas de HA](./media/sql-server-linux-ha-basics/image1.png)

No Linux, embora cada distribuição com suporte tenha o Pacemaker disponível, cada distribuição pode personalizar e ter implementações e versões ligeiramente diferentes. Algumas das diferenças serão refletidas nas instruções neste artigo. A camada de clustering é de software livre, portanto, embora seja fornecida com as distribuições, ela não é totalmente integrada da mesma maneira que um WSFC está sob o Windows. Por esse motivo, a Microsoft fornece *mssql-server-ha*, de modo que o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e a pilha do Pacemaker possam fornecer quase, mas não exatamente, a mesma experiência para AGs e FCIs como no Windows.

Para obter a documentação completa sobre o Pacemaker, incluindo uma explicação mais detalhada de tudo, com informações de referência completa, para RHEL e SLES:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

O Ubuntu não tem um guia para a disponibilidade.

Para obter mais informações sobre a pilha inteira, confira também a [página de documentação oficial do Pacemaker](https://clusterlabs.org/doc/) no site do Clusterlabs.

### <a name="pacemaker-concepts-and-terminology"></a>Conceitos e terminologia do Pacemaker
Esta seção documenta os conceitos e a terminologia comuns de uma implementação do Pacemaker.

#### <a name="node"></a>Nó
Um nó é um servidor que participa do cluster. Um cluster do Pacemaker dá suporte nativo a até 16 nós. Esse número poderá ser excedido se Corosync não estiver em execução em nós adicionais, mas Corosync for necessário para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Portanto, o número máximo de nós que um cluster pode ter para qualquer configuração baseada no [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] é 16; esse é o limite do Pacemaker e não tem nada a ver com as limitações máximas para AGs ou FCIs impostas pelo [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. 

#### <a name="resource"></a>Recurso
Um WSFC e um cluster do Pacemaker têm o conceito de um recurso. Um recurso é uma funcionalidade específica que é executada no contexto do cluster, como um disco ou um endereço IP. Por exemplo, no Pacemaker, os recursos de FCI e AG podem ser criados. Isso não é diferente do que é feito em um WSFC, no qual você vê um recurso do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para um recurso de FCI ou um AG ao configurar um AG, mas não é exatamente o mesmo devido às diferenças subjacentes em como o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] integra-se ao Pacemaker.

O Pacemaker tem recursos padrão e de clone. Os recursos de clone são aqueles executados simultaneamente em todos os nós. Um exemplo seria um endereço IP que é executado em vários nós para fins de balanceamento de carga. Qualquer recurso criado para FCIs usa um recurso padrão, já que apenas um nó pode hospedar uma FCI em um determinado momento.

[!INCLUDE [bias-sensitive-term-t](../includes/bias-sensitive-term-t.md)]

Quando um AG é criado, ele requer uma forma especializada de um recurso de clone chamado de recurso de vários estados. Embora um AG tenha apenas uma réplica primária, o AG em si está em execução em todos os nós em que está configurado para trabalhar e pode, potencialmente, permitir ações como o acesso somente leitura. Como esse é um uso "dinâmico" do nó, os recursos têm o conceito de dois estados: mestre e subordinado. Para obter mais informações, confira [Recursos de vários estados: recursos que têm vários modos](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html).

#### <a name="resource-groupssets"></a>Grupos/conjuntos de recursos

Semelhante às funções em um WSFC, um cluster do Pacemaker tem o conceito de um grupo de recursos. Um grupo de recursos (chamado de _conjunto_ no SLES) é uma coleção de recursos que funcionam juntos e podem fazer failover de um nó para outro como uma só unidade. Grupos de recursos não podem conter recursos configurados como mestre nem subordinado. Portanto, eles não podem ser usados para AGs. Embora um grupo de recursos possa ser usado para FCIs, esta geralmente não é uma configuração recomendada.

#### <a name="constraints"></a>Restrições
WSFCs têm vários parâmetros para recursos, bem como dependências, que dizem ao WSFC de uma relação pai/filho entre dois recursos diferentes. Uma dependência é apenas uma regra que informa ao WSFC qual recurso precisa estar online primeiro.

Um cluster do Pacemaker não tem o conceito de dependências, mas há restrições. Há três tipos de restrições: colocação, localização e ordenação.
-   Uma restrição de colocação impõe se dois recursos devem ou não ser executados no mesmo nó.
-   Uma restrição de localização informa ao cluster do Pacemaker onde um recurso pode (ou não pode) ser executado.
-   Uma restrição de ordenação informa ao cluster do Pacemaker a ordem em que os recursos devem iniciar.

> [!NOTE]
> Restrições de colocação não são necessárias para recursos em um grupo de recursos, pois todas elas são vistas como uma única unidade.

#### <a name="quorum-fence-agents-and-stonith"></a>Quorum, agentes de isolamento e STONITH
O quorum no Pacemaker é um pouco semelhante a um WSFC em conceito. A finalidade total de um mecanismo de quorum do cluster é garantir que o cluster permaneça ativo e em execução. Tanto o WSFC quanto os complementos de HA para as distribuições do Linux têm o conceito de votação, em que cada nó conta para o quorum. Você quer a maioria dos votos, caso contrário, em um cenário desfavorável, o cluster será desligado.

Ao contrário de um WSFC, não há nenhum recurso de testemunha para trabalhar com o quorum. Como um WSFC, a meta é manter o número de eleitores ímpares. A configuração de quorum tem considerações diferentes para AGs e FCIs.

WSFCs monitoram o status dos nós participantes e os manipulam quando ocorre um problema. As versões posteriores do WSFCs oferecem recursos como colocar em quarentena um nó que está inadequado ou não disponível (o nó não está ativado, a comunicação de rede está inoperante etc.). No lado do Linux, esse tipo de funcionalidade é fornecido por um agente de isolamento. Às, vezes, o conceito é chamado de isolamento. No entanto, esses agentes de isolamento geralmente são específicos para a implantação e, em geral, fornecidos por fornecedores de hardware e alguns fornecedores de software, como aqueles que fornecem hipervisores. Por exemplo, a VMware fornece um agente de isolamento que pode ser usado para VMs Linux virtualizadas usando vSphere.

O quorum e o isolamento vinculam-se a outro conceito chamado STONITH, Shoot the Other Node in the Head. STONITH é necessário para ter um cluster do Pacemaker com suporte em todas as distribuições do Linux. Para obter mais informações, confira [Isolamento em um cluster de alta disponibilidade da Red Hat](https://access.redhat.com/solutions/15575) (RHEL).

#### <a name="corosyncconf"></a>corosync.conf
O arquivo `corosync.conf` contém a configuração do cluster. Ele está localizado em `/etc/corosync`. No decorrer das operações normais do dia a dia, esse arquivo nunca deverá ser editado se o cluster estiver configurado corretamente.

#### <a name="cluster-log-location"></a>Localização do log do cluster
Os locais de log para clusters do Pacemaker diferem dependendo da distribuição.
-   RHEL e SLES – `/var/log/cluster/corosync.log`
-   Ubuntu – `/var/log/corosync/corosync.log`

Para alterar a localização padrão do registro em log, modifique `corosync.conf`.

## <a name="plan-pacemaker-clusters-for-ssnoversion-md"></a>Planejar clusters do Pacemaker para o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Esta seção aborda os pontos de planejamento importantes para um cluster do Pacemaker.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-ssnoversion-md"></a>Virtualização de clusters do Pacemaker baseados no Linux para o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
O uso de máquinas virtuais para implantar implantações do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] baseadas no Linux para AGs e FCIs é coberto pelas mesmas regras que as de suas contrapartes baseadas no Windows. Há um conjunto básico de regras para a compatibilidade de implantações do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] virtualizadas fornecidas pela Microsoft no [Suporte da Microsoft KB 956893](https://support.microsoft.com/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment). Hipervisores diferentes, como o Hyper-V da Microsoft e o ESXi da VMware, podem ter variações diferentes sobre isso, devido a diferenças nas próprias plataformas.

Quando se trata de AGs e FCIs em virtualização, verifique se a antiafinidade está definida para os nós de um determinado cluster do Pacemaker. Quando configuradas para alta disponibilidade em uma configuração de AG ou FCI, as VMs que hospedam o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] nunca devem estar em execução no mesmo host de hipervisor. Por exemplo, se uma FCI de dois nós for implantada, serão necessários *pelo menos* três hosts de hipervisor para que haja algum lugar para que uma das VMs que hospeda um nó continue no caso de uma falha de host, especialmente se estiver usando recursos como Migração ao Vivo ou vMotion.

Para obter mais especificações, confira:
-   Documentação do Hyper-V – [Uso de clustering de convidado para alta disponibilidade](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   White paper (escrito para implantações baseadas no Windows, mas a maior parte dos conceitos ainda se aplica) – [Planejamento de implantações do SQL Server críticas e altamente disponíveis com VMware vSphere](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

### <a name="networking"></a>Rede
Ao contrário de um WSFC, o Pacemaker não requer um nome dedicado ou pelo menos um endereço IP dedicado para o próprio cluster do Pacemaker. AGs e FCIs exigirão endereços IP (consulte a documentação de cada um para obter mais informações), mas não nomes, já que não há nenhum recurso de nome da rede. O SLES permite a configuração de um endereço IP para fins de administração, mas não é necessário, como pode ser visto em [Criar o cluster do Pacemaker](sql-server-linux-deploy-pacemaker-cluster.md#create).

Como um WSFC, o Pacemaker preferiria a rede redundante, o que significa que placas de rede distintas (NICs ou pNICs para físico) com endereços IP individuais. Em termos da configuração do cluster, cada endereço IP teria o que é conhecido como seu próprio anel. No entanto, assim como com o WSFCs hoje, muitas implementações são virtualizadas ou na nuvem pública em que há apenas uma vNIC (NIC virtualizada única) apresentada ao servidor. Se todas as pNICs e vNICs estiverem conectadas ao mesmo comutador virtual ou físico, não haverá nenhuma redundância real na camada de rede, portanto, configurar várias NICs é um pouco de uma ilusão para a máquina virtual. A redundância de rede geralmente é incorporada ao hipervisor para implantações virtualizadas e, definitivamente, é incorporada à nuvem pública.

Uma diferença com várias NICs e o Pacemaker versus um WSFC é que o Pacemaker permite vários endereços IP na mesma sub-rede, enquanto um WSFC não permite. Para obter mais informações sobre várias sub-redes e clusters do Linux, confira o artigo [Configurar várias sub-redes](sql-server-linux-configure-multiple-subnet.md).

### <a name="quorum-and-stonith"></a>Quorum e STONITH
A configuração de quorum e os requisitos estão relacionados a implantações específicas do AG ou da FCI do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

STONITH é necessário para um cluster do Pacemaker com suporte. Use a documentação da distribuição para configurar o STONITH. Um exemplo está no [Isolamento baseado em armazenamento](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) para SLES. Também há um agente STONITH para soluções baseadas no VMware vCenter para ESXi. Para obter mais informações, confira [Agente do plug-in Stonith para isolamento SOAP do VMWare VM VCenter (não oficial)](https://github.com/olafrv/fence_vmware_soap).

### <a name="interoperability"></a>Interoperabilidade
Esta seção documenta como um cluster baseado no Linux pode interagir com um WSFC ou com outras distribuições do Linux.

#### <a name="wsfc"></a>WSFC
Atualmente, não existe maneira direta para um WSFC e um cluster do Pacemaker funcionarem juntos. Isso significa que não há como criar um AG ou uma FCI que funcione em um WSFC e em um Pacemaker. No entanto, há duas soluções de interoperabilidade, ambas projetadas para AGs. A única maneira de uma FCI poder participar de uma configuração multiplataforma é se ela estiver participando como uma instância em um destes dois cenários:
-   Um AG com um tipo de cluster Nenhum. Para obter mais informações, confira a [documentação dos grupos de disponibilidade](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) do Windows.
-   Um AG distribuído, que é um tipo especial de grupo de disponibilidade que permite que dois AGs diferentes sejam configurados como seu próprio grupo de disponibilidade. Para obter mais informações sobre AGs distribuídos, confira a documentação [Grupos de disponibilidade distribuídos](../database-engine/availability-groups/windows/distributed-availability-groups.md).

#### <a name="other-linux-distributions"></a>Outras distribuições do Linux
No Linux, todos os nós de um cluster do Pacemaker devem estar na mesma distribuição. Por exemplo, isso significa que um nó RHEL não pode fazer parte de um cluster do Pacemaker que tem um nó SLES. O principal motivo para isso foi declarado anteriormente: as distribuições podem ter diferentes versões e funcionalidades, portanto, as ações não podiam funcionar corretamente. A combinação de distribuições tem a mesma história que a combinação de WSFCs e Linux: use Nenhum ou AGs distribuídos.

## <a name="next-steps"></a>Próximas etapas
[Implantar um cluster do Pacemaker para o SQL Server em Linux](sql-server-linux-deploy-pacemaker-cluster.md)
