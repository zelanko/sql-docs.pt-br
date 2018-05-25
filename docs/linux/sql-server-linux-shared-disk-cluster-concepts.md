---
title: Instâncias de Cluster de failover - SQL Server no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 0275d0004bc02f1e32e7da3630c8a0bd15532d18
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>Instâncias de Cluster de failover - SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica os conceitos relacionados a instâncias de cluster de failover do SQL Server (FCI) no Linux. 

Para criar um FCI do SQL Server no Linux, consulte [FCI configurar SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>A camada de Clustering

* RHEL, a camada do cluster é baseada no Red Hat Enterprise Linux (RHEL) [HA complemento](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf). 

    > [!NOTE] 
    > Acesso ao complemento Red Hat HA e documentação requer uma assinatura. 

* SLES, a camada do cluster é baseada em SUSE Linux Enterprise [alta disponibilidade extensão (HAE)](https://www.suse.com/products/highavailability).

    Para obter mais informações sobre a configuração de cluster, opções do recurso de agente, gerenciamento, as práticas recomendadas e recomendações, consulte [SUSE Linux Enterprise alta disponibilidade extensão 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

O complemento RHEL HA e o SUSE HAE são criados na [Pacemaker](http://clusterlabs.org/).

Como mostra o diagrama a seguir, o armazenamento é apresentado a dois servidores. Componentes de clusters - Corosync e Pacemaker - coordenam a comunicação e gerenciamento de recursos. Um dos servidores tem a conexão ativa os recursos de armazenamento e o SQL Server. Quando Pacemaker detecta uma falha de componentes de clusters gerenciam mover os recursos para o outro nó.  

![Red Hat Enterprise Linux 7 compartilhado de Cluster de disco do SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> Neste ponto, a integração do SQL Server com Pacemaker no Linux não é como acoplada como com o WSFC no Windows. De dentro do SQL, não há nenhum conhecimento sobre a presença do cluster, orquestração todas as está fora de e o serviço é controlado como uma instância autônoma por Pacemaker. Além disso, o nome de rede virtual é específico para o WSFC, não há nenhum equivalente do mesmo em Pacemaker. É esperado que @@servername e sys para retornar o nome do nó, enquanto o sys.DM os_cluster_nodes dmvs de cluster e dm_os_cluster_properties não serão nenhum registro. Para usar uma cadeia de caracteres de conexão que aponta para um nome de servidor de cadeia de caracteres e não usar o IP, será necessário registrar o IP usado para criar o recurso IP virtual (conforme explicado nas seções a seguir) no seu servidor DNS com o nome de servidor escolhido.

## <a name="number-of-instances-and-nodes"></a>Número de instâncias e nós

Uma das principais diferenças com o SQL Server no Linux é que pode haver somente uma instalação do SQL Server por servidor Linux. Essa instalação é chamada de uma instância. Isso significa que ao contrário do Windows Server que dá suporte a até 25 FCIs por cluster de failover do Windows Server (WSFC), uma FCI baseados em Linux somente terá uma única instância. Esta instância de um também é uma instância padrão; Não há nenhum conceito de uma instância nomeada no Linux. 

Um cluster Pacemaker só pode ter até 16 nós quando Corosync estiver envolvido, para que um único FCI pode abranger até 16 servidores. Uma FCI implementada com a Standard Edition do SQL Server dá suporte a até dois nós de um cluster mesmo se o cluster Pacemaker tem o máximo de 16 nós.

Em uma FCI do SQL Server, a instância do SQL Server está ativa em um nó ou em outro.

## <a name="ip-address-and-name"></a>Nome e endereço IP
Em um cluster do Linux Pacemaker, cada FCI do SQL Server precisa de seu próprio endereço IP exclusivo e nome. Se a configuração de FCI se estender por várias sub-redes, um endereço IP será necessário por sub-rede. O nome exclusivo e endereços IP são usados para acessar a FCI para que aplicativos e usuários finais não precisa saber qual servidor subjacente do cluster Pacemaker.

O nome da FCI no DNS deve ser igual ao nome do recurso FCI que é criado no cluster Pacemaker.
O nome e o endereço IP devem ser registrados no DNS.

## <a name="shared-storage"></a>Armazenamento compartilhado
Todas as FCIs, estejam eles em Linux ou Windows Server, exigem algum tipo de armazenamento compartilhado. Esse armazenamento é apresentado para todos os servidores que possivelmente podem hospedar a FCI, mas apenas um único servidor pode usar o armazenamento para a FCI a qualquer momento. As opções disponíveis para o armazenamento compartilhado no Linux são:

- iSCSI
- Network File System (NFS)
- Servidor mensagem SMB (bloco) no Windows Server, há opções ligeiramente diferentes. Uma opção que atualmente não há suportada para FCIs baseados em Linux é a capacidade de usar um disco que é local para o nó de TempDB, que é o espaço de trabalho temporário do SQL Server.

Em uma configuração que abrange vários locais, o que é armazenado em um data center deve ser sincronizado com o outro. No caso de um failover, a FCI poderão ficar online e o armazenamento é visto para ser o mesmo. Para alcançar isso exigirá algum método externo para replicação de armazenamento, se ele é feito por meio do hardware de armazenamento subjacente ou utilitário baseado em software. 

>[!NOTE]
>Para o SQL Server 2017, implantações com base em Linux usando discos apresentados diretamente para um servidor como devem ser formatadas com XFS ou EXT4. Outros sistemas de arquivos não têm suporte no momento. As alterações serão refletidas aqui.

O processo para apresentar o armazenamento compartilhado é o mesmo para os diferentes métodos com suporte:

- Configurar o armazenamento compartilhado
- Montar o armazenamento como uma pasta para os servidores que servirá como nós do cluster Pacemaker para FCI
- Se necessário, mova os bancos de dados de sistema do SQL Server para armazenamento compartilhado
- Teste do SQL Server funciona em cada servidor conectado ao armazenamento compartilhado

A principal diferença com o SQL Server no Linux é que, embora seja possível configurar o local padrão do usuário dados e log de arquivo, os bancos de dados do sistema sempre devem existir no `/var/opt/mssql/data`. No Windows Server, há a capacidade de mover os bancos de dados do sistema incluindo TempDB. Esse fato desempenha no armazenamento compartilhado como está configurado para uma FCI.

Os caminhos padrão para bancos de dados do sistema não podem ser alterados usando o `mssql-conf` utilitário. Para obter informações sobre como alterar os padrões, [alterar o local de diretório de dados ou de log padrão](sql-server-linux-configure-mssql-conf.md#datadir). Você também pode armazenar dados do SQL Server e a transação em outros locais, desde que eles tenham a segurança apropriada, mesmo se ele não é um local padrão; o local precisa ser declarada.

Os tópicos a seguir explicam como configurar os tipos de armazenamento com suporte para um Linux com base em FCI do SQL Server:

- [Configurar a instância de cluster de failover - iSCSI – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Configurar a instância de cluster de failover - NFS - SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Configurar a instância de cluster de failover - SMB - SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
