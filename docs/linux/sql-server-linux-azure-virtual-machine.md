---
title: Provisionar um servidor Linux SQL VM no Azure | Microsoft Docs
description: "Este tutorial mostra como criar uma máquina virtual de 2017 do Linux SQL Server no Azure."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 222e23b2-51e7-429b-b8e5-61e0ebe7df9b
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 0470622b0fe5a8835213617a4fc2e8c74f674873
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-linux-sql-server-2017-virtual-machine-with-the-azure-portal"></a>Criar uma máquina virtual de 2017 do Linux SQL Server com o portal do Azure

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

O Azure fornece imagens de máquinas virtuais Linux com o SQL Server de 2017 RC2 instalado. Este tópico fornece uma breve explicação sobre como usar o portal do Azure para criar uma máquina virtual Linux SQL Server. 

## <a name="create-a-linux-vm-with-sql-server-installed"></a>Criar uma VM do Linux com o SQL Server instalado

Abra o [portal do Azure](https://portal.azure.com/).

1. Clique em **novo** à esquerda.

1. No **novo** folha, clique em **de computação**.

1. Clique em **consulte todos os** lado a **aplicativos em destaque** título.

   ![Ver todas as imagens VM](./media/sql-server-linux-azure-virtual-machine/azure-compute-blade.png)

1. Na caixa de pesquisa, digite **SQL Server 2017**e pressione **Enter** para iniciar a pesquisa.

    ![Filtro de pesquisa para imagens de VM do SQL Server de 2017](./media/sql-server-linux-azure-virtual-machine/searchfilter.png)

    > [!TIP]
    > Esse filtro mostra as imagens de máquina virtual Linux disponíveis para o SQL Server 2017. Ao longo do tempo, as imagens do SQL Server 2017 para outras distribuições do Linux com suporte serão listadas. Você também pode clicar isso [link](https://ms.portal.azure.com/#blade/Microsoft_Azure_Marketplace/GalleryFeaturedMenuItemBlade/selectedMenuItemId/home/searchQuery/sql%20server%202017) para ir diretamente para os resultados da pesquisa para o SQL Server 2017. 

1. Selecione uma imagem do SQL Server 2017 nos resultados da pesquisa.

1. Clique em **Criar**.

1. Sobre o **Noções básicas sobre** folha, preencha os detalhes para a VM do Linux. 

    ![Folha de Noções básicas](./media/sql-server-linux-azure-virtual-machine/basics.png)

    > [!Note]
    > Você tem a opção de usar uma chave pública SSH ou uma senha para autenticação. SSH é mais segura. Para obter instruções sobre como gerar uma chave SSH, consulte [criar SSH chaves em Linux e Mac para VMs do Linux no Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-mac-create-ssh-keys). 

1. Clique em **OK**.

1. Sobre o **tamanho** folha, escolha um tamanho de máquina. Para desenvolvimento e testes funcionais, recomendamos que um tamanho de VM **DS2** ou superior. Para testes de desempenho, use **DS13** ou superior.

    ![Escolha um tamanho VM](./media/sql-server-linux-azure-virtual-machine/vmsizes.png)

    Para ver outros tamanhos, selecione **exibir todos os**. Para obter mais informações sobre tamanhos de máquina VM, consulte [tamanhos de VM do Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes).

1. Clique em **Selecionar**.

1. Sobre o **configurações** folha, você pode alterar as configurações ou manter as configurações padrão.

1. Clique em **OK**.

1. Sobre o **resumo** , clique em **Okey** para criar a VM.

> [!NOTE]
> A VM do Azure pré-configura o firewall para abrir a porta 1433 do SQL Server para conexões remotas. Mas, para se conectar remotamente, você também precisará adicionar uma regra de grupo de segurança de rede, conforme descrito na próxima seção.

## <a id="remote"></a>Configurar para conexões remotas

Para poder se conectar remotamente ao SQL Server em uma VM do Azure, você deve configurar uma regra de entrada no grupo de segurança de rede. A regra permite o tráfego na porta na qual o SQL Server escuta (padrão 1433). As etapas a seguir mostram como usar o portal do Azure para esta etapa. 

1. No portal, selecione **máquinas virtuais**e, em seguida, selecione a VM do SQL Server.

1. Na lista de propriedades, selecione **interfaces de rede**.

1. Em seguida, selecione a Interface de rede para sua VM.

    ![Interfaces de rede](./media/sql-server-linux-azure-virtual-machine/networkinterfaces.png)

1. Clique no link de grupo de segurança de rede.

    ![Grupo de segurança de rede](./media/sql-server-linux-azure-virtual-machine/networksecuritygroup.png)

1. Nas propriedades do grupo de segurança de rede, selecione **regras de segurança de entrada**.

1. Clique o **+ adicionar** botão.

1. Forneça um nome de "SQLServerRemoteConnections".

1. No **Service** lista, selecione **MS SQL**.

    ![Regra de grupo de segurança do MS SQL](./media/sql-server-linux-azure-virtual-machine/sqlnsgrule.png)

1. Clique em **Okey** para salvar a regra para sua VM.

## <a id="connect"></a>Conecte-se à VM do Linux

Se você já usa um shell BASH, conecte-se à VM do Azure usando o **ssh** comando. No comando a seguir, substitua o nome de usuário da VM e o endereço IP para conectar-se à VM do Linux.

```bash
ssh -l AzureAdmin 100.55.555.555
```

Você pode encontrar o endereço IP da VM no portal do Azure.

![Endereço IP no portal do Azure](./media/sql-server-linux-azure-virtual-machine/vmproperties.png)

Se você estiver executando no Windows e não tem um shell BASH, você pode instalar um cliente SSH, como PuTTY.

1. [Baixe e instale o PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Execute o PuTTY.

1. Na tela de configuração PuTTY insira o endereço IP público da VM.

1. Clique em Abrir e inserir seu nome de usuário e senha nos prompts.

Para obter mais informações sobre como se conectar às VMs do Linux, consulte [criar uma VM do Linux no Azure usando o Portal de](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-portal#ssh-to-the-vm).

## <a name="configure-sql-server"></a>Configurar o SQL Server

1. Depois de conectar-se à VM do Linux, abra um novo comando de terminal.

1. Configure o SQL Server com o comando a seguir.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup 
   ```

   Aceite a licença e inserir uma senha para a conta de administrador do sistema. Você pode iniciar o servidor quando solicitado.

1. Opcionalmente, [instalar as ferramentas do SQL Server](sql-server-linux-setup-tools.md).

## <a name="next-steps"></a>Próximas etapas

Agora que você tem uma máquina virtual de 2017 do SQL Server no Azure, você pode se conectar localmente com **sqlcmd** para executar consultas Transact-SQL.

Se você tiver configurado a VM do Azure para conexões remotas do SQL Server, você também deve ser capaz de se conectar remotamente. Para obter um exemplo de se conectar ao SQL Server no Linux de um computador remoto do Windows, consulte [SSMS de uso no Windows para se conectar ao SQL Server no Linux](sql-server-linux-develop-use-ssms.md).

Para obter mais informações sobre máquinas virtuais Linux no Azure, consulte o [documentação de máquina Virtual Linux](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/).

