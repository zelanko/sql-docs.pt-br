---
title: "Instalando recursos de aprendizado de máquina do SQL Server em uma máquina virtual do Azure | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 0c4b8ef73f4afbc54d2fc1841e281afd0342cedf
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="installing-sql-server-machine-learning-features-on-an-azure-virtual-machine"></a>Instalando recursos em uma máquina virtual do Azure de aprendizado de máquina do SQL Server
 
Se você implantar uma máquina virtual do Azure que inclui [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], agora você pode selecionar o aprendizado de máquina como um recurso a ser adicionado à instância quando a VM é criada.

+ [Criar uma nova VM que inclui serviços de R e SQL Server 2016](#new)
+ [Adicionar recursos de aprendizado de máquina para uma máquina virtual existente com o SQL Server 2016](#existing)

> [!NOTE]
> Máquinas virtuais agora estão disponíveis para o SQL Server 2017! Consulte [este anúncio](https://azure.microsoft.com/blog/announcing-new-azure-vm-images-sql-server-2017-on-linux-and-windows/) para obter detalhes.
> 
> R também está disponível como um recurso de visualização no banco de dados do SQL Azure. Para obter mais informações, consulte [usando R no SQL Azure](../r/using-r-in-azure-sql-database.md).

## <a name="create-a-new-sql-server-2017-virtual-machine"></a>Criar uma nova máquina virtual 2017 do SQL Server

Para usar o R ou Python no SQL Server 2017, certifique-se de obter uma máquina virtual com base em Windows. [!INCLUDE[sscurrentlong-md](../../includes/sscurrentlong-md.md)]no Linux oferece suporte a fast [pontuação nativo](../sql-native-scoring.md) usando a função de previsão de T-SQL, mas outros recursos de aprendizado de máquina não estão disponíveis ainda nesta edição.

Para obter uma lista de ofertas de VM do SQL Server, consulte este artigo: [visão geral do SQL Server em máquinas virtuais do Azure (Windows)](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview).

### <a name="new"></a>Criar uma nova VM do SQL Server Enterprise com o aprendizado de máquina

1. No portal do Azure, clique em máquinas virtuais e, em seguida, clique em novo.
2. Selecione o SQL Server de 2017 Enterprise Edition.
3. Configure as permissões e o nome do servidor e selecione um plano de preços.
4. Em **configurações do SQL Server** (etapa 4 no Assistente de configuração VM), localize **serviços de aprendizado de máquina (Advanced Analytics)** e clique em **habilitar**.
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
2. Habilite a execução de scripts externos e reinicie a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [configurar o SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Se isto for necessário para a execução de scripts remotos, configure o acesso de banco de dados para contas de trabalho do R.
   Para obter mais informações, consulte [Configurar o SQL Server R Services (no Banco de Dados)](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Se você pretende permitir a execução de scripts R de clientes de ciência de dados remotos, modifique uma regra de firewall na máquina virtual do Azure. Para obter mais informações, consulte [Desbloquear firewall](#firewall).
4. Instale ou habilite as bibliotecas de rede necessárias. Para obter mais informações, consulte [Adicionar protocolos de rede](#network).

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
Para obter mais informações, consulte [Configurar o SQL Server R Services (no Banco de Dados)](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).

### <a name="network"></a>Adicionar protocolos de rede

+ Habilitar pipes nomeados
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa o protocolo de Pipes Nomeados para conexões entre os computadores cliente e servidor, além de algumas conexões internas. Se a opção Pipes Nomeados não estiver habilitada, instale e habilite-a tanto na máquina virtual do Azure quanto quaisquer clientes de ciência de dados que se conectem ao servidor.
  
+ Habilitar TCP/IP

  TCP/IP é necessário para conexões de loopback. Se você receber o erro a seguir, habilite o TCP/IP na máquina virtual que oferece suporte à instância do:

  "DBNETLIB; SQL Server não existe ou acesso negado"

## <a name="related-resources"></a>Recursos relacionados

[Usando o R no banco de dados SQL do Azure](../r/using-r-in-azure-sql-database.md)