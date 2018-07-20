---
title: Instâncias de Cluster de failover – SQL Server no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 0497e1894c60e251a9cfb0d6229f1ace65b2476e
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086268"
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>Instâncias de Cluster de failover – SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica os conceitos relacionados a instâncias de cluster de failover do SQL Server (FCI) no Linux. 

Para criar uma FCI do SQL Server no Linux, consulte [configurar FCI do SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>A camada de Clustering

* No RHEL, a camada de clustering é baseada no Red Hat Enterprise Linux (RHEL) [complemento de alta disponibilidade](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf). 

    > [!NOTE] 
    > Acesso ao complemento HA do Red Hat e a documentação requer uma assinatura. 

* No SLES, a camada de clustering é baseada no SUSE Linux Enterprise [alta disponibilidade de extensão (HAE)](https://www.suse.com/products/highavailability).

    Para obter mais informações sobre a configuração de cluster, opções de recurso do agente, gerenciamento, as práticas recomendadas e recomendações, consulte [SUSE Linux Enterprise alta disponibilidade extensão 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

O complemento RHEL HA e o SUSE HAE são criados na [Pacemaker](http://clusterlabs.org/).

Como mostra o diagrama a seguir, o armazenamento é apresentado em dois servidores. Componentes de clusters - Corosync e Pacemaker - coordenam as comunicações e gerenciamento de recursos. Um dos servidores tem a conexão do Active Directory para os recursos de armazenamento e o SQL Server. Quando o Pacemaker detecta uma falha os componentes de clusters gerenciar movendo os recursos para outro nó.  

![Red Hat Enterprise Linux 7 compartilhado de Cluster de disco do SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> Neste ponto, a integração do SQL Server com o Pacemaker no Linux não é tão rígida como com o WSFC no Windows. Do dentro do SQL, não há nenhum conhecimento sobre a presença do cluster, orquestração de todos os está fora na e o serviço é controlado como uma instância autônoma por Pacemaker. Além disso, o nome de rede virtual é específico para o WSFC, não há nenhum equivalente do mesmo no Pacemaker. Espera-se que @@servername e sys. Servers para retornar o nome do nó, enquanto o DM os_cluster_nodes dmvs de cluster e dm_os_cluster_properties não serão nenhum registro. Para usar uma cadeia de caracteres de conexão que aponta para um nome de servidor de cadeia de caracteres e não usar o IP, será necessário registrar o IP usado para criar o recurso IP virtual (conforme explicado nas seções a seguir) no seu servidor DNS com o nome de servidor escolhido.

## <a name="number-of-instances-and-nodes"></a>Número de instâncias e nós

Uma diferença importante com o SQL Server no Linux é o que pode haver somente uma instalação do SQL Server por servidor Linux. Essa instalação é chamada de uma instância. Isso significa que ao contrário do Windows Server que dá suporte a até 25 FCIs por cluster de failover do Windows Server (WSFC), uma FCI com base em Linux somente terá uma única instância. Essa uma instância também é uma instância padrão; Não há nenhum conceito de uma instância nomeada no Linux. 

Um cluster Pacemaker só pode ter até 16 nós quando Corosync estiver envolvido, portanto, uma FCI única pode abranger até 16 servidores. Uma FCI implementada com a Standard Edition do SQL Server dá suporte a até dois nós de um cluster, mesmo se o cluster do Pacemaker tem o número máximo de 16 nós.

Em uma FCI do SQL Server, a instância do SQL Server está ativa em um nó ou em outro.

## <a name="ip-address-and-name"></a>Nome e endereço IP
Em um cluster Linux Pacemaker, cada FCI do SQL Server precisa de seu próprio endereço IP exclusivo e nome. Se a configuração de FCI abranger várias sub-redes, um endereço IP será exigido por sub-rede. O nome exclusivo e endereços IP são usados para acessar a FCI para que aplicativos e usuários finais não precisam saber qual servidor subjacente do cluster do Pacemaker.

O nome da FCI no DNS deve ser igual ao nome do recurso FCI que é criado no cluster do Pacemaker.
O nome e o endereço IP devem ser registrados no DNS.

## <a name="shared-storage"></a>Armazenamento compartilhado
Todas as FCIs, independentemente de estarem no Linux ou Windows Server, exigem alguma forma de armazenamento compartilhado. Esse armazenamento é apresentado para todos os servidores que possivelmente podem hospedar a FCI, mas apenas um único servidor pode usar o armazenamento para a FCI em um determinado momento. As opções disponíveis para o armazenamento compartilhado em Linux são:

- iSCSI
- Network File System (NFS)
- Servidor SMB (Message Block) no Windows Server, há opções ligeiramente diferentes. Uma opção que atualmente não há suportada para FCIs baseado em Linux é a capacidade de usar um disco que é local para o nó para o TempDB, que é o espaço de trabalho temporário do SQL Server.

Em uma configuração que abrange vários locais, o que é armazenado em um data center deve ser sincronizado com o outro. No caso de um failover, a FCI poderão ficar online e o armazenamento é visto como o mesmo. Fazer isso exigirá algum método externo para a replicação de armazenamento, se ele é feito por meio do hardware de armazenamento subjacente ou o utilitário baseado em software. 

>[!NOTE]
>Para o SQL Server 2017, implantações com base em Linux usando discos apresentados diretamente ao servidor como devem ser formatadas com XFS ou EXT4. Outros sistemas de arquivos não têm suporte no momento. Todas as alterações serão refletidas aqui.

O processo para apresentar o armazenamento compartilhado é o mesmo para os diferentes métodos com suporte:

- Configurar o armazenamento compartilhado
- Montar o armazenamento como uma pasta para os servidores que servirão como nós do cluster do Pacemaker para FCI
- Se necessário, mova os bancos de dados de sistema do SQL Server para armazenamento compartilhado
- Teste do SQL Server funciona em cada servidor conectado ao armazenamento compartilhado

A principal diferença com o SQL Server no Linux é que, embora seja possível configurar o local padrão do usuário dados e log de arquivo, os bancos de dados do sistema sempre devem existir no `/var/opt/mssql/data`. No Windows Server, há a capacidade de mover os bancos de dados do sistema incluindo TempDB. Esse fato é reproduzido em armazenamento compartilhado como está configurado para uma FCI.

Os caminhos padrão para bancos de dados não são do sistema podem ser alterados usando o `mssql-conf` utilitário. Para obter informações sobre como alterar os padrões [alterar o local de diretório de dados ou de log padrão](sql-server-linux-configure-mssql-conf.md#datadir). Você também pode armazenar dados do SQL Server e transação em outros locais, desde que eles tenham a segurança apropriada, mesmo se não for um local padrão; o local precisa ser declarada.

Os tópicos a seguir explicam como configurar tipos de armazenamento com suporte para Linux com base em FCI do SQL Server:

- [Configurar a instância de cluster de failover - iSCSI – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Configurar a instância de cluster de failover - NFS – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Configurar a instância de cluster de failover - SMB – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
