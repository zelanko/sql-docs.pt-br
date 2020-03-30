---
title: Noções básicas sobre suporte à criptografia | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ec3ad142e3dc5e2945afebeb2c9a6c97350672c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "71713305"
---
# <a name="understanding-encryption-support"></a>Noções básicas sobre suporte à criptografia

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Ao estabelecer conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o aplicativo solicitar criptografia e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para dar suporte à criptografia TLS, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] iniciará o handshake TLS. O handshake permite que o servidor e o cliente negociem a criptografia e os algoritmos criptográficos a serem usados para proteger os dados. Após a conclusão do handshake TLS, o cliente e o servidor poderão enviar com segurança os dados criptografados. Durante o handshake TLS, o servidor envia seu certificado de chave pública ao cliente. O emissor de um certificado de chave pública é conhecido como uma Autoridade de Certificação (CA). O cliente é responsável por validar que a autoridade de certificação é de sua confiança.  
  
Se o aplicativo não solicitar criptografia, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não forçará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a oferecer suporte à criptografia TLS. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver configurada para forçar a criptografia TLS, uma conexão será estabelecida sem criptografia. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para forçar a criptografia TLS, o driver habilitará a criptografia TLS automaticamente na execução em JVM (Máquina Virtual Java) configurada adequadamente; caso contrário, a conexão será encerrada e o driver gerará um erro.  
  
> [!NOTE]  
> Verifique se o valor passado para **serverName** corresponde exatamente ao CN (Nome Comum) ou ao nome DNS na rede SAN (Nome Alternativo da Entidade) no certificado do servidor para que uma conexão TLS tenha êxito.  
>
> Para obter mais informações sobre como configurar o TLS para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira [Habilitar conexões criptografadas no Mecanismo de Banco de Dados](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="remarks"></a>Comentários

Para permitir que os aplicativos usem a criptografia TLS, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] introduziu as seguintes propriedades de conexão da versão 1.2 em diante: **encrypt**, **trustServerCertificate**, **trustStore**, **trustStorePassword** e **hostNameInCertificate**. Para obter mais informações, veja [Configuração das propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 A tabela a seguir resume o comportamento da versão do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] em possíveis cenários de conexão TLS. Cada cenário usa um conjunto diferente de propriedades de conexão TLS. A tabela inclui:  
  
- **blank**: "A propriedade não existe na cadeia de conexão"  
  
- **value**: "A propriedade existe na cadeia de conexão e o valor dela é válido"  
  
- **any**: "Não importa se a propriedade existe na cadeia de conexão nem se o valor dela é válido"  
  
> [!NOTE]  
> O mesmo comportamento se aplica à autenticação de usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e à autenticação integrada do Windows.  
  
| encrypt        | trustServerCertificate | hostNameInCertificate | trustStore | trustStorePassword | Comportamento                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------- | ---------------------- | --------------------- | ---------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| false ou em branco | any                    | any                   | any        | any                | O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não forçará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a oferecer suporte à criptografia TLS. Se o servidor tiver um certificado autoassinado, o driver iniciará a troca de certificados TLS. O certificado TLS não será validado e apenas as credenciais (no pacote de logon) são criptografadas.<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia TLS, o driver iniciará a troca de certificado TLS. O certificado TLS não será validado, mas a comunicação inteira será criptografada.                                                                                                                                                                                    |
| true           | true                   | any                   | any        | any                | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia TLS com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia TLS ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificado TLS. Observe que, se a propriedade **trustServerCertificate** for definida como "true", o driver não validará o certificado TLS.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                                                                                                                          |
| true           | false ou em branco         | blank                 | blank      | blank              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia TLS com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia TLS ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificado TLS.<br /><br /> O driver usará a propriedade **serverName** especificada na URL da conexão para validar o certificado TLS do servidor e contará com as regras de procura da fábrica do gerenciador de confiança para determinar qual repositório de certificados deve usar.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                             |
| true           | false ou em branco         | value                 | blank      | blank              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia TLS com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia TLS ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificado TLS.<br /><br /> O driver validará o valor de entidade do certificado TLS usando o valor especificado para a propriedade **hostNameInCertificate**.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                                                                                                 |
| true           | false ou em branco         | blank                 | value      | value              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia TLS com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia TLS ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificado TLS.<br /><br /> O driver usará o valor da propriedade **trustStore** para localizar o arquivo trustStore do certificado e o valor da propriedade **trustStorePassword** para verificar a integridade do arquivo trustStore.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                                                |
| true           | false ou em branco         | blank                 | blank      | value              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia TLS com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia TLS ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificado TLS.<br /><br /> O driver usará o valor da propriedade **trustStorePassword** para verificar a integridade do arquivo trustStore padrão.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                                                                                                                  |
| true           | false ou em branco         | blank                 | value      | blank              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia TLS com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia TLS ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificado TLS.<br /><br /> O driver usará o valor da propriedade **trustStore** para procurar o local do arquivo trustStore.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                                                                                                                                 |
| true           | false ou em branco         | value                 | blank      | value              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia TLS com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia TLS ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificado TLS.<br /><br /> O driver usará o valor da propriedade **trustStorePassword** para verificar a integridade do arquivo trustStore padrão. Além disso, o driver usará o valor da propriedade **hostNameInCertificate** para validar o certificado TLS.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                   |
| true           | false ou em branco         | value                 | value      | blank              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia TLS com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia TLS ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificado TLS.<br /><br /> O driver usará o valor da propriedade **trustStore** para procurar o local do arquivo trustStore. Além disso, o driver usará o valor da propriedade **hostNameInCertificate** para validar o certificado TLS.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                  |
| true           | false ou em branco         | value                 | value      | value              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia TLS com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia TLS ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificado TLS.<br /><br /> O driver usará o valor da propriedade **trustStore** para localizar o arquivo trustStore do certificado e o valor da propriedade **trustStorePassword** para verificar a integridade do arquivo trustStore. Além disso, o driver usará o valor da propriedade **hostNameInCertificate** para validar o certificado TLS.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão. |
  
Se a propriedade de criptografia for definida como **true**, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usará o provedor de segurança JSSE padrão da JVM para negociar a criptografia TLS com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O provedor de segurança padrão pode não dar suporte a todos os recursos necessários para negociar a criptografia TLS com êxito. Por exemplo, o provedor de segurança padrão pode não ser compatível com o tamanho da chave pública RSA usada no certificado TLS do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nesse caso, o provedor de segurança padrão pode gerar um erro que fará com que o driver JDBC encerre a conexão. Para resolver esse problema, siga um destes procedimentos:  
  
- Configure o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com um certificado do servidor que tenha uma chave pública RSA menor  
  
- Configure a JVM para usar um provedor de segurança JSSE diferente no arquivo de propriedades de segurança "\<java-home>/lib/security/java.security"  
  
- Use uma JVM diferente  
  
## <a name="validating-server-tls-certificate"></a>Como validar o certificado TLS do servidor  

Durante o handshake TLS, o servidor envia seu certificado de chave pública ao cliente. O driver JDBC ou o cliente precisa validar que o certificado do servidor é emitido por uma autoridade de certificação de confiança do cliente. O driver requer que o certificado do servidor atenda às seguintes condições:  
  
- O certificado foi emitido por uma autoridade de certificação confiável.  
  
- O certificado deve ser emitido para autenticação do servidor.  
  
- O certificado não expirou.  
  
- O CN (Nome Comum) na Entidade ou um nome DNS na rede SAN (Nome Alternativo da Entidade) do certificado coincide com o valor **serverName** especificado na cadeia de conexão ou, caso especificado, com o valor da propriedade **hostNameInCertificate**.  
  
- Um nome DNS pode incluir caracteres curinga. Mas o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não oferece suporte à correspondência de caracteres curinga. Ou seja, abc.com não corresponderá a \*.com, mas \*.com corresponderá a \*.com.  
  
## <a name="see-also"></a>Confira também

[Usando criptografia](../../connect/jdbc/using-ssl-encryption.md)

[Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)  
