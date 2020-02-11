---
title: Criar um grupo e um servidor de gerenciamento central
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- configuration server
ms.assetid: da265482-3953-440a-ac23-0ab7e42a55eb
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 17c1e63789e9c2069d8fdecd8bd62b64bf8a886d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75244655"
---
# <a name="create-a-central-management-server-and-server-group-sql-server-management-studio"></a>Criar um servidor de gerenciamento central e um grupo de servidores (SQL Server Management Studio)
  Este tópico descreve como designar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como servidor central de gerenciamento no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Os servidores de gerenciamento central armazenam uma lista de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é organizada em um ou mais grupos de servidores de gerenciamento Central. As ações executadas com um grupo de servidores de gerenciamento central afetarão todos os servidores do grupo. Isso inclui a conexão a servidores usando o Pesquisador de Objetos e a execução de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e de políticas de Gerenciamento Baseado em Política em vários servidores ao mesmo tempo.  
  
> [!NOTE]  
>  As versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] não podem ser designadas como um servidor de gerenciamento central.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar um servidor de gerenciamento central e um grupo de servidores, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Duas funções no banco de dados msdb concedem acesso aos servidores de gerenciamento central. Somente os membros da função ServerGroupAdministratorRole podem administrar o servidor de gerenciamento central. A associação à função ServerGroupReaderRole é necessária para conectar a um servidor de gerenciamento central.  
  
 Como as conexões mantidas por um servidor de gerenciamento central são executadas no contexto do usuário com o uso da Autenticação do Windows, as permissões efetivas nos servidores registrados podem variar. Por exemplo, o usuário pode ser membro da função de servidor fixa sysadmin na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A, mas pode ter permissões limitadas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Os procedimentos a seguir descrevem como executar as seguintes etapas.  
  
1.  Crie um servidor central de gerenciamento.  
  
2.  Adicione um ou mais grupos de servidores ao servidor central de gerenciamento e adicione um ou mais servidores registrados aos grupos de servidores.  
  
#### <a name="create-a-central-management-server"></a>Criar um servidor central de gerenciamento  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Exibir** , clique em **Servidores Registrados**.  
  
2.  Em Servidores Registrados, expanda **Mecanismo de Banco de Dados**, clique com o botão direito do mouse em **Servidores Centrais de Gerenciamento**e clique em **Registrar Servidor Central de Gerenciamento**.  
  
3.  Na caixa de diálogo **Novo Registro de Servidor** , selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você deseja transformar em servidor central de gerenciamento central na lista suspensa de servidores. Você deve usar a Autenticação do Windows para o servidor central de gerenciamento.  
  
4.  Em **Servidor Registrado**, digite um nome de servidor e uma descrição opcional.  
  
5.  Na guia de **Propriedades da Conexão** , revise ou modifique as propriedades da rede e da conexão. Para obter mais informações, consulte [Conectar ao Servidor &#40;página Propriedades da Conexão&#41; Mecanismo de Banco de Dados](../f1-help/connect-to-server-connection-properties-page-database-engine.md)  
  
6.  Clique em **Testar**para testar a conexão.  
  
7.  Clique em **Save** (Salvar). A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aparecerá na pasta **Servidores Centrais de Gerenciamento** .  
  
#### <a name="create-a-new-server-group-and-add-servers-to-the-group"></a>Criar um novo grupo de servidores e adicionar servidores ao grupo  
  
1.  Em **Servidores Registrados**, expanda **Servidores Centrais de Gerenciamento**. Clique com o botão direito do mouse na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adicionada ao procedimento anterior e selecione **Novo Grupo de Servidores**.  
  
2.  Em **Propriedades do Novo Grupo de Servidores**, digite um nome de grupo e uma descrição opcional.  
  
3.  Em **Servidores Registrados**, clique com o botão direito do mouse no grupo de servidores e clique em **Novo Registro de Servidor**.  
  
4.  Em Novo Registro de Servidor, selecione uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Criar um novo servidor registrado &#40;SQL Server Management Studio&#41;](create-a-new-registered-server-sql-server-management-studio.md). Adicione mais servidores conforme apropriado.  
  
#### <a name="to-execute-queries-against-several-configuration-targets-at-the-same-time"></a>Para executar consultas em vários destinos de configuração ao mesmo tempo  
  
-   Depois de criar um servidor de gerenciamento central, um ou mais grupos de servidores e um ou mais servidores registrados, você poderá executar consultas simultâneas no grupo inteiro. Para obter mais informações sobre como executar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] nos servidores em um grupo de servidores ao mesmo tempo, consulte [Executar instruções em vários servidores simultaneamente &#40;SQL Server Management Studio&#41;](execute-statements-against-multiple-servers-simultaneously.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar vários servidores usando os Servidores de Gerenciamento Centrais](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
