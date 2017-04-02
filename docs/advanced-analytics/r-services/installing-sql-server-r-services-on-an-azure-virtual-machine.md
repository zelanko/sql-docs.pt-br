---
title: "Instalando o SQL Server R Services em uma m&#225;quina Virtual do Azure | Microsoft Docs"
ms.custom: ""
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Instalando o SQL Server R Services em uma m&#225;quina Virtual do Azure
 
Se você implantar uma máquina virtual do Azure que inclui [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], agora você pode selecionar serviços de R como um recurso a ser adicionado à instância quando a VM é criada. 



+ [Criar uma nova VM com SQL Server 2016 e serviços de R](#new)
+ [Adicionar serviços de R para uma máquina virtual existente com o SQL Server 2016](#existing)

## <a name="a-namenewacreate-a-new-sql-server-2016-enterprise-virtual-machine-with-r-services-enabled"></a><a name="new"></a>Criar uma nova máquina de Virtual do SQL Server 2016 Enterprise com R serviços habilitados

1. No Portal do Azure, clique em MÁQUINAS VIRTUAIS e, em seguida, clique em NOVO.
2. Selecione SQL Server 2016 Enterprise Edition.
3. Configure as permissões e o nome do servidor e selecione um plano de preços.
4. Na etapa 4 na VM do Assistente de instalação, em **configurações do SQL Server**, localize **Serviços R (análise avançada)** e clique em **Habilitar**.
5. Revise o resumo apresentado para validação e clique em **OK**.
6. Quando a máquina virtual está pronta, conectá-lo e abra o SQL Server Management Studio, que é instalado. Serviços de R está pronto para execução. 
7. Para verificar isso, você pode abrir uma nova janela de consulta e executar uma instrução simples, como a seguir, que usa o R para gerar uma sequência de números de 1 a 10.
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. Se você se conectarem à instância de um cliente de ciência de dados remotos, conclua [etapas adicionais](#additional-steps) conforme necessário.


## <a name="additional-steps"></a>Etapas adicionais  

Algumas etapas adicionais poderá ser necessária para usar os serviços de R Se você espera que clientes remotos acessem o servidor como contexto de computação de um SQL Server remoto.

### <a name="a-namefirewallaunblock-the-firewall"></a><a name="firewall"></a>Desbloquear o firewall  
  
Você deve alterar uma regra de firewall na máquina virtual para garantir que você pode acessar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância de um cliente de ciência de dados remotos.  Caso contrário, você não poderá usar computação usam contextos que exigem do espaço de trabalho da máquina virtual. 

Por padrão, o firewall na máquina virtual do Azure inclui uma regra que bloqueia acesso locais R para contas de usuário de rede.  
  
Para habilitar o acesso aos serviços de R de clientes de ciência de dados remotos:
1. Na máquina virtual, abra o Firewall do Windows com segurança avançada.
2. Selecione **regras de saída**
3. Desabilite a regra a seguir:  
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`  
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar retornos de chamada ODBC para clientes remotos

Se você espera que clientes R chamando o servidor precisará emitir consultas ODBC como parte de suas soluções de R, você deve garantir que a barra inicial pode fazer chamadas ODBC em nome do cliente remoto. Para fazer isso, você deve permitir que as contas de trabalho do SQL que são usadas por barra inicial para fazer logon na instância.
Para obter mais informações, consulte [Set Up SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md). 

### <a name="a-namenetworkaadd-network-protocols"></a><a name="network"></a>Adicionar protocolos de rede  
  
+ Habilitar Pipes nomeado
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa o protocolo Pipes nomeados para conexões entre os computadores cliente e servidor e para algumas conexões internas. Se Pipes nomeados não estiver habilitado, instale e habilitá-lo sobre a máquina virtual do Azure e em clientes de ciência de dados que se conectam ao servidor.  
  
+ Habilitar TCP/IP

  TCP/IP é necessário para conexões de loopback para R serviços do SQL Server. Se você receber o erro a seguir, habilitar TCP/IP na máquina virtual que oferece suporte a instância DBNETLIB; SQL Server não existe ou acesso negado.

## <a name="how-to-disable-r-services-on-an-instance"></a>Como desabilitar serviços de R em uma instância

Você também pode habilitar ou desabilitar o recurso em uma máquina virtual existente a qualquer momento. 

1. Abra a folha de máquina virtual
2. Clique em **configurações**, e selecione **configuração do SQL Server**.


## <a name="a-nameexistingaadd-sql-server-r-services-to-an-existing-sql-server-2016-enterprise-virtual-machine"></a><a name="existing"></a>Adicionar serviços de R do SQL Server para uma máquina virtual de 2016 Enterprise do SQL Server existente

Se você criou uma VM do Azure com o SQL Server 2016 que não inclui serviços de R, você pode adicionar o recurso seguindo estas etapas:

1. Execute novamente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalação e adiciona o recurso de **configuração do servidor** página do assistente.
2. Permitir a execução de scripts externos e reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância. Para obter mais informações, consulte consulte [Set Up SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Configure o acesso de banco de dados para contas de trabalho R, se for necessário para execução de script remoto.
   Para obter mais informações, consulte [Set Up SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md). 
3. (Opcional) Modificar uma regra de firewall na máquina virtual do Azure, se você pretende permitir a execução de script R de clientes de ciência de dados remotos. Para obter mais informações, consulte [Desbloquear firewall](#firewall).
4. Instale ou habilite as bibliotecas de rede necessários. Para obter mais informações, consulte [Adicionar protocolos de rede](#network).

## <a name="see-also"></a>Consulte também
[Configurar serviços do Sql Server R](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)