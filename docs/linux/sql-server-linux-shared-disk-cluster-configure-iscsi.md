---
title: Configurar o iSCSI de armazenamento de instância de cluster de failover – SQL Server no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 514d19e4358b536109c76112115bac380f390bce
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>Configurar a instância de cluster de failover - iSCSI – SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar o armazenamento iSCSI para uma instância de cluster de failover (FCI) no Linux. 

## <a name="configure-iscsi"></a>Configurar o iSCSI 
iSCSI usa a rede para apresentar os discos de um servidor conhecido como um destino para servidores. Os servidores que se conectar ao destino iSCSI exigem que um iniciador iSCSI está configurado. Os discos de destino recebem permissões explícitas para que somente os iniciadores que devem ser capazes de acessá-los podem fazê-lo. O destino em si deve ser confiável e altamente disponível.

### <a name="important-iscsi-target-information"></a>Informações de destino iSCSI importantes
Embora esta seção não aborda como configurar um destino iSCSI, pois ele é específico para o tipo de origem que você usará, certifique-se de que a segurança para os discos que serão usadas por nós de cluster está configurada.  

O destino nunca deve ser configurado em qualquer um de nós de FCI se usando um destino iSCSI baseadas em Linux. Para desempenho e disponibilidade, redes iSCSI devem ser separados daqueles usados pelo tráfego de rede regular na origem e servidores do cliente. Redes usadas para iSCSI devem ser rápidas. Lembre-se nessa rede consumir largura de banda alguns processadores, portanto, planeje adequadamente se usando um servidor regular.
O mais importante para garantir que é concluída no destino é que os discos que são criados são atribuídos as permissões apropriadas para que apenas os servidores que participam na FCI têm acesso a eles. Um exemplo é mostrado abaixo do destino iSCSI Microsoft onde linuxnodes1 é o nome criado, e nesse caso, os endereços IP de nós são atribuídos para que apareça NewFCIDisk1.vhdx a eles.

![Initiator (iniciador)][1]

### <a name="instructions"></a>Instruções

Esta seção aborda como configurar um iniciador iSCSI em servidores que servirá como nós de FCI. As instruções devem funcionar como em RHEL e Ubuntu.

Para obter mais informações sobre o iniciador iSCSI para as distribuições com suporte, consulte os links a seguir:
- [Red Hat](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](http://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  Escolha um dos servidores que participarão na configuração de FCI. Não importa qual delas. iSCSI deve estar em uma rede dedicada, para configurar o iSCSI para reconhecer e usar essa rede. Executar `sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new` onde `<iSCSIIfaceName>` é o nome amigável ou exclusivo para a rede. O exemplo a seguir usa `iSCSINIC`:
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  Editar `/var/lib/iscsi/ifaces/iSCSIIfaceName`. Verifique se que ele tem os seguintes valores completamente preenchidos:

    - iface.net_ifacename é o nome da placa de rede, como visto no sistema operacional.
    - iface.hwaddress é o endereço MAC do nome exclusivo que será criado para esta interface abaixo.
    - iface.ipaddress
    - iface.subnet_Mask 

    Consulte o seguinte exemplo:

    ![iSCSITargetSettings][2]

3.  Localize o destino iSCSI.

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName > é o nome amigável exclusivo para/da rede, \<TargetIPAddress > é o endereço IP do destino iSCSI, e \<TargetPort > é a porta de destino iSCSI. 

    ![iSCSITargetResults][3]

 
4.  Faça logon no destino

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName > é o nome exclusivo/amigável para a rede e \<TargetIPAddress > é o endereço IP do destino iSCSI.

    ![iSCSITargetLogin][4]

5.  Verifique se há uma conexão com o destino iSCSI.

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  Verifique os discos conectados no iSCSI

    ```bash
    sudo grep “Attached SCSI” /var/log/messages
    ```
    ![30-iSCSIattachedDisks][7]

7.  Crie um volume físico no disco iSCSI.

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<nome do dispositivo > é o nome do dispositivo da etapa anterior. 

 
8.  Crie um grupo de volumes no disco iSCSI. Discos atribuídos a um único grupo de volumes são vistos como um pool ou uma coleção. 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName > é o nome do grupo de volumes e \<devicename > é o nome do dispositivo da etapa 6. 
 
9.  Crie e verifique se o volume lógico para o disco.

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<tamanho > é o tamanho do volume a ser criado e pode ser especificado com G (gigabytes), T (terabytes), etc.,\<LogicalVolumeName > é o nome do volume lógico, e \<VolumeGroupName > é o nome do grupo de volumes das etapa anterior. 

    O exemplo a seguir cria um volume de 25GB.
 
    ![Create25GBVol][10]

10. Execute `sudo lvs` para ver o LVM que foi criado.
 
11. Formate o volume lógico com um sistema de arquivos com suporte. Para EXT4, use o exemplo a seguir:

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName > é o nome do grupo de volumes da etapa anterior. \<LogicalVolumeName > é o nome do volume lógico da etapa anterior.  

12. Para bancos de dados do sistema ou em qualquer coisa armazenada no local padrão de dados, siga estas etapas. Caso contrário, pule para a etapa 13.

   *    Certifique-se de que o SQL Server está interrompido no servidor que você está trabalhando.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Opção totalmente para ser o superusuário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    sudo -i
    ```

   *    Alternar para ser o usuário mssql. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    su mssql
    ```

   *    Crie um diretório temporário para armazenar dados do SQL Server e os arquivos de log. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > é o nome da pasta. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/TempDir.

    ```bash
    mkdir /var/opt/mssql/TempDir
    ```
    
   *    Copie os arquivos de log e de dados do SQL Server para o diretório temporário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > é o nome da pasta da etapa anterior.
    
   *    Verifique se os arquivos no diretório.

    ```bash
    ls \<TempDir>
    ```
    \<TempDir > é o nome da pasta da etapa d.

   *    Exclua os arquivos do diretório de dados do SQL Server existente. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    Verifique se que os arquivos foram excluídos. A figura abaixo mostra um exemplo de toda a sequência de c a h.

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45 CopyMove][8]
 
   *    Tipo `exit` para alternar novamente para o usuário raiz.

   *    Monte o volume lógico da iSCSI na pasta de dados do SQL Server. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName > é o nome do grupo de volumes e \<LogicalVolumeName > é o nome do volume lógico que foi criado. A seguinte sintaxe de exemplo corresponde ao grupo de volumes e o volume lógico do comando anterior.

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    Altere o proprietário da montagem para mssql. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    Alterar a propriedade do grupo de montagem para mssql. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    Alterne para o usuário mssql. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    su mssql
    ``` 

   *    Copie os arquivos do /var/opt/mssql/data diretório temporário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    Verifique se que os arquivos estão lá.

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    Digite `exit` para não ser mssql.
    
   *    Insira `exit` a não ser a raiz.

   *    Inicie o SQL Server. Se tudo foi copiado corretamente e segurança aplicada corretamente, do SQL Server deve mostrar é iniciado.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    Interrompa o SQL Server e verifique se que ele está desligado.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. Para tarefas diferentes bancos de dados do sistema, como bancos de dados de usuário ou backups, siga estas etapas. Se apenas usando o local padrão, vá para a etapa 14.

   *    Alternar para ser o superusuário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    sudo -i
    ```

   *    Crie uma pasta que será usada pelo SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<Nome da pasta > é o nome da pasta. Caminho completo da pasta deve ser especificado se não está no local correto. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    Monte o volume lógico da iSCSI na pasta que foi criado na etapa anterior. Você não receberá nenhuma confirmação se for bem-sucedido.
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > é o nome do grupo de volumes, \<LogicalVolumeName > é o nome do volume lógico que foi criado, e \<FolderName > é o nome da pasta. Sintaxe de exemplo é mostrada abaixo.

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    Alterar a propriedade da pasta criada para mssql. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    chown mssql <FolderName>
    ```

    \<Nome da pasta > é o nome da pasta que foi criado. Um exemplo é mostrado a seguir.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    Altere o grupo da pasta criada para mssql. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    chown mssql <FolderName>
    ```

    \<Nome da pasta > é o nome da pasta que foi criado. Um exemplo é mostrado a seguir.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    Tipo `exit` deixe de ser o superusuário.

   *    Para testar, crie um banco de dados nessa pasta. O exemplo abaixo usa o sqlcmd para criar um banco de dados, alterne o contexto para ele, verifique se os arquivos existem no nível do sistema operacional e, em seguida, exclui o local temporário. Você pode usar o SSMS.
  
    ![50-ExampleCreateSSMS][9]

   *    Desmontar o compartilhamento 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > é o nome do grupo de volumes, \<LogicalVolumeName > é o nome do volume lógico que foi criado, e \<FolderName > é o nome da pasta. Sintaxe de exemplo é mostrada abaixo.

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. Configure o servidor de modo que somente Pacemaker pode ativar o grupo de volumes.

    ```bash
    sudo lvmconf --enable-halvm --services –startstopservices
    ```
 
15. Gere uma lista dos grupos de volume no servidor. Todos os itens listados que não seja o disco iSCSI é usado pelo sistema, como para o disco do sistema operacional.

    ```bash
    sudo vgs
    ```

16. Modifique a seção de configuração de ativação de /etc/lvm/lvm.conf o arquivo. Configure a linha a seguir:

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker > é a lista de grupos de volume da saída de etapa 20 que não será usado por FCI. Coloque cada uma entre aspas e separado por uma vírgula. Um exemplo é mostrado a seguir.

    ![55-ListOfVGs][11]
 
 
17. Quando o Linux é iniciado, ele instala o sistema de arquivos. Para garantir que somente Pacemaker pode montar o disco iSCSI, recrie a imagem do sistema de arquivos raiz. 

    Execute o seguinte comando que pode levar alguns minutos para ser concluído. Você não obterá novamente nenhuma mensagem de êxito.

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. Reinicialize o servidor.

19. Em outro servidor que participará na FCI, execute as etapas 1 a 6. Isso apresentará o destino iSCSI para o SQL Server. 
 
20. Gere uma lista dos grupos de volume no servidor. Ele deverá mostrar que o grupo de volume criado anteriormente. 

    ```bash
    sudo vgs
    ``` 
23. Iniciar o SQL Server e verifique se que ele pode ser iniciado neste servidor.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. Interrompa o SQL Server e verifique se está desligada.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. Repita as etapas 1 a 6 em outros servidores que participarão na FCI.

Agora você está pronto para configurar a FCI.

|Distribuição |Tópico 
|----- |-----
|**Red Hat Enterprise Linux com o complemento HA** |[Configurar](sql-server-linux-shared-disk-cluster-configure.md)<br/>[Operar](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server com o complemento HA** |[Configurar](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>Próximas etapas

[Configurar a instância de cluster de failover - SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure.md)

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
