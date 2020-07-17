---
title: Solucionar problemas de conectividade do PolyBase Kerberos | Microsoft Docs
description: Para solucionar problemas de autenticação do PolyBase com um cluster Hadoop protegido por Kerberos, você pode usar o diagnóstico interativo interno do PolyBase.
author: alazad-msft
ms.author: alazad
ms.reviewer: mikeray
ms.technology: polybase
ms.devlang: ''
ms.topic: conceptual
ms.date: 10/02/2019
ms.prod: sql
ms.prod_service: polybase, sql-data-warehouse, pdw
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 9e50701d0486ee7bc00bf765d2a71cb4de0c0b25
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196164"
---
# <a name="troubleshoot-polybase-kerberos-connectivity"></a>Solucionar problemas de conectividade do PolyBase Kerberos

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Você pode usar o diagnóstico interativo, interno no PolyBase, para ajudar a solucionar problemas de autenticação no uso do PolyBase em um cluster Hadoop protegido por Kerberos. 

Este artigo descreve o processo de depuração desses problemas por dessa ferramenta interna de diagnóstico.

> [!TIP]
> Em vez de seguir as etapas neste guia, você pode optar por executar o [Testador Kerberos do HDFS](https://github.com/microsoft/sql-server-samples/tree/master/samples/manage/hdfs-kerberos-tester) para solucionar problemas de conexões Kerberos do HDFS para o PolyBase, quando enfrentar uma falha de Kerberos do HDFS ao criar uma tabela externa em um cluster HDFS protegido pelo Kerberos.
> Essa ferramenta ajudará a resolver problemas não relativos ao SQL Server, para ajudá-lo a se concentrar na resolução de problemas de configuração de Kerberos do HDFS, principalmente identificando problemas com configurações incorretas de nome de usuário/senha e configurações incorretas de instalação de Kerberos em clusters.      
> Essa ferramenta é completamente independente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ela está disponível como um Jupyter Notebook e requer o Azure Data Studio.

## <a name="prerequisites"></a>Pré-requisitos

1. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM CU6/[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU3/[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ou superior com o PolyBase instalado
1. Um cluster Hadoop (Cloudera ou Hortonworks) protegido por Kerberos (Active Directory ou MIT)

## <a name="introduction"></a>Introdução
Primeiramente, é necessário entender o protocolo Kerberos em um alto nível. Há três atores envolvidos:

1. O cliente Kerberos (SQL Server)
1. O recurso protegido (HDFS, MR2, YARN, histórico de trabalhos etc.)
1. Centro de distribuição de chaves (conhecido como um controlador de domínio no Active Directory)

Cada recurso protegido do Hadoop é registrado no **KDC (Centro de Distribuição de Chaves)** com um único **SPN (Nome da Entidade de Serviço)** quando o Kerberos é configurado no cluster Hadoop. A meta é que o cliente obtenha um tíquete de usuário temporário, chamado **Tíquete de Concessão de Tíquete (TGT)** , para solicitar outro tíquete temporário, chamado **Tíquete de Serviço (ST)** ao KDC no SPN específico que se deseja acessar.  

No PolyBase, quando uma autenticação é solicitada em qualquer recurso protegido por Kerberos, o handshake com quatro viagens de ida e volta a seguir ocorre:

1. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta ao KDC e obtém um TGT para o usuário. O TGT é criptografado usando a chave privada do KDC.
1. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chama o recurso protegido do Hadoop, HDFS e determina qual SPN necessita de um ST.
1. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] volta para o KDC, passa o TGT novamente e solicita um ST para acessar o recurso protegido específico. O ST é criptografado usando a chave privada protegida do serviço.
1. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encaminha o ST para o Hadoop e é autenticado para criar uma sessão nesse serviço.

![SQL Server do PolyBase](./media/polybase-sqlserver.png)

Problemas com a autenticação se encaixam em uma ou mais das quatro etapas acima. Para acelerar a depuração, o PolyBase introduziu uma ferramenta de diagnóstico integrada para ajudar a identificar o ponto de falha.

## <a name="troubleshooting"></a>Solução de problemas

O PolyBase tem os seguintes arquivos XML de configuração contendo as propriedades do cluster Hadoop:

- core-site.xml
- hdfs-site.xml
- hive-site.xml
- jaas.conf
- mapred-site.xml
- yarn-site.xml

Esses arquivos estão localizados em:

`\[System Drive\]:{install path}\{instance}\{name}\MSSQL\Binn\PolyBase\Hadoop\conf`

Por exemplo, o padrão para o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] é `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\PolyBase\Hadoop\conf`.

Atualize **core-site.xml** e adicione as três propriedades abaixo. Defina os valores de acordo com o ambiente:

```xml
<property>
    <name>polybase.kerberos.realm</name>
    <value>CONTOSO.COM</value>
</property>
<property>
    <name>polybase.kerberos.kdchost</name>
    <value>kerberos.contoso.com</value>
</property>
<property>
    <name>hadoop.security.authentication</name>
    <value>KERBEROS</value>
</property>
```
> [!NOTE]
> O valor da propriedade `polybase.kerberos.realm` precisa estar todo em letras maiúsculas.

Posteriormente, será necessário atualizar os outros XMLs se você quiser realizar operações de aplicação. No entanto, apenas com a configuração desse arquivo, pelo menos o sistema de arquivos HDFS poderá ser acessado.

A ferramenta é executada independentemente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], portanto, ela não precisará estar em execução ou ser reiniciada se as XMLs de configuração forem atualizadas. Para executar a ferramenta, execute os comandos a seguir no host com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado:

```cmd
> cd C:\Program Files\Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\Binn\PolyBase  
> java -classpath ".\Hadoop\conf;.\Hadoop\*;.\Hadoop\HDP2_2\*" com.microsoft.polybase.client.HdfsBridge {Name Node Address} {Name Node Port} {Service Principal} {Filepath containing Service Principal's Password} {Remote HDFS file path (optional)}
```

## <a name="arguments"></a>Argumentos

| Argumento | Descrição|
| --- | --- |
| *Endereço do nó de nome* | O IP ou FQDN do nó de nome. Refere-se ao argumento "LOCATION" em seu CREATE EXTERNAL DATA SOURCE T-SQL.|
| *Porta do nó de nome* | A porta do nó de nome. Refere-se ao argumento "LOCATION" em seu CREATE EXTERNAL DATA SOURCE T-SQL. Por exemplo, 8020. |
| *Entidade de Serviço* | A entidade de serviço do administrador para o KDC. Corresponde ao argumento "IDENTITY" no seu `CREATE DATABASE SCOPED CREDENTIAL` T-SQL.|
| *Senha do serviço* | Em vez de digitar a senha no console, armazene-a em um arquivo e passe o caminho do arquivo aqui. O conteúdo do arquivo deve corresponder ao usado como seu argumento "SECRET" no seu `CREATE DATABASE SCOPED CREDENTIAL` T-SQL. |
| *Caminho do arquivo HDFS remoto (opcional)* | O caminho de um arquivo existente a ser acessado. Se não estiver especificado, a raiz "/" será usada. |

## <a name="example"></a>Exemplo

```cmd
java -classpath ".\Hadoop\conf;.\Hadoop\*;.\Hadoop\HDP2_2\*" com.microsoft.polybase.client.HdfsBridge 10.193.27.232 8020 admin_user C:\temp\kerberos_pass.txt
```

A saída é detalhada para depuração avançada, mas há apenas quatro pontos de verificação principais para procurar, independentemente de você estar usando o MIT ou o AD. Eles correspondem às quatro etapas descritas acima. 

Os seguintes trechos são de um MIT KDC. É possível consultar saídas de exemplo do MIT e do AD no final deste artigo, nas Referências.

## <a name="checkpoint-1"></a>Ponto de verificação 1
Deve haver um despejo hexadecimal de um tíquete com `Server Principal = krbtgt/MYREALM.COM@MYREALM.COM`. Isso indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi autenticado com êxito no KDC e recebeu um TGT. Caso contrário, o problema está estritamente entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o KDC, e não no Hadoop.

O PolyBase **não** oferece suporte a relações de confiança entre o AD e o MIT e deve ser configurado no mesmo KDC configurado no cluster Hadoop. Nesses ambientes, criar uma conta de serviço manualmente no KDC em questão e usá-la para executar a autenticação funcionará.

```cmd
|>>> KrbAsReq creating message 
 >>> KrbKdcReq send: kdc=kerberos.contoso.com UDP:88, timeout=30000, number of retries =3, #bytes=143 
 >>> KDCCommunication: kdc=kerberos.contoso.com UDP:88, timeout=30000,Attempt =1, #bytes=143 
 >>> KrbKdcReq send: #bytes read=646 
 >>> KdcAccessibility: remove kerberos.contoso.com 
 >>> EType: sun.security.krb5.internal.crypto.Des3CbcHmacSha1KdEType 
 >>> KrbAsRep cons in KrbAsReq.getReply myuser 
 [2017-04-25 21:34:33,548] INFO 687[main] - com.microsoft.polybase.client.KerberosSecureLogin.secureLogin(KerberosSecureLogin.java:97) - Subject: 
 Principal: admin_user@CONTOSO.COM 
 Private Credential: Ticket (hex) = 
 0000: 61 82 01 48 30 82 01 44 A0 03 02 01 05 A1 0E 1B a..H0..D........ 
 0010: 0C 41 50 53 48 44 50 4D 53 2E 43 4F 4D A2 21 30 .CONTOSO.COM.!0 
 0020: 1F A0 03 02 01 02 A1 18 30 16 1B 06 6B 72 62 74 ........0...krbt 
 0030: 67 74 1B 0C 41 50 53 48 44 50 4D 53 2E 43 4F 4D gt..CONTOSO.COM 
 0040: A3 82 01 08 30 82 01 04 A0 03 02 01 10 A1 03 02 ....0........... 
 *[...Condensed...]* 
 0140: 67 6D F6 41 6C EB E0 C3 3A B2 BD B1 gm.Al...:... 
 Client Principal = admin_user@CONTOSO.COM 
 Server Principal = krbtgt/CONTOSO.COM@CONTOSO.COM 
 *[...Condensed...]* 
 [2017-04-25 21:34:34,500] INFO 1639[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1579) - Successfully authenticated against KDC server. 
```

## <a name="checkpoint-2"></a>Ponto de verificação 2
O PolyBase tentará acessar o HDFS e falhará, pois a solicitação não continha o Tíquete de Serviço necessário.

```cmd
 [2017-04-25 21:34:34,501] INFO 1640[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1584) - Attempting to access external filesystem at URI: hdfs://10.193.27.232:8020 
 Found ticket for admin_user@CONTOSO.COM to go to krbtgt/CONTOSO.COM@CONTOSO.COM expiring on Wed Apr 26 21:34:33 UTC 2017 
 Entered Krb5Context.initSecContext with state=STATE_NEW 
 Found ticket for admin_user@CONTOSO.COM to go to krbtgt/CONTOSO.COM@CONTOSO.COM expiring on Wed Apr 26 21:34:33 UTC 2017 
 Service ticket not found in the subject 
```

## <a name="checkpoint-3"></a>Ponto de verificação 3
Um segundo despejo hexadecimal indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizou o TGT com êxito e adquiriu o tíquete de serviço aplicável para o SPN do nó do nome do KDC.

```cmd
 >>> KrbKdcReq send: kdc=kerberos.contoso.com UDP:88, timeout=30000, number of retries =3, #bytes=664 
 >>> KDCCommunication: kdc=kerberos.contoso.com UDP:88, timeout=30000,Attempt =1, #bytes=664 
 >>> KrbKdcReq send: #bytes read=669 
 >>> KdcAccessibility: remove kerberos.contoso.com 
 >>> EType: sun.security.krb5.internal.crypto.Des3CbcHmacSha1KdEType 
 >>> KrbApReq: APOptions are 00100000 00000000 00000000 00000000 
 >>> EType: sun.security.krb5.internal.crypto.Des3CbcHmacSha1KdEType 
 Krb5Context setting mySeqNumber to: 1033039363 
 Created InitSecContextToken: 
 0000: 01 00 6E 82 02 4B 30 82 02 47 A0 03 02 01 05 A1 ..n..K0..G...... 
 0010: 03 02 01 0E A2 07 03 05 00 20 00 00 00 A3 82 01 ......... ...... 
 0020: 63 61 82 01 5F 30 82 01 5B A0 03 02 01 05 A1 0E ca.._0..[....... 
 0030: 1B 0C 41 50 53 48 44 50 4D 53 2E 43 4F 4D A2 26 ..CONTOSO.COM.& 
 0040: 30 24 A0 03 02 01 00 A1 1D 30 1B 1B 02 6E 6E 1B 0$.......0...nn. 
 0050: 15 73 68 61 73 74 61 2D 68 64 70 32 35 2D 30 30 .hadoop-hdp25-00 
 0060: 2E 6C 6F 63 61 6C A3 82 01 1A 30 82 01 16 A0 03 .local....0..... 
 0070: 02 01 10 A1 03 02 01 01 A2 82 01 08 04 82 01 04 ................ 
 *[...Condensed...]* 
 0240: 03 E3 68 72 C4 D2 8D C2 8A 63 52 1F AE 26 B6 88 ..hr.....cR..&.. 
 0250: C4 . 
```

## <a name="checkpoint-4"></a>Ponto de verificação 4
Por fim, as propriedades de arquivo do caminho de destino devem ser impressas junto com uma mensagem de confirmação. As propriedades do arquivo confirmam que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi autenticado pelo Hadoop usando o ST e uma sessão foi concedida para acessar o recurso protegido.

Ao atingir esse ponto, confirma-se que: (i) os três atores são capazes de se comunicar corretamente, (ii) o core-site.xml e o jaas.conf estão corretos e (iii) o KDC reconheceu as credenciais.

```cmd
 [2017-04-25 21:34:35,096] INFO 2235[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1586) - File properties for "/": FileStatus{path=hdfs://10.193.27.232:8020/; isDirectory=true; modification_time=1492028259862; access_time=0; owner=hdfs; group=hdfs; permission=rwxr-xr-x; isSymlink=false} 
 [2017-04-25 21:34:35,098] INFO 2237[main] - com.microsoft.polybase.client.HdfsBridge.main(HdfsBridge.java:1587) - Successfully accessed the external file system. 
```

## <a name="common-errors"></a>Erros comuns
Se a ferramenta foi executada e as propriedades de arquivo do caminho de destino *não* foram impressas (Ponto de verificação 4), deve haver uma exceção no centro. Examine-a e considere o contexto do fluxo de quatro etapas em que ela ocorreu. Considere os seguintes problemas comuns que podem ter ocorrido, em ordem:

| Exceção e mensagens | Causa | 
| --- | --- |
| org.apache.hadoop.security.AccessControlException<br>A autenticação SIMPLES não está habilitada. Disponível:[TOKEN, KERBEROS] | O core-site.xml não tem a propriedade hadoop.security.authentication definida como "KERBEROS".|
|javax.security.auth.login.LoginException<br>Cliente não encontrado no banco de dados do Kerberos (6) – CLIENT_NOT_FOUND |    O administrador de Entidade de Serviço fornecido não existe no realm especificado em core-site.xml.|
| javax.security.auth.login.LoginException<br> Houve uma falha na soma de verificação |O administrador de Entidade de Serviço existe, mas a senha está incorreta. |
| Nome da configuração nativa: C:\Windows\krb5.ini<br>Carregado da configuração nativa | Esta mensagem indica que o krb5LoginModule do Java detectou configurações personalizadas do cliente em seu computador. Verifique as configurações de cliente personalizadas que podem estar causando o problema. |
| javax.security.auth.login.LoginException<br>java.lang.IllegalArgumentException<br>Nome da entidade de segurança ilícita admin_user@CONTOSO.COM: org.apache.hadoop.security.authentication.util.KerberosName$NoMatchingRule: não há regras aplicadas para admin_user@CONTOSO.COM | Adicione a propriedade “hadoop.security.auth_to_local” ao core-site.xml com as regras apropriadas por cluster Hadoop. |
| java.net.ConnectException<br>A tentativa de acessar o sistema de arquivos externo no URI: hdfs://10.193.27.230:8020<br>Houve uma falha na chamada de IAAS16981207/10.107.0.245 to 10.193.27.230:8020 na exceção de conexão | A autenticação do KDC foi bem-sucedida, mas não conseguiu acessar o nó de nome do Hadoop. Verifique o IP e a porta do nó de nome. Verifique se que o firewall está desabilitado no Hadoop. |
| java.io.FileNotFoundException<br>O arquivo não existe: /test/data.csv |    A autenticação foi bem-sucedida, mas o local especificado não existe. Verifique o caminho ou teste com a raiz "/" primeiro. |

## <a name="debugging-tips"></a>Dicas de depuração

### <a name="mit-kdc"></a>MIT KDC  
Todos os SPNs registrados com o KDC, incluindo os administradores, podem ser exibidos por meio da execução de **kadmin.local** > (logon do administrador) > **listprincs** no host do KDC ou em qualquer cliente do KDC. Se o Kerberos está configurado corretamente no cluster do Hadoop, deve haver um SPN para cada um dos serviços disponíveis no cluster (por exemplo: `nn`, `dn`, `rm`, `yarn`, `spnego` etc.) Os arquivos keytab correspondentes (substitutos para senhas) podem ser vistos em **/etc/security/keytabs**, por padrão. Eles são criptografados usando a chave privada do KDC.  

Também considere usar a ferramenta [`kinit`](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html) para verificar as credenciais de administrador no KDC localmente. Um exemplo de uso seria: `kinit identity@MYREALM.COM`. Um prompt de senha indica que a identidade existe.  
Os logs do KDC estão disponíveis em **/var/log/krb5kdc.log** por padrão, que inclui todas as solicitações de tíquetes, bem como o IP do cliente que fez a solicitação. Deve haver duas solicitações de IP do computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual a ferramenta foi executada: primeiro para o TGT do Servidor de Autenticação, como **AS\_REQ**, seguido por um **TGS\_REQ** para o ST do Servidor de Concessão de Tíquetes.

```bash
 [root@MY-KDC log]# tail -2 /var/log/krb5kdc.log 
 May 09 09:48:26 MY-KDC.local krb5kdc[2547](info): **AS_REQ** (3 etypes {17 16 23}) 10.107.0.245: ISSUE: authtime 1494348506, etypes {rep=16 tkt=16 ses=16}, admin_user@CONTOSO.COM for **krbtgt/CONTOSO.COM@CONTOSO.COM** 
 May 09 09:48:29 MY-KDC.local krb5kdc[2547](info): **TGS_REQ** (3 etypes {17 16 23}) 10.107.0.245: ISSUE: authtime 1494348506, etypes {rep=16 tkt=16 ses=16}, admin_user@CONTOSO.COM for **nn/hadoop-hdp25-00.local@CONTOSO.COM** 
```

### <a name="active-directory"></a>Active Directory 
No Active Directory, os SPNs podem ser exibidos por meio do Painel de Controle > Usuários e Computadores do Active Directory > *MyRealm* > *MyOrganizationalUnit*. Se o Kerberos está configurado corretamente no cluster do Hadoop, há um SPN para cada um dos serviços disponíveis (por exemplo: `nn`, `dn`, `rm`, `yarn`, `spnego` etc.)

### <a name="general-debugging-tips"></a>Dicas gerais de depuração
É útil ter alguma experiência em Java para examinar os logs e depurar os problemas de Kerberos, que são independentes do recurso PolyBase do SQL server.

Se você ainda estiver com problemas para acessar o Kerberos, siga as etapas abaixo para depurar:

1. Verifique se você consegue acessar os dados do HDFS Kerberos de fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode: 

    - Escrever seu próprio programa Java ou
    - Use a classe `HdfsBridge` da pasta de instalação do PolyBase. Por exemplo:

      ```java
      -classpath ".\Hadoop\conf;.\Hadoop\*;.\Hadoop\HDP2_2\*" com.microsoft.polybase.client.HdfsBridge 10.193.27.232 8020 admin_user C:\temp\kerberos_pass.txt
      ```

     No exemplo acima, `admin_user` inclui apenas o nome de usuário, não qualquer parte do domínio.

2. Se você não consegue acessar dados do HDFS do Kerberos de fora do PolyBase:
    - Há dois tipos de autenticação Kerberos: A autenticação Kerberos do Active Directory e a autenticação do MIT Kerberos.
    - Verifique se o usuário existe na conta de domínio e use a mesma conta de usuário ao tentar acessar o HDFS.

3. Para o Active Directory Kerberos, verifique se você pode ver um tíquete em cache usando o comando `klist` no Windows.
    - Entre no computador do PolyBase e execute `klist` e `klist tgt` no prompt de comando para ver se os tipos de criptografia, o nome de usuário e o KDC estão corretos.

4. Se o KDC tiver suporte apenas para AES256, verifique se [arquivos de política JCE](http://www.oracle.com/technetwork/java/javase/downloads/index.html) estão instalados.

## <a name="see-also"></a>Confira também
[Integrar o PolyBase com o Cloudera usando a Autenticação do Active Directory](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/10/17/integrating-polybase-with-cloudera-using-active-directory-authentication)  
[Guia do Cloudera para a configuração do Kerberos para CDH](https://www.cloudera.com/documentation/enterprise/5-6-x/topics/cm_sg_principal_keytab.html)  
[Guia do Hortonworks para a configuração do Kerberos para HDP](https://docs.hortonworks.com/HDPDocuments/Ambari-2.2.0.0/bk_Ambari_Security_Guide/content/ch_configuring_amb_hdp_for_kerberos.html)  
[Solucionando problemas do PolyBase](polybase-troubleshooting.md)
