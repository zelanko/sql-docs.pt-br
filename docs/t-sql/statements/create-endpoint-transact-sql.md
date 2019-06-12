---
title: CREATE ENDPOINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENDPOINT
- CREATE ENDPOINT
- ENDPOINT_TSQL
- CREATE_ENDPOINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HTTP SOAP support [SQL Server]
- CREATE ENDPOINT statement
- Availability Groups [SQL Server], configuring
- endpoints [SQL Server], creating
- SOAP [SQL Server built-in support], endpoints
- SOAP [SQL Server built-in support], sqlbatch
- DATABASE_MIRRORING option
- HTTP protocol option [SQL Server]
- SOAP [SQL Server built-in support], ad hoc
- TCP protocol option [SQL Server]
- SERVICE_BROKER option
- Availability Groups [SQL Server], endpoint
ms.assetid: 6405e7ec-0b5b-4afd-9792-1bfa5a2491f6
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fc582f9328196233768e1fd7e7bd2bb81688c81d
ms.sourcegitcommit: 249c0925f81b7edfff888ea386c0deaa658d56ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66413446"
---
# <a name="create-endpoint-transact-sql"></a>CREATE ENDPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria pontos de extremidade e define suas propriedades, incluindo os métodos disponíveis para os aplicativos clientes. Para obter informações sobre permissões relacionadas, consulte [Permissões GRANT de ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
 A sintaxe para CREATE ENDPOINT pode ser dividida logicamente em duas partes:  
  
-   A primeira parte começa com AS e termina antes da cláusula FOR.  
  
     Nessa parte, você fornece informações específicas para o protocolo de transporte (TCP) e define um número de porta de escuta para o ponto de extremidade, como também o método de autenticação do ponto de extremidade e/ou uma lista de endereços IP (se houver) para os quais você quer restringir acesso ao ponto de extremidade.  
  
-   A segunda parte começa com a cláusula FOR.  
  
     Nessa parte, você define a carga útil que tem suporte no ponto de extremidade. A carga útil pode ser uma de vários tipos com suporte: [!INCLUDE[tsql](../../includes/tsql-md.md)], agente de serviços, espelhamento de banco de dados. Nesta parte, você inclui também informações específicas de linguagem.  
  
> **OBSERVAÇÃO:** Os Serviços Web XML nativos (pontos de extremidade SOAP/HTTP) foram removidos do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE ENDPOINT endPointName [ AUTHORIZATION login ]  
[ STATE = { STARTED | STOPPED | DISABLED } ]  
AS { TCP } (  
   <protocol_specific_arguments>  
        )  
FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING } (  
   <language_specific_arguments>  
        )  
  
<AS TCP_protocol_specific_arguments> ::=  
AS TCP (  
  LISTENER_PORT = listenerPort  
  [ [ , ] LISTENER_IP = ALL | ( xx.xx.xx.xx IPv4 address ) | ( '__:__1' IPv6 address ) ]  
  
)  
  
<FOR SERVICE_BROKER_language_specific_arguments> ::=  
FOR SERVICE_BROKER (  
   [ AUTHENTICATION = {   
            WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ [ , ] ENCRYPTION = { DISABLED | { { SUPPORTED | REQUIRED }   
       [ ALGORITHM { AES | RC4 | AES RC4 | RC4 AES } ] }   
   ]  
   [ [ , ] MESSAGE_FORWARDING = { ENABLED | DISABLED } ]  
   [ [ , ] MESSAGE_FORWARD_SIZE = forward_size ]  
)  
  

<FOR DATABASE_MIRRORING_language_specific_arguments> ::=  
FOR DATABASE_MIRRORING (  
   [ AUTHENTICATION = {   
            WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
   [ [ [ , ] ] ENCRYPTION = { DISABLED | { { SUPPORTED | REQUIRED }   
       [ ALGORITHM { AES | RC4 | AES RC4 | RC4 AES } ] }   
  
    ]   
   [ , ] ROLE = { WITNESS | PARTNER | ALL }  
)  
```  
  
## <a name="arguments"></a>Argumentos  
 *endPointName*  
 É o nome atribuído ao ponto de extremidade que está sendo criado. Use ao atualizar ou excluir o ponto de extremidade.  
  
 AUTHORIZATION *login*  
 Especifica um logon de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Windows válido, ao qual é atribuído a propriedade do objeto de ponto de extremidade recém-criado. Se AUTHORIZATION não for especificado, por padrão, o chamador se tornará proprietário do objeto recém-criado.  
  
 Para atribuir propriedade especificando AUTHORIZATION, o chamador deve ter a permissão IMPERSONATE no *login* especificado.  
  
 Para reatribuir a propriedade, consulte [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
 STATE **=** { STARTED | **STOPPED** | DISABLED }  
 É o estado do ponto de extremidade quando ele é criado. Se o estado não for especificado quando o ponto de extremidade for criado, STOPPED será o padrão.  
  
 STARTED  
 O ponto de extremidade é iniciado e está escutando ativamente as conexões.  
  
 DISABLED  
 O ponto de extremidade está desabilitado. Neste estado, o servidor escuta as solicitações da porta, mas devolve erros aos clientes.  
  
 **STOPPED**  
 O ponto de extremidade está parado. Nesse estado, o servidor não escuta a porta do ponto de extremidade nem responde a qualquer solicitação de tentativa para usar o ponto de extremidade.  
  
 Para alterar o estado, use [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
 AS { TCP }  
 Especifica o protocolo de transporte a ser usado.  
  
 FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING }  
 Especifica o tipo de carga útil.  
  
 No momento, não há nenhum argumento específico de linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)] a ser passado no parâmetro `<language_specific_arguments>`.  
  
 **Opção de protocolo TCP**  
  
 Os argumentos a seguir se aplicam apenas à opção protocolo TCP.  
  
 LISTENER_PORT **=** _listenerPort_  
 Especifica o número da porta de escuta para conexões pelo protocolo TCP/IP service broker. Por convenção, 4022 é usado, mas qualquer número entre 1024 e 32767 é válido.  
  
 LISTENER_IP **=** ALL | **(** _4-part-ip_ **)**  |  **(** "*ip_address_v6*" **)**  
 Especifica o endereço IP de escuta do ponto de extremidade. O padrão é ALL. Isso significa que o ouvinte aceitará uma conexão em qualquer endereço IP válido.  
  
 Se você configurar o espelhamento de banco de dados com um endereço IP, em vez de um nome de domínio totalmente qualificado (`ALTER DATABASE SET PARTNER = partner_IP_address` ou `ALTER DATABASE SET WITNESS = witness_IP_address`), especifique `LISTENER_IP =IP_address`, em vez de `LISTENER_IP=ALL`, ao criar pontos de extremidade de espelhamento.  
  
 **Opções de SERVICE_BROKER e DATABASE_MIRRORING**  
  
 Os argumentos AUTHENTICATION e ENCRYPTION a seguir são comuns às opções SERVICE_BROKER e DATABASE_MIRRORING.  
  
> [!NOTE]  
>  Para opções específicas do SERVICE_BROKER, consulte "Opções SERVICE_BROKER", posteriormente nesta seção. Para opções específicas de DATABASE_MIRRORING, consulte "Opções DATABASE_MIRRORING", posteriormente nesta seção.  
  
 AUTHENTICATION **=** \<authentication_options> Especifica os requisitos de autenticação de TCP/IP para conexões desse ponto de extremidade. O padrão é WINDOWS.  
  
 Os métodos de autenticação com suporte incluem NTLM e ou Kerberos ou ambos.  
  
> [!IMPORTANT]  
>  Todas as conexões de espelhamento em uma instância de servidor usam um único ponto de extremidade de espelhamento de banco de dados. Qualquer tentativa para criar um ponto de extremidade de espelhamento de banco de dados adicional falhará.  
  
 **\<authentication_options> ::=**  
  
 **WINDOWS** [ { NTLM | KERBEROS | **NEGOTIATE** } ]  
 Especifica que o ponto de extremidade deve ser conectado usando o protocolo de Autenticação do Windows para autenticar os pontos de extremidade. Esse é o padrão.  
  
 Se você especificar um método de autorização (NTLM ou KERBEROS), esse método sempre será usado como o protocolo de autenticação. O valor padrão, NEGOTIATE, faz o ponto de extremidade usar o protocolo de negociação Windows para escolher NTLM ou Kerberos.  
  
 CERTIFICATE *certificate_name*  
 Especifica que o ponto de extremidade destina-se a autenticar a conexão usando o certificado especificado por *certificate_name* para estabelecer a identidade para autorização. Os pontos de extremidade distantes devem ter um certificado com a chave pública correspondente à chave privada do certificado especificado.  
  
 WINDOWS [ { NTLM | KERBEROS | **NEGOTIATE** } ] CERTIFICATE *certificate_name*  
 Especifica que ponto de extremidade deve tentar conexão usando a Autenticação do Windows e, se essa tentativa falhar, tentar o certificado especificado.  
  
 CERTIFICATE *certificate_name* WINDOWS [ { NTLM | KERBEROS | **NEGOTIATE** } ]  
 Especifica que ponto de extremidade deve tentar conexão usando certificado especificado e, se essa tentativa falhar, tentar a Autenticação do Windows.  
  
 ENCRYPTION = { DISABLED | SUPPORTED | **REQUIRED** } [ALGORITHM { **AES** | RC4 | AES RC4 | RC4 AES } ]  
 Especifica se a criptografia deve usada no processo. O padrão é REQUIRED.  
  
 DISABLED  
 Especifica que os dados enviados em uma conexão não estão criptografados.  
  
 SUPPORTED  
 Especifica que os dados só serão criptografados se o ponto de extremidade oposto especificar SUPPORTED ou REQUIRED.  
  
 REQUIRED  
 Especifica que conexões para esse ponto de extremidade devem usar criptografia. Portanto, para conexão com esse ponto de extremidade, outros pontos de extremidade deverão ter ENCRYPTION definido como SUPPORTED ou REQUIRED.  
  
 Opcionalmente, você pode usar o argumento ALGORITHM para especificar a forma de criptografia usada pelo ponto de extremidade, como segue:  
  
 **AES**  
 Especifica que o ponto de extremidade deve usar o algoritmo AES. Esse é o padrão no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.  
  
 RC4  
 Especifica que o ponto de extremidade deve usar o algoritmo RC4. Esse é o padrão em todo o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e em versões posteriores, o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
 AES RC4  
 Especifica que o dois pontos de extremidade negociarão por um algoritmo de criptografia com esse ponto de extremidade, dando preferência ao algoritmo AES.  
  
 RC4 AES  
 Especifica que o dois pontos de extremidade negociarão por um algoritmo de criptografia com esse ponto de extremidade, dando preferência ao algoritmo RC4.  
  
> [!NOTE]  
>  O algoritmo RC4 é preterido. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Recomendamos usar AES.  
  
 Se ambos os ponto de extremidade especificarem ambos os algoritmos, mas em ordens diferentes, vence o ponto de extremidade que aceita a conexão.  
  
 **Opções de SERVICE_BROKER**  
  
 Os argumentos a seguir são específicos da opção SERVICE_BROKER.  
  
 MESSAGE_FORWARDING **=** { ENABLED | **DISABLED** }  
 Determina se mensagens recebidas por esse ponto de extremidade que são para serviços localizados em outro lugar serão enviadas.  
  
 ENABLED  
 Encaminha mensagens se um endereço de encaminhamento estiver disponível.  
  
 DISABLED  
 Descarta mensagens para serviços localizados em outro lugar. Esse é o padrão.  
  
 MESSAGE_FORWARD_SIZE **=** _forward_size_  
 Especifica a quantidade máxima de armazenamento em megabytes a ser alocada para ser usada no ponto de extremidade ao armazenar mensagens a serem encaminhadas.  
  
 **Opções de DATABASE_MIRRORING**  
  
 O argumento seguinte é específico da opção DATABASE_MIRRORING.  
  
 ROLE **=** { WITNESS | PARTNER | ALL }  
 Especifica a função ou funções de espelhamento de banco de dados com suporte no ponto de extremidade.  
  
 WITNESS  
 Permite que o ponto de extremidade execute a função de testemunha no processo de espelhamento.  
  
> [!NOTE]  
>  Para [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)], WITNESS é a única opção disponível.  
  
 PARTNER  
 Permite que o ponto de extremidade execute a função de parceiro no processo de espelhamento.  
  
 ALL  
 Permite que o ponto de extremidade execute a função de testemunha e parceiro no processo de espelhamento.  
  
 Para obter mais informações sobre essas funções, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
> [!NOTE]  
>  Não há nenhuma porta padrão para DATABASE_MIRRORING.  
  
## <a name="remarks"></a>Remarks  
 Instruções ENDPOINT DDL não podem ser executadas em uma transação de usuário. Instruções ENDPOINT DDL não falham, mesmo que uma transação ativa de nível de isolamento de instantâneo esteja usando o ponto de extremidade que está sendo alterado.  
  
 Podem ser executadas solicitações em um ENDPOINT pelo seguinte:  
  
-   Membros da função de servidor fixa **sysadmin**  
  
-   O proprietário do ponto de extremidade  
  
-   Usuários ou grupos com permissão CONNECT no ponto de extremidade  
  
## <a name="permissions"></a>Permissões  
 Requer permissão CREATE ENDPOINT ou associação na função de servidor fixa **sysadmin** . Para obter mais informações, consulte [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
## <a name="example"></a>Exemplo  
  
### <a name="creating-a-database-mirroring-endpoint"></a>Criando um ponto de extremidade de espelhamento de banco de dados  
 O exemplo a seguir cria um ponto de extremidade de espelhamento de banco de dados. O ponto de extremidade usa número de porta `7022`, embora nenhum número da porta disponível funcione. O ponto de extremidade é configurado para usar Autenticação do Windows que só usa Kerberos. A opção `ENCRYPTION` é configurada ao valor não padrão de `SUPPORTED` para oferecer suporte a dados criptografados ou não criptografados. O ponto de extremidade está sendo configurado para oferecer suporte às funções de parceiro e testemunha.  
  
```sql  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (  
       AUTHENTICATION = WINDOWS KERBEROS,  
       ENCRYPTION = SUPPORTED,  
       ROLE=ALL);  
GO  
```  

### <a name="create-a-new-endpoint-pointing-to-a-specific-ipv4-address-and-port"></a>Criar um novo ponto de extremidade que aponta para uma porta e um endereço IPv4 específicos

```sql
CREATE ENDPOINT ipv4_endpoint_special
STATE = STARTED
AS TCP (
    LISTENER_PORT = 55555, LISTENER_IP = (10.0.75.1)
)
FOR TSQL ();

GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] TO public; -- Keep existing public permission on default endpoint for demo purpose
GRANT CONNECT ON ENDPOINT::ipv4_endpoint_special
TO login_name;
```

### <a name="create-a-new-endpoint-pointing-to-a-specific-ipv6-address-and-port"></a>Criar um novo ponto de extremidade que aponta para uma porta e um endereço IPv6 específicos

```sql
CREATE ENDPOINT ipv6_endpoint_special
STATE = STARTED
AS TCP (
    LISTENER_PORT = 55555, LISTENER_IP = ('::1')
)
FOR TSQL ();

GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] TO public;
GRANT CONNECT ON ENDPOINT::ipv6_endpoint_special

```
  
## <a name="see-also"></a>Confira também  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [DROP ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

