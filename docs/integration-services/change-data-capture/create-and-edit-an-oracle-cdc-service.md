---
title: "Criar e editar um serviço Oracle CDC | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- createSrv
ms.assetid: 10cd612e-d8f1-4af2-97d3-a0c22e1e2326
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7d6b89f2605cfdbc2f16cc2983171640362eb5b
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="create-and-edit-an-oracle-cdc-service"></a>Criar e editar um Serviço Oracle CDC
  Você cria e edita um novo Serviço do Windows do Oracle CDC a partir do Console de Configuração do Serviço CDC.  
  
 Para criar um novo Serviço do Windows do Oracle CDC, selecione **Serviços Locais de CDC** no painel esquerdo e clique em **Novo Serviço** no painel **Ações** . Você também pode clicar com o botão direito do mouse em **Serviços Locais de CDC** e selecionar **Novo Serviço**. O caixa de diálogo Novo Serviço do Windows do Oracle CDC é aberta.  
  
 **OR**  
  
 Para editar as propriedade de serviço CDC, selecione o serviço para o qual você deseja editar as propriedades e clique em **Propriedades** no painel **Ações** . Você também pode clicar com o botão direito do mouse no serviço com o qual você está trabalhando e selecionar **Propriedades**. A caixa de diálogo Propriedades do Serviço CDC será aberta.  
  
 Insira as informações a seguir na caixa de diálogo Novo Serviço do Windows do Oracle CDC ou na caixa de diálogo Propriedades de Serviço CDC.  
  
**Nome do Serviço**  
 Digite o nome do novo Serviço do Windows do Oracle CDC. Você não deve usar nomes longos, se possível. Os caracteres / e \ não podem ser usados no nome de serviço.  
  
> [!NOTE]  
> Esta opção não está disponível ao editar o serviço. Você não pode alterar o nome de um Serviço do Windows que já exist.  
  
 **Descrição**  
 Digite uma descrição do serviço para ajudar a identificá-lo.  
  
 **Conta de Serviço**  
 Selecione um dos seguintes para determinar sob qual conta se deve executar o serviço:  
  
-   **Conta Sistema Local**  
  
     Isto não é recomendado porque dá permissões demais ao serviço.  
  
-   **Esta conta**  
  
     No Windows Vista ou Windows Server 2008, a conta de serviço padrão é NETWORK SERVICE.  
  
     No Windows 7, Windows Server 2008 R2 e posterior, a conta de serviço padrão é NT Service\\<service-name>.  
  
     Usar estas contas permite que você trabalhe sem usar senhas, porque uma senha não é necessária para estas contas. Além disso, estas contas fornecem somente as permissões exigidas necessárias para que o Serviço Oracle CDC seja executado.  
  
     Você pode usar uma conta do Windows local ou de domínio para a conta de serviço. Neste caso, você deve inserir a **Senha** para essa conta. Esta conta pode ser para o host local ou uma conta de domínio. Atualize a senha quando ela for alterada usando os Serviços Locais no Painel de Controle do Windows.  
  
 **Nome do servidor**: selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino para se conectar (por exemplo, **\\\\<nome_do_computador>\\<nome_da_instância>**). Por padrão, é exibida a instância de servidor usada na última conexão.  
  
 **Autenticação**  
 Selecione uma destas opções:  
  
-   **Autenticação do Windows**: se você selecionar esta opção, o serviço Oracle CDC se conectará à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino usando a identidade da conta de serviço. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executada em um computador diferente, a Autenticação do Windows deverá ser usada com contas de domínio.  
  
-   **Autenticação do SQL Server**: se você selecionar esta opção, deverá digitar o **Nome de usuário** e **Senha** para o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que deseja usar. O serviço Oracle CDC usa estas credenciais ao conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 O logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado pelo Serviço Oracle CDC somente precisa ser um membro da função pública de servidor fixa, nenhum outro privilégio será necessário. Quando novas Instâncias Oracle CDC são adicionadas, esse logon ganhará acesso **db_owner** aos bancos de dados CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associados.  
  
 Para criar a definição de Serviço do Windows do Oracle CDC, o programa precisa de acesso de atualização ao banco de dados MSXDBCDC na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associada. Quando você clica em **OK**, uma caixa de diálogo solicita que o usuário insira um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com um acesso de atualização para o banco de dados MSXDBCDC.  
  
 Para obter informações sobre os dados que você deverá digitar na caixa de diálogo Conecte-se ao SQL Server, consulte [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md).  
  
 **Opções**  
 Clique na seta para exibir opções disponíveis a serem configuradas. Você pode escolher deixar estas opções com o valor padrão. As opções disponíveis são:  
  
-   **Tempo limite de conexão**: digite o tempo (em segundos) que o Serviço CDC para Oracle aguarda uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de exceder o tempo limite. O valor padrão é **15**.  
  
-   **Tempo limite de execução**: digite o tempo (em segundos) que o Serviço Windows do Oracle CDC aguarda até que um comando seja executado antes de exceder o tempo limite. O valor padrão é **30**.  
  
-   **Criptografar Conexão**: selecione **Criptografar Conexão** para a comunicação entre o Serviço Oracle CDC e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino usando uma conexão criptografada.  
  
-   **Avançado**: digite as propriedades de conexão adicionais, se necessário.  
  
 **Senha mestra**  
 Insira uma senha a ser usada pelo Serviço do Windows do Oracle CDC para proteger as credenciais da mineração de logs do Oracle.  
  
 A mesma senha mestre também deve ser usada quando outras instâncias são configuradas do mesmo serviço em outros nós em um cluster em configuração de alta disponibilidade. Se você perder ou modificar a senha mestra, todas as senhas de mineração de logs armazenadas em bancos de dados de Instância Oracle CDC devem ser reinseridas usando o CDC Designer Console.  
  
## <a name="see-also"></a>Consulte Também  
 [Como criar e editar um Serviço CDC](../../integration-services/change-data-capture/how-to-create-and-edit-a-cdc-service.md)  
  
  
