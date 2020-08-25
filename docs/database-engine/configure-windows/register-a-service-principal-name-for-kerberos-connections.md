---
title: Registrar um nome de entidade de serviço para conexões de Kerberos
description: Saiba como registrar um SPN (nome da entidade de serviço) com o Active Directory. Esse registro é necessário para usar a autenticação Kerberos com o SQL Server.
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SPNs
- network connections [SQL Server], SPNs
- registering SPNs
- Server Principal Names
- SPNs [SQL Server]
ms.assetid: e38d5ce4-e538-4ab9-be67-7046e0d9504e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 08/12/2020
ms.openlocfilehash: 242b87166035c8ffc0e01272b5910f85a66620e7
ms.sourcegitcommit: bf5acef60627f77883249bcec4c502b0205300a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88200679"
---
# <a name="register-a-service-principal-name-for-kerberos-connections"></a>Registrar um nome de entidade de serviço para conexões de Kerberos

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

 Para usar a autenticação Kerberos com o SQL Server, é preciso atender a estas duas condições:  

- Os computadores cliente e servidor devem fazer parte do mesmo domínio do Windows ou de domínios confiáveis.  

- Um SPN (Nome da Entidade de Serviço) deve ser registrado no Active Directory, o qual assume a função do Centro de Distribuição de Chaves em um domínio Windows. O SPN, depois de registrado, é mapeado para a conta do Windows que iniciou o serviço da instância do SQL Server. Se o registro do SPN não tiver sido realizado ou tiver falhado, a camada de segurança do Windows não poderá determinar a conta associada ao SPN e a autenticação Kerberos não será usada.

    > [!NOTE]  
    >  Se o servidor não puder registrar automaticamente o SPN, será necessário registrá-lo manualmente. Veja [Registro manual de SPN](#Manual).  

É possível verificar se uma conexão está usando Kerberos consultando a exibição de gerenciamento dinâmico sys.dm_exec_connections. Execute a consulta a seguir e verifique o valor da coluna auth_scheme, que será "KERBEROS" se Kerberos estiver habilitado.

```sql
SELECT auth_scheme FROM sys.dm_exec_connections WHERE session_id = @@spid ;
```

> [!TIP]
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager para SQL Server** é uma ferramenta de diagnóstico que ajuda a solucionar problemas do Kerberos relativos à conectividade com o SQL Server. Para obter mais informações, consulte [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  

##  <a name="the-role-of-the-spn-in-authentication"></a><a name="Role"></a> A função do SPN na autenticação  

Quando um aplicativo abre uma conexão e usa a Autenticação do Windows, o SQL Server Native Client passa o nome do computador, o nome da instância e, opcionalmente, um SPN do SQL Server. Se a conexão passar um SPN, ele será usado sem qualquer alteração.  

Se a conexão não passar um SPN, um SPN padrão será construído a partir do protocolo usado, do nome do servidor e do nome da instância.  

Em ambos os casos, o SPN é enviado ao centro de distribuição de chave para obter um token de segurança para autenticar a conexão. Se não for possível obter um token de segurança, a autenticação usará o NTLM.  

Um SPN (nome da entidade de serviço) é o nome pelo qual um cliente identifica exclusivamente uma instância de um serviço. O serviço de autenticação Kerberos pode usar um SPN para autenticar um serviço. Quando um cliente deseja se conectar a um serviço, ele localiza uma instância do serviço, compõe um SPN para essa instância, conecta-se ao serviço e apresenta o SPN para autenticação do serviço.  
  
> [!NOTE]  
>  As informações fornecidas neste tópico também se aplicam a configurações do SQL Server que usam clustering.  
  
A Autenticação do Windows é o método preferencial de os usuários se autenticarem no SQL Server. Os clientes que usam a Autenticação do Windows são autenticados usando NTLM ou Kerberos. Em um ambiente do Active Directory, a autenticação Kerberos é sempre tentada primeiro. A autenticação Kerberos não está disponível para clientes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que usam pipes nomeados.  

##  <a name="permissions"></a><a name="Permissions"></a> Permissões

Quando o serviço do Mecanismo de Banco de Dados é iniciado, ele tenta registrar o SPN (nome da entidade de serviço). Suponha que a conta que está iniciando o SQL Server não tenha permissão para registrar um SPN no Active Directory Domain Services. Nesse caso, essa chamada falha, e uma mensagem de aviso é registrada no log de eventos do aplicativo, bem como no log de erros do SQL Server. Para registrar o SPN, é necessário que o Mecanismo de Banco de Dados esteja em execução em uma conta interna, como Sistema Local (não recomendado) ou SERVIÇO DE REDE, ou em uma conta com permissão para registrar um SPN. Você pode registrar um SPN usando uma conta de administrador de domínio, mas isso não é recomendável em um ambiente de produção. Quando o SQL Server é executado nos sistemas operacionais Windows 7 ou Windows Server 2008 R2, é possível executar o SQL Server usando uma conta virtual ou uma MSA (conta de serviço gerenciado). Tanto contas virtuais quanto MSAs podem registrar um SPN. Se o SQL Server não estiver em execução em uma dessas contas, o SPN não será registrado na inicialização, e o administrador do domínio deverá registrar o SPN manualmente.

> [!NOTE]  
>  Quando o domínio do Windows estiver configurado para execução em um nível inferior ao nível funcional do Windows Server 2008 R2, a Conta de Serviço Gerenciado não terá as permissões necessárias para registrar os SPNs do serviço do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Se a autenticação Kerberos for necessária, o Administrador de Domínio deverá registrar manualmente os SPNs do SQL Server na Conta de Serviço Gerenciado.

Informações adicionais estão disponíveis em [Como implementar a delegação restrita de Kerberos com o SQL Server 2008](https://technet.microsoft.com/library/ee191523.aspx)  

##  <a name="spn-formats"></a><a name="Formats"></a> Formatos de SPN

Começando pelo [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o formato de SPN é alterado para dar suporte à autenticação Kerberos em TCP/IP, pipes nomeados e memória compartilhada. Os formatos de SPN com suporte para instâncias padrão e nomeadas são os seguintes:  
  
**Instância nomeada**  
  
-   **MSSQLSvc/\<FQDN>:[\<port> | \<instancename>]** , em que:  
  
    -   **MSSQLSvc** é o serviço que está sendo registrado.  
  
    -   **\<FQDN>** é o nome de domínio totalmente qualificado do servidor.  
  
    -   **\<port>** é o número da porta TCP.  
  
    -   **\<instancename>** é o nome da instância do SQL Server.  
  
**Instância padrão**  
  
-   **MSSQLSvc/\<FQDN>:\<port>**  | **MSSQLSvc/\<FQDN>** , em que:  
  
    -   **MSSQLSvc** é o serviço que está sendo registrado.  
  
    -   **\<FQDN>** é o nome de domínio totalmente qualificado do servidor.  
  
    -   **\<port>** é o número da porta TCP.  
  
    > [!NOTE]
    > O novo formato de SPN não requer um número da porta. Ou seja, um servidor de várias portas ou um protocolo que não usa números de porta pode usar a autenticação Kerberos.  
   
|Formato de SPN|Descrição|  
|-|-|  
|MSSQLSvc/\<FQDN>:\<port>|O SPN padrão gerado pelo provedor quando o protocolo TCP é usado. \<port> é um número da porta TCP.|  
|MSSQLSvc/\<FQDN>|O SPN padrão gerado pelo provedor para uma instância padrão quando um protocolo diferente de TCP é usado. \<FQDN> é um nome de domínio totalmente qualificado.|  
|MSSQLSvc/\<FQDN>:\<instancename>|O SPN padrão gerado pelo provedor para uma instância nomeada quando um protocolo diferente de TCP é usado. \<instancename> é o nome de uma instância do SQL Server.|  

> [!NOTE]  
> No caso de uma conexão TCP/IP, na qual a porta TCP é incluída no SPN, é necessário que o SQL Server habilite o protocolo TCP para que um usuário se conecte usando a autenticação Kerberos. 

##  <a name="automatic-spn-registration"></a><a name="Auto"></a> Registro automático de SPN  

Quando uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] é iniciada, o SQL Server tenta registrar o SPN para o serviço SQL Server. Quando a instância é interrompida, o SQL Server tenta cancelar o registro do SPN. Em uma conexão TCP/IP, o SPN é registrado no formato *MSSQLSvc/\<FQDN>* : *\<tcpport>* . Tanto as instâncias nomeadas quanto as instâncias padrão são registradas como *MSSQLSvc*, dependendo do valor de *\<tcpport>* para fazer a diferenciação entre as instâncias.  
  
Para outras conexões que oferecem suporte a Kerberos, o SPN é registrado no formato *MSSQLSvc/\<FQDN>* / *\<instancename>* para uma instância nomeada. O formato para registrar uma instância padrão é *MSSQLSvc/\<FQDN>* .  

Talvez seja necessária a intervenção manual para registrar ou cancelar o SPN se a conta do serviço não tiver as permissões necessárias para essas ações.  

##  <a name="manual-spn-registration"></a><a name="Manual"></a> Registro manual de SPN  

Para registrar um SPN manualmente, é necessário que o administrador use a ferramenta Setspn.exe fornecida com as Ferramentas de Suporte [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] da Microsoft. Para obter mais informações, veja o artigo da Base de Dados de Conhecimento sobre [Ferramentas de suporte do Windows Server 2003 Service Pack 1](https://support.microsoft.com/kb/892777) .  

Setspn.exe é uma ferramenta de linha de comando que permite ao usuário ler, modificar e excluir a propriedade de diretório de SPNs (nome da entidade de serviço). Essa ferramenta também permite ao usuário exibir os SPNs atuais, redefinir SPNs padrão da conta e adicionar ou excluir SPNs complementares.  

O seguinte exemplo ilustra a sintaxe usada para registrar manualmente um SPN para uma conexão TCP/IP usando uma conta de usuário de domínio:  

```
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:1433 redmond\accountname  
```

> [!NOTE]
> Se já houver um SPN, ele deverá ser excluído antes de ser registrado novamente. É possível fazer isso usando o comando `setspn` juntamente com a opção `-D` . Os exemplos a seguir ilustram como registrar manualmente um novo SPN com base em instância. Para uma instância padrão que usa uma conta de usuário de domínio, use:  

```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com redmond\accountname  
```  
  
Para uma instância nomeada, use:  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:instancename redmond\accountname  
```  
  
##  <a name="client-connections"></a><a name="Client"></a> Conexões cliente  

Há suporte para SPNs especificados pelo usuário nos drivers cliente. No entanto, se um SPN não for fornecido, ele será gerado automaticamente com base no tipo de conexão cliente. Para uma conexão TCP, um SPN no formato *MSSQLSvc*/*FQDN*:[*port*] é usado tanto para instâncias nomeadas quanto para instâncias padrão.  
  
Para pipes nomeados e conexões de memória compartilhada, um SPN no formato *MSSQLSvc/\<FQDN>:\<instancename>* é usado para uma instância nomeada e *MSSQLSvc/\<FQDN>* é usado para a instância padrão.  
  
**Usando uma conta de serviço como um SPN**  
  
Contas de serviço podem ser usadas como um SPN. Elas são especificadas pelo atributo de conexão para autenticação Kerberos e têm os seguintes formatos:  
  
- **username\@domain** ou **domain\username** para uma conta de usuário de domínio  

- **machine$\@domain** ou **host\FQDN** para uma conta de domínio de computador, como Sistema Local ou SERVIÇOS DE REDE.  

Para determinar o método de autenticação de uma conexão, execute a seguinte consulta.  
  
```sql  
SELECT net_transport, auth_scheme   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
``` 

##  <a name="authentication-defaults"></a><a name="Defaults"></a> Padrões de autenticação  

A tabela a seguir descreve os padrões de autenticação usados com base em cenários de registro de SPN.  
  
|Cenário|Método de autenticação|  
|--------------|---------------------------|  
|O SPN faz o mapeamento para a conta de domínio correta, conta virtual, MSA ou conta interna. Por exemplo, Sistema Local ou SERVIÇO DE REDE.|Conexões locais usam NTLM, conexões remotas usam Kerberos.|  
|O SPN faz o mapeamento para a conta de domínio correta, conta virtual, MSA ou conta interna.|Conexões locais usam NTLM, conexões remotas usam Kerberos.|  
|O SPN faz o mapeamento para a conta de domínio incorreta, conta virtual, MSA ou conta interna.|A autenticação falha.|  
|A pesquisa de SPN falha ou não faz o mapeamento correto para uma conta de domínio, conta virtual, MSA ou conta interna ou não é uma conta de domínio correta, conta virtual, MSA ou conta interna.|Conexões locais e remotas usam NTLM.|  

> [!NOTE]
> "Correto" significa que a conta mapeada pelo SPN registrado é a conta na qual o serviço do SQL Server está em execução.  

##  <a name="comments"></a><a name="Comments"></a> Comentários  

A DAC (conexão de administrador dedicada) usa um SPN com base no nome da instância. A autenticação Kerberos poderá ser usada com DAC se o SPN tiver sido registrado com êxito. Como alternativa, um usuário poderá especificar o nome de conta como um SPN.

Se o registro de SPN falhar durante a inicialização, essa falha será registrada no log de erros do SQL Server e a inicialização continuará.  

Se o cancelamento de registro do SPN falhar durante o desligamento, essa falha será registrada no log de erros do SQL Server e o desligamento prosseguirá.  

## <a name="see-also"></a>Consulte Também  
- [Suporte a SPN &#40;Nome da Entidade de Serviço&#41; em conexões de cliente](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)
- [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)
- [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)
- [Recursos do SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)
- [Gerenciar problemas de autenticação Kerberos em um ambiente do Reporting Services](https://technet.microsoft.com/library/ff679930.aspx)
