---
title: Registrar um nome da entidade de serviço para conexões Kerberos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SPNs
- network connections [SQL Server], SPNs
- registering SPNs
- Server Principal Names
- SPNs [SQL Server]
ms.assetid: e38d5ce4-e538-4ab9-be67-7046e0d9504e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5acd507be99d7ff36245e723d20aebc36f42a917
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62781991"
---
# <a name="register-a-service-principal-name-for-kerberos-connections"></a>Registrar um nome de entidade de serviço para conexões de Kerberos
  Para usar a autenticação Kerberos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é preciso satisfazer estas duas condições:  
  
-   Os computadores cliente e servidor devem fazer parte do mesmo domínio do Windows ou de domínios confiáveis.  
  
-   Um SPN (Nome da Entidade de Serviço) deve ser registrado no Active Directory, o qual assume a função do Centro de Distribuição de Chaves em um domínio Windows. O SPN, depois de registrado, é mapeado para a conta do Windows que iniciou o serviço da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se o registro do SPN não foi realizado ou falhou, a camada de segurança do Windows não poderá determinar a conta associada ao SPN e a autenticação Kerberos não será utilizada.  
  
    > [!NOTE]  
    >  Se o servidor não puder registrar automaticamente o SPN, será necessário registrá-lo manualmente. Veja [Registro manual de SPN](#Manual).  
  
 É possível verificar se uma conexão está usando Kerberos consultando a exibição de gerenciamento dinâmico sys.dm_exec_connections. Execute a consulta a seguir e verifique o valor da coluna auth_scheme, que será "KERBEROS" se Kerberos estiver habilitado.  
  
```  
SELECT auth_scheme FROM sys.dm_exec_connections WHERE session_id = @@spid ;  
```  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** é uma ferramenta de diagnóstico que ajuda a solucionar problemas de Kerberos relativos à conectividade com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
##  <a name="Role"></a> A função do SPN na autenticação  
 Quando um aplicativo abre uma conexão e usa a Autenticação do Windows, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client passa o nome do computador, o nome da instância e, opcionalmente, um SPN do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se a conexão passar um SPN, ele será usado sem qualquer alteração.  
  
 Se a conexão não passar um SPN, um SPN padrão será construído a partir do protocolo usado, do nome do servidor e do nome da instância.  
  
 Em ambos os casos, o SPN é enviado ao centro de distribuição de chave para obter um token de segurança para autenticar a conexão. Se não for possível obter um token de segurança, a autenticação usará o NTLM.  
  
 Um SPN (nome da entidade de serviço) é o nome pelo qual um cliente identifica exclusivamente uma instância de um serviço. O serviço de autenticação Kerberos pode usar um SPN para autenticar um serviço. Quando um cliente deseja se conectar a um serviço, ele localiza uma instância do serviço, compõe um SPN para essa instância, conecta-se ao serviço e apresenta o SPN para autenticação do serviço.  
  
> [!NOTE]  
>  As informações fornecidas neste tópico também se aplicam a configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usam clustering.  
  
 A Autenticação do Windows é o método preferencial de os usuários se autenticarem no SQL Server. Os clientes que usam a Autenticação do Windows são autenticados usando NTLM ou Kerberos. Em um ambiente do Active Directory, a autenticação Kerberos é sempre tentada primeiro. A autenticação Kerberos não está disponível para clientes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que usam pipes nomeados.  
  
##  <a name="Permissions"></a> Permissões  
 Quando o serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é iniciado, ele tenta registrar o SPN (Nome da Entidade de Serviço). Se a conta que estiver iniciando o SQL Server não tiver permissão para registrar um SPN nos Active Directory Domain Services, ocorrerá uma falha nessa chamada e uma mensagem de aviso será registrada no log de eventos do aplicativo, bem como no log de erros do SQL Server. Para registrar o SPN, é necessário que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] esteja em execução em uma conta interna, como Sistema Local (não recomendado) ou SERVIÇO DE REDE, ou uma conta com permissão para registrar um SPN, como a conta do administrador de domínio. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executado no sistema operacional  [!INCLUDE[win7](../../includes/win7-md.md)] ou  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] , você poderá executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando uma conta virtual ou uma conta de serviço gerenciada (MSA). Tanto contas virtuais quanto MSAs podem registrar um SPN. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver em execução em uma dessas contas, o SPN não será registrado na inicialização e o administrador do domínio deverá registrar o SPN manualmente.  
  
> [!NOTE]  
>  Quando o domínio do Windows é configurado para execução em um nível inferior ao nível funcional do [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Windows Server 2008 R2, a Conta de Serviço Gerenciada não tem as permissões necessárias para registrar os SPNs do serviço [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Se a autenticação Kerberos for necessária, o Administrador de Domínio deverá registrar manualmente os SPNs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na Conta de Serviço Gerenciada.  
  
 O artigo da Base de Dados de Conhecimento, [Como usar a autenticação Kerberos no SQL Server](https://support.microsoft.com/kb/319723), contém informações sobre como conceder permissões de leitura e gravação a um SPN de uma conta que não seja um Administrador de Domínio.  
  
 Informações adicionais estão disponíveis em [Como implementar a delegação restrita de Kerberos com o SQL Server 2008](https://technet.microsoft.com/library/ee191523.aspx)  
  
##  <a name="Formats"></a> Formatos de SPN  
 Começando pelo [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o formato de SPN é alterado para dar suporte à autenticação Kerberos em TCP/IP, pipes nomeados e memória compartilhada. Os formatos de SPN com suporte para instâncias padrão e nomeadas são os seguintes:  
  
 **Instância nomeada**  
  
-   *MSSQLSvc/FQDN*: [_porta_**|**_InstanceName_], em que:  
  
    -   *MSSQLSvc* é o serviço que está sendo registrado.  
  
    -   *FQDN* é o nome de domínio totalmente qualificado do servidor.  
  
    -   *Port* é o número da porta TCP.  
  
    -   *InstanceName* é o nome da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.  
  
 **Instância padrão**  
  
-   *MSSQLSvc/FQDN*:_porta_**|**_MSSQLSvc/FQDN_, em que:  
  
    -   *MSSQLSvc* é o serviço que está sendo registrado.  
  
    -   *FQDN* é o nome de domínio totalmente qualificado do servidor.  
  
    -   *Port* é o número da porta TCP.  
  
 O formato de SPN novo não requer um número de porta. Isso significa que um servidor de várias portas ou um protocolo que não usa números de porta pode usar a autenticação Kerberos.  
  
> [!NOTE]  
>  No caso de uma conexão TCP/IP, na qual a porta TCP é incluída no SPN, é necessário que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] habilite o protocolo TCP a um usuário para que ele se conecte usando a autenticação Kerberos.  
  
|||  
|-|-|  
|MSSQLSvc/*FQDN: porta*|O SPN padrão gerado pelo provedor quando o protocolo TCP é usado. *port* é um número de porta TCP.|  
|MSSQLSvc/*fqdn*|O SPN padrão gerado pelo provedor para uma instância padrão quando um protocolo diferente de TCP é usado. *fqdn* é um nome de domínio totalmente qualificado.|  
|MSSQLSvc/*FQDN: InstanceName*|O SPN padrão gerado pelo provedor para uma instância nomeada quando um protocolo diferente de TCP é usado. *InstanceName* é o nome de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
##  <a name="Auto"></a> Registro automático de SPN  
 Quando uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] é iniciada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta registrar o SPN para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando a instância é interrompida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta cancelar o SPN. Para uma conexão TCP/IP, o SPN é registrado no formato *MSSQLSvc/\<FQDN>* : *\<tcpport>* . Tanto as instâncias nomeadas quanto as instâncias padrão são registradas como *MSSQLSvc*, dependendo do valor *\<tcpport>* para fazer a diferenciação entre as instâncias.  
  
 Para outras conexões que dão suporte a Kerberos, o SPN é registrado no formato *MSSQLSvc/\<FQDN>*:*\<InstanceName>* para uma instância nomeada. O formato para registrar uma instância padrão é *MSSQLSvc/\<FQDN>* .  
  
 Talvez seja necessária a intervenção manual para registrar ou cancelar o SPN se a conta do serviço não tiver as permissões necessárias para essas ações.  
  
##  <a name="Manual"></a> Registro manual de SPN  
 Para registrar um SPN manualmente, é necessário que o administrador use a ferramenta Setspn.exe fornecida com as Ferramentas de Suporte [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] da Microsoft. Para obter mais informações, veja o artigo da Base de Dados de Conhecimento sobre [Ferramentas de suporte do Windows Server 2003 Service Pack 1](https://support.microsoft.com/kb/892777) .  
  
 O Setspn.exe é uma ferramenta de linha de comando que permite ao usuário ler, modificar e excluir a propriedade de diretório SPN (Nome da Entidade de Serviço). Essa ferramenta também permite ao usuário exibir os SPNs atuais, redefinir SPNs padrão da conta e adicionar ou excluir SPNs complementares.  
  
 O exemplo a seguir ilustra a sintaxe usada para registrar manualmente um SPN para uma conexão TCP/IP.  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:1433 accountname  
```  
  
 **Observação** Se um SPN já existir, ele deverá ser excluído antes que possa ser registrado novamente. É possível fazer isso usando o comando `setspn` juntamente com a opção `-D` . Os exemplos a seguir ilustram como registrar manualmente um novo SPN com base em instância. Para uma instância padrão, use:  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com accountname  
```  
  
 Para uma instância nomeada, use:  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:instancename accountname  
```  
  
##  <a name="Client"></a> Conexões cliente  
 Há suporte para SPNs especificados pelo usuário nos drivers cliente. Entretanto, se um SPN não for fornecido, será gerado automaticamente com base no tipo de conexão cliente. Para uma conexão TCP, um SPN no formato *MSSQLSvc*/*FQDN*:[*port*] é usado tanto para instâncias nomeadas quanto para instâncias padrão.  
  
 Para pipes nomeados e conexões de memória compartilhada, um SPN no formato *MSSQLSvc*/*FQDN*:*InstanceName* é usado para uma instância nomeada e o*FQDN* de *MSSQLSvc*/é usado para a instância padrão.  
  
 **Usando uma conta de serviço como um SPN**  
  
 Contas de serviço podem ser usadas como um SPN. Elas são especificadas pelo atributo de conexão para autenticação de Kerberos e têm os seguintes formatos:  
  
-   **username@domain** ou **domain\username** para uma conta de usuário de domínio  
  
-   **machine$@domain** ou **host\FQDN** de uma conta de domínio de computador, como Sistema Local ou SERVIÇOS DE REDE.  
  
 Para determinar o método de autenticação de uma conexão, execute a seguinte consulta.  
  
```sql  
SELECT net_transport, auth_scheme   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
##  <a name="Defaults"></a> Padrões de autenticação  
 A tabela a seguir descreve os padrões de autenticação usados com base em cenários de registro de SPN.  
  
|Cenário|Método de autenticação|  
|--------------|---------------------------|  
|O SPN faz o mapeamento para a conta de domínio correta, conta virtual, MSA ou conta interna. Por exemplo, Sistema Local ou SERVIÇO DE REDE.<br /><br /> Observação: correto significa que a conta mapeada pelo SPN registrado é a conta na qual o serviço de SQL Server está sendo executado.|Conexões locais usam NTLM, conexões remotas usam Kerberos.|  
|O SPN faz o mapeamento para a conta de domínio correta, conta virtual, MSA ou conta interna.<br /><br /> Observação: correto significa que a conta mapeada pelo SPN registrado é a conta na qual o serviço de SQL Server está sendo executado.|Conexões locais usam NTLM, conexões remotas usam Kerberos.|  
|O SPN faz o mapeamento para a conta de domínio incorreta, conta virtual, MSA ou conta interna.|A autenticação falha.|  
|A pesquisa de SPN falha ou não faz o mapeamento para uma conta de domínio correta, conta virtual, MSA ou conta interna ou não é uma conta de domínio correta, conta virtual, MSA ou conta interna.|Conexões locais e remotas usam NTLM.|  
  
##  <a name="Comments"></a> Comentários  
 A DAC (Conexão de Administrador Dedicada) usa um SPN com base no nome da instância. A autenticação Kerberos poderá ser usada com DAC se o SPN tiver sido registrado com êxito. Como alternativa, um usuário poderá especificar o nome de conta como um SPN.  
  
 Se o registro de SPN falhar durante a inicialização, essa falha será registrada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a inicialização continuará.  
  
 Se o cancelamento do SPN falhar durante o desligamento, essa falha será registrada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o desligamento prosseguirá.  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte a SPN &#40;Nome da Entidade de Serviço&#41; em conexões com o cliente](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)   
 [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)   
 [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)   
 [Recursos do SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Gerenciar problemas de autenticação Kerberos em um ambiente do Reporting Services](https://technet.microsoft.com/library/ff679930.aspx)  
  
  
