---
title: Habilitar conexões criptografadas com o Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2019
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- TLS [SQL Server]
- Transport Layer Security (TLS)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
- TLS certificates
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 53ca4d2631e41e0a815dbf240fc0a7006ec8ce8b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75252856"
---
# <a name="enable-encrypted-connections-to-the-database-engine"></a>Habilitar conexões criptografadas com o Mecanismo de Banco de Dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como habilitar conexões criptografadas para uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] especificando um certificado para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. O computador servidor deve ter um certificado configurado e a máquina cliente deve estar configurada para confiar na autoridade raiz do certificado. Provisionamento é o processo de instalar um certificado importando-o para o Windows.  
  
> [!IMPORTANT]
> Após o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o protocolo SSL foi descontinuado. Use o protocolo TLS em vez disso.

## <a name="transport-layer-security-tls"></a>Protocolo TLS
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar o Protocolo TLS para criptografar dados transmitidos em uma rede entre uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um aplicativo cliente. A criptografia TLS é realizada dentro da camada de protocolo e está disponível para todos os clientes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com suporte.
O TLS pode ser usado para validação de servidor quando uma conexão de cliente solicita criptografia. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executada em um computador ao qual foi atribuído um certificado de uma autoridade de certificação pública, a identidade do computador e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão emitidas pela cadeia de certificados que leva à autoridade raiz confiável. Essa validação de servidor exige que o computador no qual o aplicativo cliente está sendo executado seja configurado para confiar na autoridade raiz do certificado que é usado pelo servidor. A criptografia com um certificado autoassinado é possível e está descrita na seção a seguir, mas um certificado autoassinado oferece apenas proteção limitada.
O nível de criptografia usado pelo TLS, 40 ou 128 bits, depende da versão do sistema operacional do Microsoft Windows em execução no aplicativo e nos computadores do banco de dados.

> [!WARNING]
> O uso do nível de criptografia de 40 bits é considerado inseguro.

> [!WARNING]
> As conexões TLS criptografadas usando um certificado autoassinado não fornecem alta segurança. Elas são suscetíveis a ataques “man-in-the-middle”. Não se deve confiar no TLS usando certificados autoassinados em um ambiente de produção ou em servidores conectados à Internet.

A habilitação da criptografia TLS aumenta a segurança dos dados transmitidos pelas redes entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicativos. No entanto, quando todo o tráfego entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um aplicativo cliente é criptografado usando TLS, o seguinte processamento adicional é necessário:
-  Idas e voltas extras da rede são necessárias no momento da conexão.
-  Os pacotes enviados do aplicativo para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser criptografados pela pilha TLS do cliente e descriptografados pela pilha TLS do servidor.
-  Os pacotes enviados da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o aplicativo devem ser criptografados pela pilha TLS do servidor e descriptografados pela pilha TLS do cliente.

## <a name="remarks"></a>Comentários
 O certificado deve ser emitido para **Autenticação do Servidor**. O nome do certificado deve ser o FQDN (nome de domínio totalmente qualificado) do computador.  
  
 Os certificados são armazenados localmente para os usuários no computador. Para instalar um certificado para uso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é necessário executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager com uma conta que tem privilégios de administrador local.

 O cliente deve poder verificar a propriedade do certificado usado pelo servidor. Se o cliente tiver o certificado de chave pública da autoridade de certificação que assinou o certificado de servidor, nenhuma outra configuração será necessária. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows inclui os certificados de chave pública de muitas autoridades de certificação. Se o certificado do servidor foi assinado por uma autoridade de certificação pública ou privada para a qual o cliente não tem o certificado de chave pública, será necessário instalar o certificado de chave pública da autoridade de certificação que assinou o certificado do servidor.  
  
> [!NOTE]  
> Para usar critografia com um cluster de failover, você deve instalar o certificado de servidor com o nome DNS completamente qualificado do servidor virtual em todos os nós no cluster de failover. Por exemplo, se você tiver um cluster de dois nós, com nós chamados ***test1.\*\<sua empresa>\*.com*** e ***test2.\*\<sua empresa>\*.com*** e tiver um servidor virtual chamado ***virtsql***, será necessário instalar um certificado para ***virtsql.\*\<sua empresa>\*.com*** nos dois nós. É possível definir o valor da opção **ForceEncryption** na caixa de propriedade **Protocolos para virtsql** de **Configuração de Rede do SQL Server** como **Sim**.

> [!NOTE]
> Ao criar conexões criptografadas para um indexador do Azure Search para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma VM do Azure, confira [Configurar uma conexão de um indexador do Azure Search para SQL Server em uma VM do Azure](https://azure.microsoft.com/documentation/articles/search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers/). 

## <a name="certificate-requirements"></a>Requisitos de certificado
Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carregar um certificado TLS, o certificado deve atender às seguintes condições:

- O certificado deve estar no repositório de certificado do computador local ou no armazenamento de certificado do usuário atual.

- A Conta de Serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter a permissão necessária para acessar o certificado TLS.

- A hora do sistema atual deve ser posterior à propriedade **Válido de** do certificado e anterior à propriedade Válido para do certificado.

- O certificado deve ser significativo para a autenticação do servidor. Isso exige a propriedade **Uso Avançado de Chave** do certificado para especificar a **Autenticação do Servidor (1.3.6.1.5.5.7.3.1)** .

- O certificado deve ser criado usando a opção **KeySpec** de **AT_KEYEXCHANGE**. Normalmente, a propriedade de uso de chave do certificado (**KEY_USAGE**) também incluirá a codificação de chaves (**CERT_KEY_ENCIPHERMENT_KEY_USAGE**).

- A propriedade **Assunto** do certificado deve indicar que o nome comum (CN) é igual ao nome do host ou ao nome de domínio totalmente qualificado (FQDN) do computador servidor. Ao usar o nome do host, o sufixo DNS precisa ser especificado no certificado. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver em execução em um cluster de failover, o nome comum deverá corresponder ao nome do host ou ao FQDN do servidor virtual e os certificados deverão ser fornecidos em todos os nós no cluster de failover.

- O [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] e o [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SNAC (Cliente Nativo) dão suporte a certificados curinga. O SNAC foram preteridos desde então e substituídos pelo [Driver do Microsoft OLE DB para SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) e [Microsoft ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md). Outros clientes podem não dar suporte a certificados curinga. Para obter mais informações, confira a documentação do cliente e o [KB 258858](https://support.microsoft.com/kb/258858).       
  O certificado curinga não pode ser selecionado usando o SQL Server Configuration Manager. Para usar um certificado curinga, é necessário editar a chave do Registro `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQLServer\SuperSocketNetLib` e inserir a impressão digital do certificado, sem espaços, no valor **Certificado**.  

  > [!WARNING]  
  > [!INCLUDE[ssnoteregistry_md](../../includes/ssnoteregistry-md.md)]  

## <a name="to-provision-install-a-certificate-on-a-single-server"></a>Para provisionar (instalar) um certificado em um servidor único  
Com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], o gerenciamento de certificados integra-se ao SQL Server Configuration Manager. O SQL Server Configuration Manager para [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] pode ser usado com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Consulte [Gerenciamento de Certificado (SQL Server Configuration Manager)](../../database-engine/configure-windows/manage-certificates.md) para adicionar um certificado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] única.

Se estiver usando [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e o SQL Server Configuration Manager para [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] não estiver disponível, siga estas etapas:

1. No menu **Iniciar** , clique em **Executar**e na caixa **Abrir** , digite **MMC** e clique em **OK**.  
  
2. No console do MMC, no menu **Arquivo** , clique em **Adicionar/Remover Snap-in**.  
  
3. Na caixa de diálogo **Adicionar/Remover Snap-in** , clique em **Adicionar**.  
  
4. Na caixa de diálogo **Adicionar Snap-in Autônomo** , clique em **Certificados**e em **Adicionar**.  
  
5. Na caixa de diálogo **Snap-in de certificados** , clique em **Conta de computador**e em **Concluir**.  
  
6. Na caixa de diálogo **Adicionar Snap-in Autônomo** , clique em **Fechar.**  
  
7. Na caixa de diálogo **Adicionar/Remover Snap-in** , clique em **OK**.  
  
8. No snap-in de **Certificados** , expanda **Certificados**, expanda **Pessoal**, clique com o botão direito do mouse em **Certificados**, aponte para **Todas as Tarefas**e clique em **Importar**.  

9. Clique com o botão direito do mouse no certificado importado, aponte para **Todas as Tarefas**e clique em **Gerenciar Chaves Privadas**. Na caixa de diálogo **Segurança**, adicione a permissão de leitura para a conta de usuário usada pela conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
10. Complete o **Assistente para Importação de Certificados**, para adicionar um certificado ao computador e feche o console MMC. Para obter mais informações sobre como adicionar um certificado a um computador, consulte sua documentação do Windows.  
  
## <a name="to-provision-install-a-certificate-across-multiple-servers"></a>Para provisionar (instalar) um certificado em vários servidores
Com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], o gerenciamento de certificados integra-se ao SQL Server Configuration Manager. O SQL Server Configuration Manager para [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] pode ser usado com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Consulte [Gerenciamento de Certificados (SQL Server Configuration Manager)](../../database-engine/configure-windows/manage-certificates.md) para adicionar um certificado em uma configuração do Cluster de Failover ou em uma configuração do Grupo de Disponibilidade.

Se estiver usando o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e o SQL Server Configuration Manager para [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] não estiver disponível, siga as etapas na seção [Provisionar (instalar) um certificado em um único servidor](#to-provision-install-a-certificate-on-a-single-server) para cada servidor.

## <a name="to-export-the-server-certificate"></a>Para exportar o certificado de servidor  
  
1. No snap-in de **Certificados** , localize o certificado na pasta **Certificados** / **Pessoal** , clique com o botão direito do mouse em **Certificado**, aponte para **Todas as Tarefas**e clique em **Exportar**.  
  
2. Complete o **Assistente para Exportação de Certificados**armazenando o arquivo de certificado em um local conveniente.  
  
## <a name="to-configure-the-server-to-force-encrypted-connections"></a>Para configurar o servidor para forçar conexões criptografadas

> [!IMPORTANT]
> A conta de serviço do SQL Server deve ter permissões de leitura no certificado usado para forçar a criptografia no SQL Server. Para uma conta de serviço sem privilégios, as permissões de leitura precisarão ser adicionadas ao certificado. A falha em fazer isso pode fazer com que a reinicialização do serviço do SQL Server falhe.
  
1. No **SQL Server Configuration Manager**, expanda **Configuração de Rede do SQL Server**, clique com o botão direito do mouse em **Protocolos para** _\<server instance>_ e selecione**Propriedades**.  
  
2. Na caixa de diálogo **Protocolos para** _\<instance name>_ **Propriedades**, na guia **Certificado**, selecione o certificado desejado na lista suspensa da caixa **Certificado** e clique em **OK**.  
  
3. Na guia **Sinalizadores** , na caixa **ForceEncryption** , selecione **Sim**e clique em **OK** para fechar a caixa de diálogo.  
  
4. Reinicie o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

> [!NOTE]
> Para garantir a conectividade segura entre o cliente e o servidor, configure o cliente para solicitar conexões criptografadas. Mais detalhes são explicados [mais adiante neste artigo](#to-configure-the-client-to-request-encrypted-connections).

## <a name="to-configure-the-client-to-request-encrypted-connections"></a>Para configurar o cliente para solicitar conexões criptografadas  

1. Copie o certificado original ou o arquivo de certificado exportado no computador cliente.  
  
2. No computador cliente, use o snap-in de **Certificados** para instalar o certificado raiz ou o arquivo do certificado exportado.  
  
3. Usando o SQL Server Configuration Manager, clique com o botão direito do mouse em **Configuração do SQL Server Native Client** e clique em **Propriedades**.  
  
4. Na página **Sinalizadores** , na caixa **Forçar criptografia de protocolo** , clique em **Sim**.  
  
## <a name="to-encrypt-a-connection-from-sql-server-management-studio"></a>Para criptografar uma conexão do SQL Server Management Studio  
  
1. Na barra de ferramentas do Pesquisador de Objetos, clique em **Conectar**e clique em **Mecanismo de Banco de Dados**.  
  
2. Na caixa de diálogo **Conectar ao Servidor** , complete as informações de conexão e clique em **Opções**.  
  
3. Na guia **Propriedades de Conexão** , clique em **Criptografar conexão**.  

## <a name="internet-protocol-security-ipsec"></a>Protocolo IPsec
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser criptografado durante a transmissão usando o IPSec. O IPSec é fornecido pelos sistemas operacionais do cliente e servidor e não requer nenhuma configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre o IPSec, consulte a documentação de rede ou do Windows.

## <a name="see-also"></a>Consulte Também
[Suporte a TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/kb/3135244)     
[Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)     
