---
title: Noções básicas do suporte a SSL | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5da6c0f567e86a5d9ba979f01cb82ec382834651
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027301"
---
# <a name="understanding-ssl-support"></a>Noções básicas do suporte a SSL

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Ao estabelecer conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o aplicativo solicitar criptografia e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para dar suporte à criptografia SSL, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] iniciará o handshake SSL. O handshake permite que o servidor e o cliente negociem a criptografia e os algoritmos criptográficos a serem usados para proteger os dados. Após a conclusão do handshake SSL, o cliente e o servidor poderão enviar com segurança os dados criptografados. Durante o handshake SSL, o servidor envia seu certificado de chave pública ao cliente. O emissor de um certificado de chave pública é conhecido como uma Autoridade de Certificação (CA). O cliente é responsável por validar que a autoridade de certificação é de sua confiança.  
  
Se o aplicativo não solicitar criptografia, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não forçará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a oferecer suporte à criptografia SSL. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver configurada para forçar a criptografia SSL, uma conexão será estabelecida sem criptografia. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para forçar a criptografia SSL, o driver habilitará a criptografia SSL automaticamente na execução em JVM (Máquina Virtual Java) configurada adequadamente; caso contrário, a conexão será encerrada e o driver gerará um erro.  
  
> [!NOTE]  
> Verifique se o valor passado para **serverName** corresponde exatamente ao CN (Nome Comum) ou ao nome DNS na rede SAN (Nome Alternativo da Entidade) no certificado do servidor para que uma conexão SSL tenha êxito.  
>
> Para obter mais informações sobre como configurar o SSL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja o tópico Criptografando Conexões para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Remarks

Para permitir que os aplicativos usem a criptografia SSL, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] introduziu as seguintes propriedades de conexão da versão 1.2 em diante: **encrypt**, **trustServerCertificate**, **trustStore**, **trustStorePassword** e **hostNameInCertificate**. Para obter mais informações, veja [Configuração das propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 A tabela a seguir resume o comportamento da versão do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] em possíveis cenários de conexão SSL. Cada cenário usa um conjunto diferente de propriedades de conexão SSL. A tabela inclui:  
  
- **Blank**: "a propriedade não existe na cadeia de conexão"  
  
- **valor**: "a propriedade existe na cadeia de conexão e seu valor é válido"  
  
- **any**: "não importa se a propriedade existe na cadeia de conexão ou seu valor é válido"  
  
> [!NOTE]  
> O mesmo comportamento se aplica à autenticação de usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e à autenticação integrada do Windows.  
  
| encrypt        | trustServerCertificate | hostNameInCertificate | trustStore | trustStorePassword | Comportamento                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------- | ---------------------- | --------------------- | ---------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| false ou em branco | any                    | any                   | any        | any                | O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não forçará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a oferecer suporte à criptografia SSL. Se o servidor tiver um certificado autoassinado, o driver iniciará a troca de certificados SSL. O certificado SSL não será validado e apenas as credenciais (no pacote de logon) são criptografadas.<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL, o driver iniciará a troca de certificados SSL. O certificado SSL não será validado, mas a comunicação inteira será criptografada.                                                                                                                                                                                    |
| true           | true                   | any                   | any        | any                | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL. Observe que, se a propriedade **trustServerCertificate** for definida como "true", o driver não validará o certificado SSL.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                                                                                                                          |
| true           | false ou em branco         | blank                 | blank      | blank              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará a propriedade **serverName** especificada na URL da conexão para validar o certificado SSL do servidor e contará com as regras de procura da fábrica do gerenciador de confiança para determinar qual repositório de certificados deve usar.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                             |
| true           | false ou em branco         | value                 | blank      | blank              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver validará o valor de entidade do certificado SSL usando o valor especificado para a propriedade **hostNameInCertificate**.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                                                                                                 |
| true           | false ou em branco         | blank                 | value      | value              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o valor da propriedade **trustStore** para localizar o arquivo trustStore do certificado e o valor da propriedade **trustStorePassword** para verificar a integridade do arquivo trustStore.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                                                |
| true           | false ou em branco         | blank                 | blank      | value              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o valor da propriedade **trustStorePassword** para verificar a integridade do arquivo trustStore padrão.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                                                                                                                  |
| true           | false ou em branco         | blank                 | value      | blank              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o valor da propriedade **trustStore** para procurar o local do arquivo trustStore.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                                                                                                                                 |
| true           | false ou em branco         | value                 | blank      | value              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o valor da propriedade **trustStorePassword** para verificar a integridade do arquivo trustStore padrão. Além disso, o driver usará o valor da propriedade **hostNameInCertificate** para validar o certificado SSL.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                   |
| true           | false ou em branco         | value                 | value      | blank              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o valor da propriedade **trustStore** para procurar o local do arquivo trustStore. Além disso, o driver usará o valor da propriedade **hostNameInCertificate** para validar o certificado SSL.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.                                                                                  |
| true           | false ou em branco         | value                 | value      | value              | As solicitações [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usam criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o valor da propriedade **trustStore** para localizar o arquivo trustStore do certificado e o valor da propriedade **trustStorePassword** para verificar a integridade do arquivo trustStore. Além disso, o driver usará o valor da propriedade **hostNameInCertificate** para validar o certificado SSL.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão. |
  
Se a propriedade de criptografia for definida como **true**, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usará o provedor de segurança JSSE padrão da JVM para negociar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O provedor de segurança padrão pode não dar suporte a todos os recursos necessários para negociar a criptografia SSL com êxito. Por exemplo, o provedor de segurança padrão pode não ser compatível com o tamanho da chave pública RSA usada no certificado SSL do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nesse caso, o provedor de segurança padrão pode gerar um erro que fará com que o driver JDBC encerre a conexão. Para resolver esse problema, siga um destes procedimentos:  
  
- Configure o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com um certificado do servidor que tenha uma chave pública RSA menor  
  
- Configure a JVM para usar um provedor de segurança JSSE diferente no arquivo de propriedades de segurança "\<java-home>/lib/security/java.security"  
  
- Use uma JVM diferente  
  
## <a name="validating-server-ssl-certificate"></a>Validando o certificado SSL do servidor  

Durante o handshake SSL, o servidor envia seu certificado de chave pública ao cliente. O driver JDBC ou o cliente precisa validar que o certificado do servidor é emitido por uma autoridade de certificação de confiança do cliente. O driver requer que o certificado do servidor atenda às seguintes condições:  
  
- O certificado foi emitido por uma autoridade de certificação confiável.  
  
- O certificado deve ser emitido para autenticação do servidor.  
  
- O certificado não expirou.  
  
- O CN (Nome Comum) na Entidade ou um nome DNS na rede SAN (Nome Alternativo da Entidade) do certificado coincide com o valor **serverName** especificado na cadeia de conexão ou, caso especificado, com o valor da propriedade **hostNameInCertificate**.  
  
- Um nome DNS pode incluir caracteres curinga. Mas o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não oferece suporte à correspondência de caracteres curinga. Ou seja, abc.com não corresponderá a \*.com, mas \*.com corresponderá a \*.com.  
  
## <a name="see-also"></a>Confira também

[Como usar a criptografia SSL](../../connect/jdbc/using-ssl-encryption.md)

[Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)  
