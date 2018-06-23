---
title: Habilitar conexões criptografadas ao mecanismo de banco de dados (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
caps.latest.revision: 44
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 87550bc2c29485eaa1f4ad10e6ca82b79af19724
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012965"
---
# <a name="enable-encrypted-connections-to-the-database-engine-sql-server-configuration-manager"></a>Habilitar conexões criptografadas no Mecanismo de Banco de Dados (SQL Server Configuration Manager)
  Este tópico descreve como habilitar conexões criptografadas para uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] especificando um certificado para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. O computador servidor deve ter um certificado configurado e a máquina cliente deve estar configurada para confiar na autoridade raiz do certificado. Provisionamento é o processo de instalar um certificado importando-o para o Windows.  
  
 O certificado deve ser emitido para **Autenticação do Servidor**. O nome do certificado deve ser o FQDN (nome de domínio totalmente qualificado) do computador.  
  
 Os certificados são armazenados localmente para os usuários no computador. Para instalar um certificado para uso pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve estar executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager na mesma conta de usuário que o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que o serviço esteja sendo executado como LocalSystem, NetworkService ou LocalService. Neste caso você pode usar uma conta administrativa.  
  
 O cliente deve poder verificar a propriedade do certificado usado pelo servidor. Se o cliente tiver o certificado de chave pública da autoridade de certificação que assinou o certificado de servidor, nenhuma outra configuração será necessária. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows inclui os certificados de chave pública de muitas autoridades de certificação. Se o certificado do servidor foi assinado por uma autoridade de certificação pública ou privada para a qual o cliente não tem o certificado de chave pública, será necessário instalar o certificado de chave pública da autoridade de certificação que assinou o certificado do servidor.  
  
> [!NOTE]  
>  Para usar critografia com um cluster de failover, você deve instalar o certificado de servidor com o nome DNS completamente qualificado do servidor virtual em todos os nós no cluster de failover. Por exemplo, se você tiver um cluster de dois nós, com os nós chamados test1.*\<your company>*.com e test2.*\<your company>*.com e um servidor virtual chamado virtsql, precisará instalar um certificado para virtsql.*\<your company>*.com em ambos os nós. Você pode definir o valor da opção **ForceEncryption**como **Sim**.  
  
 **Neste tópico**  
  
-   **Para habilitar conexões criptografadas:**  
  
     [Provisionar (instalar) um certificado no servidor](#Provision)  
  
     [Exportar o certificado do servidor](#Export)  
  
     [Configurar o servidor para aceitar conexões criptografadas](#ConfigureServerConnections)  
  
     [Configurar o cliente para solicitar conexões criptografadas](#ConfigureClientConnections)  
  
     [Criptografar uma conexão do SQL Server Management Studio](#EncryptConnection)  
  
##  <a name="SSMSProcedure"></a>  
  
###  <a name="Provision"></a> Para instalar um certificado no servidor  
  
1.  No **iniciar** menu, clique em **executar**e no **abrir** , digite `MMC` e clique em **Okey**.  
  
2.  No console do MMC, no menu **Arquivo** , clique em **Adicionar/Remover Snap-in**.  
  
3.  Na caixa de diálogo **Adicionar/Remover Snap-in** , clique em **Adicionar**.  
  
4.  Na caixa de diálogo **Adicionar Snap-in Autônomo** , clique em **Certificados**e em **Adicionar**.  
  
5.  Na caixa de diálogo **Snap-in de certificados** , clique em **Conta de computador**e em **Concluir**.  
  
6.  Na caixa de diálogo **Adicionar Snap-in Autônomo** , clique em **Fechar.**  
  
7.  Na caixa de diálogo **Adicionar/Remover Snap-in** , clique em **OK**.  
  
8.  No snap-in de **Certificados**, expanda **Certificados**, expanda **Pessoal**, clique com o botão direito do mouse em **Certificados**, aponte para **Todas as Tarefas** e clique em **Importar**.  
  
9. Complete o **Assistente para Importação de Certificados**, para adicionar um certificado ao computador e feche o console MMC. Para obter mais informações sobre como adicionar um certificado a um computador, consulte sua documentação do Windows.  
  
###  <a name="Export"></a> Para exportar o certificado de servidor  
  
1.  No snap-in de **Certificados** , localize o certificado na pasta **Certificados** / **Pessoal** , clique com o botão direito do mouse em **Certificado**, aponte para **Todas as Tarefas**e clique em **Exportar**.  
  
2.  Complete o **Assistente para Exportação de Certificados**armazenando o arquivo de certificado em um local conveniente.  
  
###  <a name="ConfigureServerConnections"></a> Para configurar o servidor para aceitar conexões criptografadas  
  
1.  No **SQL Server Configuration Manager**, expanda **Configuração de Rede do SQL Server**, clique com o botão direito do mouse em **Protocolos de** *\<server instance>* e, depois, selecione **Propriedades**.  
  
2.  No **protocolos para *\<nome da instância >* **propriedades** caixa de diálogo de **certificado** guia, selecione o certificado desejado na lista suspensa para o **certificado** caixa e, em seguida, clique em **Okey**.  
  
3.  Na guia **Sinalizadores** , na caixa **ForceEncryption** , selecione **Sim**e clique em **OK** para fechar a caixa de diálogo.  
  
4.  Reinicie o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="ConfigureClientConnections"></a> Para configurar o cliente para solicitar conexões criptografadas  
  
1.  Copie o certificado original ou o arquivo de certificado exportado no computador cliente.  
  
2.  No computador cliente, use o snap-in de **Certificados** para instalar o certificado raiz ou o arquivo do certificado exportado.  
  
3.  No painel de console, clique com o botão direito do mouse em **Configuração do SQL Server Native Client**e clique em **Propriedades**.  
  
4.  Na página **Sinalizadores** , na caixa **Forçar criptografia de protocolo** , clique em **Sim**.  
  
###  <a name="EncryptConnection"></a> Para criptografar uma conexão do SQL Server Management Studio  
  
1.  Na barra de ferramentas do Pesquisador de Objetos, clique em **Conectar**e clique em **Mecanismo de Banco de Dados**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , complete as informações de conexão e clique em **Opções**.  
  
3.  Na guia **Propriedades de Conexão** , clique em **Criptografar conexão**.  
  
  