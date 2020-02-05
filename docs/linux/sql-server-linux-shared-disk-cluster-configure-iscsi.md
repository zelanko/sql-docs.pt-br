---
title: 'Configurar o armazenamento da FCI iSCSI: SQL Server em Linux'
description: Saiba como configurar uma FCI (instância de cluster de failover) usando o iSCSI no SQL Server em Linux.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e10f354a8f0af2467a9519a794995043864a4cd6
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558570"
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>Configurar a instância de cluster de failover – iSCSI – SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar o armazenamento iSCSI para uma FCI (instância de cluster de failover) no Linux. 

## <a name="configure-iscsi"></a>Configurar iSCSI 
O iSCSI usa a rede para apresentar discos de um servidor conhecido como um destino para servidores. Os servidores que se conectam ao destino iSCSI exigem que um iniciador iSCSI esteja configurado. Os discos no destino recebem permissões explícitas, de forma que somente os iniciadores que devem poder acessá-los conseguem fazer isso. O próprio destino deve estar altamente disponível e ser confiável.

### <a name="important-iscsi-target-information"></a>Informações importantes de destino iSCSI
Embora esta seção não aborde como configurar um destino iSCSI, uma vez que ele é específico ao tipo de fonte que você usará, verifique se a segurança dos discos que serão usados pelos nós de cluster está configurada.  

O destino nunca deverá ser configurado em nenhum dos nós FCI se estiver usando um destino iSCSI baseado em Linux. Para desempenho e disponibilidade, as redes iSCSI devem ser separadas das usadas pelo tráfego de rede regular nos servidores de origem e de cliente. As redes usadas para o iSCSI devem ser rápidas. Lembre-se de que a rede consome alguma largura de banda do processador, portanto, planeje adequadamente se estiver usando um servidor normal.
O mais importante a garantir que seja concluído no destino é que os discos criados recebam as permissões apropriadas para que somente os servidores que participam da FCI tenham acesso a eles. Um exemplo é mostrado abaixo do destino iSCSI da Microsoft, em que linuxnodes1 é o nome criado e, nesse caso, os endereços IP dos nós são atribuídos para que NewFCIDisk1.vhdx apareça para eles.

![Initiator (iniciador)][1]

### <a name="instructions"></a>Instruções

Esta seção explicará como configurar um iniciador iSCSI nos servidores que atuarão como nós para o FCI. As instruções devem funcionar como estão no RHEL e no Ubuntu.

Para obter mais informações sobre o iniciador iSCSI para as distribuições compatíveis, confira os links a seguir:
- [Red Hat](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](https://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  Escolha um dos servidores que participarão da configuração da FCI. Não importa qual. O iSCSI deve estar em uma rede dedicada, portanto, configure o iSCSI para reconhecer e usar essa rede. Execute `sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new`, em que `<iSCSIIfaceName>` é o nome exclusivo ou amigável para a rede. O exemplo a seguir usa `iSCSINIC`:
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  Edite `/var/lib/iscsi/ifaces/iSCSIIfaceName`. Verifique se ele tem os seguintes valores preenchidos completamente:

    - iface.net _ifacename é o nome da placa de rede como visto no sistema operacional.
    - iface.hwaddress é o endereço MAC do nome exclusivo que será criado para esta interface abaixo.
    - iface.ipaddress
    - iface.subnet_Mask 

    Consulte o seguinte exemplo:

    ![iSCSITargetSettings][2]

3.  Localize o destino iSCSI.

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName> é o nome exclusivo/amigável da rede, \<TargetIPAddress> é o endereço IP do destino iSCSI e \<TargetPort> é a porta do destino iSCSI. 

    ![iSCSITargetResults][3]

 
4.  Fazer logon no destino

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName> é o nome exclusivo/amigável para a rede e \<TargetIPAddress> é o endereço IP do destino iSCSI.

    ![iSCSITargetLogin][4]

5.  Verifique se há uma conexão com o destino iSCSI.

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  Verificar discos conectados iSCSI

    ```bash
    sudo grep "Attached SCSI" /var/log/messages
    ```
    ![30-iSCSIattachedDisks][7]

7.  Crie um volume físico no disco iSCSI.

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<devicename> é o nome do dispositivo da etapa anterior. 

 
8.  Crie um grupo de volumes no disco iSCSI. Os discos atribuídos a um único grupo de volumes são vistos como um pool ou uma coleção. 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName> é o nome do grupo de volumes e \<devicename> é o nome do dispositivo da Etapa 6. 
 
9.  Crie e verifique o volume lógico do disco.

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<size> é o tamanho do volume a ser criado e pode ser especificado com G (gigabytes), T (terabytes) etc.,\<LogicalVolumeName> é o nome do volume lógico e \<VolumeGroupName> é o nome do grupo de volumes do etapa anterior. 

    O exemplo a seguir cria um volume de 25 GB.
 
    ![Create25GBVol][10]

10. Execute `sudo lvs` para ver o LVM que foi criado.
 
11. Formate o volume lógico com um sistema de arquivos com suporte. Para EXT4, use o exemplo a seguir:

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName> é o nome do grupo de volumes da etapa anterior. \<LogicalVolumeName> é o nome do volume lógico da etapa anterior.  

12. Para bancos de dados do sistema ou qualquer item armazenado na localização de dados padrão, siga estas etapas. Caso contrário, vá para a etapa 13.

   *    Verifique se o SQL Server está parado no servidor em que você está trabalhando.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Alterne totalmente para o superusuário. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    sudo -i
    ```

   *    Alterne para ser o usuário mssql. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    su mssql
    ```

   *    Crie um diretório temporário para armazenar os dados e os arquivos de log do SQL Server. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir> é o nome da pasta. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/TempDir.

    ```bash
    mkdir /var/opt/mssql/TempDir
    ```
    
   *    Copie os dados e os arquivos de log do SQL Server para o diretório temporário. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir> é o nome da pasta da etapa anterior.
    
   *    Verifique se os arquivos estão no diretório.

    ```bash
    ls \<TempDir>
    ```
    \<TempDir> é o nome da pasta da etapa D.

   *    Exclua os arquivos do diretório de dados do SQL Server existente. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   *    Verifique se os arquivos foram excluídos. A figura abaixo mostra um exemplo de toda a sequência de c a h.

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45-CopyMove][8]
 
   *    Digite `exit` para voltar ao usuário raiz.

   *    Monte o volume lógico iSCSI na pasta SQL Server Data. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName> é o nome do grupo de volume e \<LogicalVolumeName> é o nome do volume lógico que foi criado. A sintaxe de exemplo a seguir corresponde ao grupo de volumes e ao volume lógico do comando anterior.

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    Altere o proprietário da montagem para mssql. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    Altere a propriedade do grupo da montagem para mssql. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    Alterne para o usuário mssql. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    su mssql
    ``` 

   *    Copie os arquivos do diretório temporário /var/opt/mssql/data. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    Verifique se os arquivos estão lá.

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    Digite `exit` para não ser MSSQL.
    
   *    Digite `exit` para não ser raiz.

   *    Inicie o SQL Server. Se tudo for copiado corretamente e a segurança for aplicada corretamente, o SQL Server deverá ser mostrado como iniciado.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    Interrompa o SQL Server e verifique se ele está desligado.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. Para outros itens que não os bancos de dados do sistema, como bancos de dados de usuário ou backups, siga estas etapas. Se estiver usando apenas a localização padrão, vá para a Etapa 14.

   *    Alterne para o superusuário. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    sudo -i
    ```

   *    Crie uma pasta que será usada pelo SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<FolderName> é o nome da pasta. O caminho completo da pasta precisará ser especificado se não estiver na localização correta. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    Monte o volume lógico iSCSI na pasta que foi criada na etapa anterior. Você não receberá nenhuma confirmação se tiver êxito.
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName> é o nome do grupo de volumes, \<LogicalVolumeName> é o nome do volume lógico que foi criado e \<FolderName> é o nome da pasta. A sintaxe de exemplo é mostrada abaixo.

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    Altere a propriedade da pasta criada para mssql. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    chown mssql <FolderName>
    ```

    \<FolderName> é o nome da pasta que foi criada. Um exemplo é mostrado abaixo.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    Altere o grupo da pasta criada para mssql. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    chown mssql <FolderName>
    ```

    \<FolderName> é o nome da pasta que foi criada. Um exemplo é mostrado abaixo.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    Digite `exit` para deixar de ser o superusuário.

   *    Para testar, crie um banco de dados nessa pasta. O exemplo mostrado a seguir usa o sqlcmd para criar um banco de dados, alternar o contexto para ele, verificar se os arquivos existem no nível do sistema operacional e, em seguida, exclui a localização temporária. Você pode usar o SSMS.
  
    ![50-ExampleCreateSSMS][9]

   *    Desmontar o compartilhamento 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName> é o nome do grupo de volumes, \<LogicalVolumeName> é o nome do volume lógico que foi criado e \<FolderName> é o nome da pasta. A sintaxe de exemplo é mostrada abaixo.

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. Configure o servidor para que apenas o Pacemaker possa ativar o grupo de volumes.

    ```bash
    sudo lvmconf --enable-halvm --services -startstopservices
    ```
 
15. Gere uma lista dos grupos de volumes no servidor. Qualquer item listado que não seja o disco iSCSI será usado pelo sistema, como para o disco do sistema operacional.

    ```bash
    sudo vgs
    ```

16. Modifique a seção de configuração de ativação do arquivo /etc/lvm/lvm.conf. Configure a seguinte linha:

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker> é a lista de grupos de volumes da saída da Etapa 20 que não será usada pelo FCI. Coloque cada um entre aspas e separe por uma vírgula. Um exemplo é mostrado abaixo.

    ![55-ListOfVGs][11]
 
 
17. Quando o Linux for iniciado, ele montará o sistema de arquivos. Para garantir que apenas o Pacemaker possa montar o disco iSCSI, recompile a imagem do sistema de arquivos raiz. 

    Execute o comando a seguir, o que pode levar alguns minutos para ser concluído. Você não receberá nenhuma mensagem se tiver êxito.

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. Reinicialize o servidor.

19. Em outro servidor que participará do FCI, execute as Etapas de 1 a 6. Isso apresentará o destino iSCSI para o SQL Server. 
 
20. Gere uma lista dos grupos de volumes no servidor. Ele deve mostrar o grupo de volumes criado anteriormente. 

    ```bash
    sudo vgs
    ``` 
23. Inicie o SQL Server e verifique se ele pode ser iniciado neste servidor.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. Interrompa o SQL Server e verifique se ele está desligado.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. Repita as Etapas de 1-6 em quaisquer outros servidores que participarão do FCI.

Agora você está pronto para configurar a FCI.

|Distribuição |Tópico 
|----- |-----
|**Red Hat Enterprise Linux com o complemento de HA** |[Configurar](sql-server-linux-shared-disk-cluster-configure.md)<br/>[Operar](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server com o complemento de HA** |[Configurar](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>Próximas etapas

[Configurar a instância de cluster de failover – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/05-initiator.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/10-iscsiTargetSettings.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/15-iSCSITargetResults.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/20-iSCSITargetLogin.png
[5]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/25-iSCSIVerify.png
[6]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/7-setiscsinetwork.png
[7]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/30-iSCSIattachedDisks.png
[8]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/45-CopyMove.png
[9]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/50-ExampleCreateSSMS.png
[10]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/40-Create25GBVol.png
[11]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/55-ListOfVGs.png
