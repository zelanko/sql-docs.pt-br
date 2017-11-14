---
title: "Noções básicas sobre o suporte a SSL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 82440c6d3ffe0ee0f2c2b9080328c0fed302cb31
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-ssl-support"></a>Compreendendo o suporte a SSL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], se o aplicativo solicitar criptografia e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurado para dar suporte à criptografia SSL, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] iniciará o handshake SSL. O handshake permite que o servidor e o cliente negociem a criptografia e os algoritmos criptográficos a serem usados para proteger os dados. Após a conclusão do handshake SSL, o cliente e o servidor poderão enviar com segurança os dados criptografados. Durante o handshake SSL, o servidor envia seu certificado de chave pública para o cliente. O emissor de um certificado de chave pública é conhecido como uma Autoridade de Certificação (CA). O cliente é responsável por validar que a autoridade de certificação é de sua confiança.  
  
 Se o aplicativo não solicitar criptografia, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não forçará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para oferecer suporte à criptografia SSL. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instância não está configurada para forçar a criptografia SSL, uma conexão será estabelecida sem criptografia. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instância está configurada para forçar a criptografia SSL, o driver habilitará a criptografia SSL automaticamente ao executar em Java Virtual Machine (JVM) configurada adequadamente, ou caso contrário a conexão será encerrada e o driver irá gerar um erro.  
  
> [!NOTE]  
>  Verifique se o valor passado para **serverName** corresponda exatamente ao nome DNS ou CN (nome comum) de entidade alternativo SAN (nome) no certificado do servidor para uma conexão SSL tenha êxito.  
  
> [!NOTE]  
>  Para obter mais informações sobre como configurar o SSL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte Criptografando conexões com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tópico [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="remarks"></a>Comentários  
 Para permitir que aplicativos usar a criptografia SSL, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] introduziu as seguintes propriedades de conexão a partir da versão 1.2: **criptografar**, **trustServerCertificate**, **trustStore**, **trustStorePassword**, e **hostNameInCertificate**. Para obter mais informações, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 A tabela a seguir resume como o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] versão comporta-se para possíveis cenários de conexão SSL. Cada cenário usa um conjunto diferente de propriedades de conexão SSL. A tabela inclui:  
  
-   **em branco**: "a propriedade não existe na cadeia de conexão"  
  
-   **valor**: "a propriedade existe na cadeia de conexão e seu valor é válido"  
  
-   **qualquer**: "Não importa se a propriedade existe na cadeia de conexão ou seu valor é válido"  
  
> [!NOTE]  
>  O mesmo comportamento se aplica para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticação integrada do Windows e autenticação de usuário.  
  
|encrypt|trustServerCertificate|hostNameInCertificate|trustStore|trustStorePassword|Comportamento|  
|-------------|----------------------------|---------------------------|----------------|------------------------|--------------|  
|false ou em branco|any|any|any|any|O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não forçará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para oferecer suporte à criptografia SSL. Se o servidor tiver um certificado autoassinado, o driver iniciará a troca de certificados SSL. O certificado SSL não será validado e apenas as credenciais (no pacote de logon) são criptografadas.<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL, o driver iniciará a troca de certificados SSL. O certificado SSL não será validado, mas a comunicação inteira será criptografada.|  
|true|true|any|any|any|O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitações para usar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL. Observe que, se o **trustServerCertificate** propriedade é definida como "true", o driver não validará o certificado SSL.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.|  
|true|false ou em branco|blank|blank|blank|O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitações para usar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o **serverName** propriedade especificada na URL de conexão para validar o certificado SSL do servidor e contam com regras de procura da fábrica do Gerenciador de confiança para determinar qual repositório de certificados usar.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.|  
|true|false ou em branco|value|blank|blank|O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitações para usar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver validará o valor da entidade do certificado SSL usando o valor especificado para o **hostNameInCertificate** propriedade.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.|  
|true|false ou em branco|blank|value|value|O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitações para usar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o **trustStore** valor da propriedade para localizar o arquivo trustStore do certificado e **trustStorePassword** valor da propriedade para verificar a integridade do arquivo trustStore.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.|  
|true|false ou em branco|blank|blank|value|O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitações para usar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o **trustStorePassword** valor da propriedade para verificar a integridade do arquivo trustStore padrão.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.|  
|true|false ou em branco|blank|value|blank|O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitações para usar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o **trustStore** valor da propriedade para procurar o local do arquivo trustStore.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.|  
|true|false ou em branco|value|blank|value|O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitações para usar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o **trustStorePassword** valor da propriedade para verificar a integridade do arquivo trustStore padrão. Além disso, o driver usará o **hostNameInCertificate** valor da propriedade para validar o certificado SSL.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.|  
|true|false ou em branco|value|value|blank|O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitações para usar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o **trustStore** valor da propriedade para procurar o local do arquivo trustStore. Além disso, o driver usará o **hostNameInCertificate** valor da propriedade para validar o certificado SSL.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.|  
|true|false ou em branco|value|value|value|O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solicitações para usar a criptografia SSL com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br /> Se o servidor exigir que o cliente dê suporte à criptografia SSL ou se o servidor der suporte à criptografia, o driver iniciará a troca de certificados SSL.<br /><br /> O driver usará o **trustStore** valor da propriedade para localizar o arquivo trustStore do certificado e **trustStorePassword** valor da propriedade para verificar a integridade do arquivo trustStore. Além disso, o driver usará o **hostNameInCertificate** valor da propriedade para validar o certificado SSL.<br /><br /> Se o servidor não estiver configurado para dar suporte à criptografia, o driver irá gerar um erro e encerrará a conexão.|  
  
 Se a propriedade de criptografia é definida como **true**, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa o provedor de segurança JSSE de padrão da JVM para negociar a criptografia SSL com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. O provedor de segurança padrão pode não dar suporte a todos os recursos necessários para negociar a criptografia SSL com êxito. Por exemplo, o provedor de segurança padrão pode não suportar o tamanho da chave pública RSA usada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] certificado SSL. Nesse caso, o provedor de segurança padrão pode gerar um erro que fará com que o driver JDBC encerre a conexão. Para resolver esse problema, siga um destes procedimentos:  
  
-   Configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] com um certificado de servidor que tenha uma chave pública RSA menor  
  
-   Configure a JVM para usar um provedor de segurança JSSE diferente no "\<java-home > / lib/security/java.security" arquivo de propriedades de segurança  
  
-   Use uma JVM diferente  
  
## <a name="validating-server-ssl-certificate"></a>Validando o certificado SSL do servidor  
 Durante o handshake SSL, o servidor envia seu certificado de chave pública para o cliente. O driver JDBC ou o cliente precisa validar que o certificado do servidor é emitido por uma autoridade de certificação de confiança do cliente. O driver requer que o certificado do servidor atenda às seguintes condições:  
  
-   O certificado foi emitido por uma autoridade de certificação confiável.  
  
-   O certificado deve ser emitido para autenticação do servidor.  
  
-   O certificado não expirou.  
  
-   O nome comum (CN) no assunto ou um nome DNS no assunto alternativo SAN (nome) do certificado corresponde exatamente a **serverName** valor especificado na cadeia de conexão ou, se especificado, o  **hostNameInCertificate** o valor da propriedade.  
  
-   Um nome DNS pode incluir caracteres curinga. Mas o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não oferece suporte a correspondência de curingas. Ou seja, abc.com não corresponderá a *.com, mas \*.com corresponderá \*. com.  
  
## <a name="see-also"></a>Consulte também  
 [Usando a criptografia SSL](../../connect/jdbc/using-ssl-encryption.md)   
 [Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  

