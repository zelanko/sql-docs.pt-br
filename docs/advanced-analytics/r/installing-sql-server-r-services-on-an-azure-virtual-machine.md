---
title: Instalando recursos de aprendizado de máquina do SQL Server em uma máquina virtual do Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: bb1cd5e695e59c898a0e5dbcad279e1a8796bb63
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="install-sql-server-machine-learning-features-on-an-azure-virtual-machine"></a>Instalar recursos em uma máquina virtual do Azure de aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
É recomendável usar o [máquina virtual de ciência de dados](ttps://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-vm), mas se você quiser uma VM que tenha apenas serviços de aprendizado de máquina do SQL Server 2017 ou SQL Server 2016 R Services, este artigo o orienta através das etapas.

## <a name="create-a-virtual-machine-on-azure"></a>Criar uma máquina virtual no Azure

1. No portal do Azure, na lista do lado esquerdo, clique em **máquinas virtuais** e, em seguida, clique em **adicionar**.
2. Pesquisa de SQL Server 2017 Enterprise Edition ou SQL Server 2016 Enterprise Edition.
3. Configure as permissões e o nome do servidor e selecione um plano de preços.
4. Em **configurações do SQL Server** (etapa 4 no Assistente de configuração VM), localize **serviços de aprendizado de máquina (Advanced Analytics)** (ou **R Services** para SQL Server 2016) e clique em  **Habilitar**.
5. Examine o resumo apresentado para validação e clique em **OK**.
6. Quando a máquina virtual estiver pronta, conecte-se a ela e abra o SQL Server Management Studio, que é pré-instalado. Aprendizado de máquina está pronto para ser executado.
7. Para verificar isso, você pode abrir uma nova janela de consulta e executar uma instrução simples como esta, que usa o R para gerar uma sequência de números de 1 a 10.

    ```
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
    ```

6. Se você pretende conectar-se à instância de um cliente de ciência de dados remotos, conclua [etapas adicionais](#additional-steps) conforme necessário.

### <a name="disable-machine-learning-features-on-a-sql-server-vm"></a>Desativar os recursos de aprendizado de máquina em uma VM do SQL Server

Você também pode habilitar ou desabilitar o recurso em uma máquina de virtual do SQL Server existente a qualquer momento.

1. Abra a folha de máquina virtual.
2. Clique em **Configurações** e selecione **Configuração do SQL Server**.
3. Fazer alterações em recursos e aplicar.

### <a name="existing"></a>Adicionar R Services a uma VM existente do SQL Server 2016 Enterprise

Se você tiver criado uma máquina virtual do Azure que incluiu o SQL Server sem aprendizado de máquina, você pode adicionar o recurso seguindo estas etapas:

1. Execute novamente a configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e adicione o recurso da página **Configuração do Servidor** do assistente.
2. Habilite a execução de scripts externos e reinicie a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [instalar o SQL Server 2016 R Services](../install/sql-r-services-windows-install.md).
3. (Opcional) Se isto for necessário para a execução de scripts remotos, configure o acesso de banco de dados para contas de trabalho do R.
4. (Opcional) Se você pretende permitir a execução de scripts R de clientes de ciência de dados remotos, modifique uma regra de firewall na máquina virtual do Azure. Para obter mais informações, consulte [Desbloquear firewall](#firewall).
5. Instale ou habilite as bibliotecas de rede necessárias. Para obter mais informações, consulte [Adicionar protocolos de rede](#network).

## <a name="additional-steps"></a>Etapas adicionais

Algumas etapas adicionais serão necessárias se você espera que os clientes remotos acessem o servidor como um contexto de computação remoto do SQL Server.

### <a name="firewall"></a>Desbloquear o firewall

Por padrão, o firewall na máquina virtual do Azure inclui uma regra que bloqueia o acesso para contas de usuário local de rede.

Você deve desabilitar essa regra para garantir que você pode acessar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância de um cliente de ciência de dados remotos.  Caso contrário, seu código de aprendizado de máquina não pode executar em contextos de computação que usam o espaço de trabalho da máquina virtual.

Para habilitar o acesso de clientes de ciência de dados remotos:

1. Na máquina virtual, abra o Firewall do Windows com Segurança Avançada.
2. Selecione **Regras de Saída**
3. Desabilite a regra a seguir:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar retornos de chamada ODBC para clientes remotos

Se você espera que os clientes chamando o servidor precisará emitir consultas ODBC como parte de sua soluções de aprendizado de máquina, certifique-se de que a barra inicial pode fazer chamadas ODBC em nome do cliente remoto. Para fazer isso, você deve permitir que as contas de trabalho do SQL que são usadas pelo Launchpad façam logon na instância.
Para obter mais informações, consulte [instalar o SQL Server 2016 R Services](../install/sql-r-services-windows-install.md).

### <a name="network"></a>Adicionar protocolos de rede

+ Habilitar pipes nomeados
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa o protocolo de Pipes Nomeados para conexões entre os computadores cliente e servidor, além de algumas conexões internas. Se a opção Pipes Nomeados não estiver habilitada, instale e habilite-a tanto na máquina virtual do Azure quanto quaisquer clientes de ciência de dados que se conectem ao servidor.
  
+ Habilitar TCP/IP

  TCP/IP é necessário para conexões de loopback. Se você receber o erro a seguir, habilite o TCP/IP na máquina virtual que oferece suporte à instância do:

  "DBNETLIB; SQL Server não existe ou acesso negado"