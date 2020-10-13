---
title: Instâncias de cluster de failover – SQL Server em Linux
description: Os conceitos das instâncias de cluster de failover do SQL Server em Linux incluem a camada de clustering, o número de instâncias, o endereço IP e o nome e o armazenamento compartilhado.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 1b2b852a1c1acecefa3b702bb140d9128d04a212
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784643"
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>Instâncias de cluster de failover – SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo explica os conceitos relacionados a FCI (instâncias de cluster de failover) do SQL Server no Linux. 

Para criar FCI do SQL Server no Linux, confira [Configurar FCI do SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>A Camada de Clustering

* Em RHEL, a camada de clustering baseia-se no [complemento de HA](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) do RHEL (Red Hat Enterprise Linux). 

    > [!NOTE] 
    > O acesso ao complemento de HA do Red Hat e à documentação exige uma assinatura. 

* No SLES, a camada de clustering baseia-se na [HAE (Extensão de Alta Disponibilidade)](https://www.suse.com/products/highavailability) do SUSE Linux Enterprise.

    Para obter mais informações sobre configuração de cluster, opções do agente de recursos, gerenciamento, melhores práticas e recomendações, confira a [Extensão de Alta Disponibilidade do SUSE Linux Enterprise 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

O complemento de HA RHEL e o HAE do SUSE são criados no [Pacemaker](https://clusterlabs.org/).

Como mostra o diagrama a seguir, o armazenamento é apresentado a dois servidores. Os componentes de clustering – Corosync e Pacemaker – coordenam a comunicação e o gerenciamento de recursos. Um dos servidores tem a conexão ativa com os recursos de armazenamento e o SQL Server. Quando o Pacemaker detecta uma falha, os componentes de clustering gerenciam a movimentação dos recursos para o outro nó.  

![Cluster SQL de disco compartilhado do Red Hat Enterprise Linux 7](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> Neste ponto, a integração do SQL Server com o Pacemaker em Linux não está tão acoplada quanto a do WSFC em Windows. No SQL, não há nenhum conhecimento sobre a presença do cluster, toda a orquestração ocorre de fora para dentro e o serviço é controlado como uma instância autônoma pelo Pacemaker. Além disso, o nome da rede virtual é específico do WSFC; não há equivalente ao mesmo no Pacemaker. Espera-se que @@servername e o sys.servers retornem o nome do nó, enquanto o cluster dmvs sys.dm_os_cluster_nodes e sys.dm_os_cluster_properties não retornarão registros. Para usar uma cadeia de conexão que aponta para um nome do servidor de cadeia de caracteres e não usar o IP, elas precisarão se registrar no servidor DNS o IP usado para criar o recurso de IP virtual (conforme explicado nas seções a seguir) com o nome do servidor escolhido.

## <a name="number-of-instances-and-nodes"></a>Número de instâncias e nós

Uma diferença importante com SQL Server em Linux é que só pode haver uma instalação de SQL Server por servidor Linux. Essa instalação é chamada de instância. Isso significa que, diferentemente do Windows Server, que dá suporte a até 25 FCIs por WSFC (cluster de failover do Windows Server), um FCI baseado em Linux terá apenas uma única instância. Essa instância também é uma instância padrão. Não há nenhum conceito de uma instância nomeada no Linux. 

Um cluster do Pacemaker só pode ter até 16 nós quando o Corosync está envolvido, de modo que um único FCI pode abranger até 16 servidores. Um FCI implementado com a Standard Edition do SQL Server dá suporte a até dois nós de um cluster, mesmo que o cluster do Pacemaker tenha o máximo de 16 nós.

Em uma FCI do SQL Server, a Instância do SQL Server está ativa em um nó ou no outro.

## <a name="ip-address-and-name"></a>Nome e Endereço IP
Em um cluster do Pacemaker do Linux, cada FCI do SQL Server precisa de seu próprio endereço IP e nome exclusivos. Se a configuração do FCI abranger várias sub-redes, um endereço IP será necessário por sub-rede. O nome exclusivo e os endereços IP são usados para acessar a FCI de modo que os aplicativos e os usuários finais não precisam ter conhecimento do servidor subjacente do cluster do Pacemaker.

O nome da FCI no DNS deve ser igual ao nome do recurso da FCI criado no cluster do Pacemaker.
O nome e o endereço IP devem ser registrados no DNS.

## <a name="shared-storage"></a>Armazenamento compartilhado
Todas as FCIs, estejam no Linux ou no Windows Server, exigem alguma forma de armazenamento compartilhado. Esse armazenamento é apresentado a todos os servidores que podem hospedar a FCI, mas apenas um único servidor pode usar o armazenamento para a FCI em um determinado momento. As opções disponíveis para o armazenamento compartilhado no Linux são:

- iSCSI
- NFS (sistema de arquivos de rede)
- Protocolo SMB. No Windows Server, há opções ligeiramente diferentes. Uma opção que atualmente não é compatível com FCIs baseadas em Linux é a capacidade de usar um disco local para o nó para TempDB, que é o workspace temporário do SQL Server.

Em uma configuração que abrange vários locais, o que é armazenado em um data center deve ser sincronizado com o outro. No caso de um failover, a FCI poderá ficar online e o armazenamento será visto como o mesmo. Conseguir isso exigirá um método externo para replicação de armazenamento, seja ele feito por meio do hardware de armazenamento subjacente ou por algum utilitário baseado em software. 

>[!NOTE]
>Para SQL Server, as implantações baseadas em Linux usando discos apresentados diretamente a um servidor devem ser formatadas com XFS ou EXT4. No momento, não há suporte para outros sistemas de arquivos. Todas as alterações serão refletidas aqui.

O processo para apresentar o armazenamento compartilhado é o mesmo para os diferentes métodos compatíveis:

- Configurar o armazenamento compartilhado
- Monte o armazenamento como uma pasta nos servidores que servirão como nós do cluster do Pacemaker para a FCI
- Se necessário, mova os bancos de dados do sistema do SQL Server para o armazenamento compartilhado
- Testar se o SQL Server funciona de cada servidor conectado ao armazenamento compartilhado

Uma grande diferença com o SQL Server em Linux é que, embora você possa configurar a localização do arquivo de log e dos dados do usuário padrão, os bancos de dados do sistema sempre devem existir em `/var/opt/mssql/data`. No Windows Server, é possível mover os bancos de dados do sistema, incluindo TempDB. Isso afeta o modo como o armazenamento compartilhado é configurado para uma FCI.

Os caminhos padrão para bancos de dados que não do sistema podem ser alterados usando o utilitário `mssql-conf`. Para obter informações sobre como alterar os padrões, [Altere a localização do diretório de dados ou de log padrão](sql-server-linux-configure-mssql-conf.md#datadir). Você também pode armazenar dados e transações do SQL Server em outras localizações, contanto que tenham a segurança apropriada, mesmo que não seja uma localização padrão; a localização precisaria ser declarada.

Os tópicos a seguir explicam como configurar tipos de armazenamento compatíveis para uma FCI do SQL Server baseada em Linux:

- [Configurar a instância de cluster de failover – iSCSI – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Configurar a instância de cluster de failover – NFS – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Configurar a instância de cluster de failover – SMB – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
