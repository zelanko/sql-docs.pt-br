---
title: "Instalação do SQL Server R Services em uma Máquina Virtual do Azure | Microsoft Docs"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e673268b1f6b56890f22576d293135b2675ed4ab
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="installing-sql-server-r-services-on-an-azure-virtual-machine"></a>Instalação do SQL Server R Services em uma Máquina Virtual do Azure
 
Se você implantar uma máquina virtual do Azure que inclui [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], agora você pode selecionar o aprendizado de máquina como um recurso a ser adicionado à instância quando a VM é criada.

+ [Criar uma nova VM com SQL Server 2016 e R Services](#new)
+ [Adicionar o R Services a uma máquina virtual existente com o SQL Server 2016](#existing)

## <a name="new"></a>Criar uma nova máquina virtual do SQL Server 2016 Enterprise com o R Services habilitado

1. No portal do Azure, clique em máquinas virtuais e, em seguida, clique em novo.
2. Selecione SQL Server 2016 Enterprise Edition.
3. Configure as permissões e o nome do servidor e selecione um plano de preços.
4. Na Etapa 4 no assistente de configuração de VM, em **Configurações do SQL Server**, localize **R Services (Análise Avançada)** e clique em **Habilitar**.
5. Examine o resumo apresentado para validação e clique em **OK**.
6. Quando a máquina virtual estiver pronta, conecte-se a ela e abra o SQL Server Management Studio, que é pré-instalado. O R Services está pronto para execução.
7. Para verificar isso, você pode abrir uma nova janela de consulta e executar uma instrução simples como esta, que usa o R para gerar uma sequência de números de 1 a 10.
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. Se você for se conectar à instância de um cliente de ciência de dados remotos, conclua as [etapas adicionais](#additional-steps) conforme necessário.


## <a name="additional-steps"></a>Etapas adicionais  

Algumas etapas adicionais serão necessárias se você espera que os clientes remotos acessem o servidor como um contexto de computação remoto do SQL Server.

### <a name="firewall"></a>Desbloquear o firewall

Por padrão, o firewall na máquina virtual do Azure inclui uma regra que bloqueia o acesso de rede para contas de usuários locais de R.

Você deve desabilitar essa regra para garantir que você pode acessar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância de um cliente de ciência de dados remotos.  Caso contrário, seu código R não pode executar em contextos de computação que usam o espaço de trabalho da máquina virtual, mesmo se outro código de R usa o contexto de computação do SQL Server sem problemas.

Para habilitar o acesso de clientes de ciência de dados remotos ao R Services:

1. Na máquina virtual, abra o Firewall do Windows com Segurança Avançada.
2. Selecione **Regras de Saída**
3. Desabilite a regra a seguir:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar retornos de chamada ODBC para clientes remotos

Se você esperar que clientes do R chamando o servidor precisem emitir consultas ODBC como parte de suas soluções de R, você deverá assegurar que o Launchpad possa fazer chamadas ODBC em nome do cliente remoto. Para fazer isso, você deve permitir que as contas de trabalho do SQL que são usadas pelo Launchpad façam logon na instância.
Para obter mais informações, consulte [Configurar o SQL Server R Services (no Banco de Dados)](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).

### <a name="network"></a>Adicionar protocolos de rede

+ Habilitar pipes nomeados
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa o protocolo de Pipes Nomeados para conexões entre os computadores cliente e servidor, além de algumas conexões internas. Se a opção Pipes Nomeados não estiver habilitada, instale e habilite-a tanto na máquina virtual do Azure quanto quaisquer clientes de ciência de dados que se conectem ao servidor.
  
+ Habilitar TCP/IP

  O TCP/IP é necessário para conexões de loopback ao SQL Server R Services. Se você receber o erro a seguir, habilite o TCP/IP na máquina virtual que oferece suporte à instância do:

  "DBNETLIB; SQL Server não existe ou acesso negado"

## <a name="how-to-disable-r-services-on-an-instance"></a>Como desabilitar o R Services em uma instância

Você também pode habilitar ou desabilitar o recurso em uma máquina virtual existente a qualquer momento.

1. Abra a folha da máquina virtual
2. Clique em **Configurações** e selecione **Configuração do SQL Server**.

## <a name="existing"></a>Adicionar o SQL Server R Services a uma máquina de virtual existente do SQL Server 2016 Enterprise

Se você tiver criado uma máquina virtual do Azure que não inclui serviços de R, você pode adicionar o recurso seguindo estas etapas:

1. Execute novamente a configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e adicione o recurso da página **Configuração do Servidor** do assistente.
2. Habilite a execução de scripts externos e reinicie a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Configurar o SQL Server R Services (no Banco de Dados)](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Se isto for necessário para a execução de scripts remotos, configure o acesso de banco de dados para contas de trabalho do R.
   Para obter mais informações, consulte [Configurar o SQL Server R Services (no Banco de Dados)](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Se você pretende permitir a execução de scripts R de clientes de ciência de dados remotos, modifique uma regra de firewall na máquina virtual do Azure. Para obter mais informações, consulte [Desbloquear firewall](#firewall).
4. Instale ou habilite as bibliotecas de rede necessárias. Para obter mais informações, consulte [Adicionar protocolos de rede](#network).

## <a name="related-resources"></a>Recursos relacionados

[Configurar o SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

