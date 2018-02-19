---
title: "Compreendendo transações XA | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6599312aa6c25275e6b7a642c6764591d1bf4cba
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="understanding-xa-transactions"></a>Compreendendo transações XA
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece suporte para as transações distribuídas opcionais da plataforma Java, Enterprise Edition/JDBC 2.0. As conexões JDBC obtidas através da classe [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) podem participar de ambientes de processamento de transações distribuídas padrão, como servidores de aplicativo da plataforma Java, Enterprise Edition (Java EE).  
  
> [!WARNING]  
>  O Microsoft JDBC Driver 4.2 (e posterior) para SQL inclui novas opções de tempo limite para o recurso existente para reversão automática de transações não preparadas. Consulte [Definindo as configurações de tempo limite do lado do servidor para reversão automática de transações não preparadas](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide) mais adiante neste tópico para obter mais detalhes.  
  
## <a name="remarks"></a>Comentários  
 As classes para a implementação das transações distribuídas são as seguintes:  
  
|Classe|Implements|Description|  
|-----------|----------------|-----------------|  
|com.microsoft.sqlserver.jdbc.SQLServerXADataSource|javax.sql.XADataSource|A fábrica de classes para conexões distribuídas.|  
|com.microsoft.sqlserver.jdbc.SQLServerXAResource|javax.transaction.xa.XAResource|O adaptador de recursos para o gerenciador de transações.|  
  
> [!NOTE]  
>  As conexões de transações distribuídas XA usam como padrão o nível de isolamento Leitura Confirmada.  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>Diretrizes e limitações ao usar transações XA  
 As diretrizes adicionais a seguir se aplicam a transações firmemente acopladas:  
  
-   Ao usar transações XA junto com o MS DTC, talvez você observe que a versão atual do MS DTC não oferece suporte ao comportamento de ramificações XA firmemente acopladas. Por exemplo, o MS DTC tem um mapeamento um-para-um entre uma ID de transação de ramificação XA (XID) e uma ID de transação do MS DTC, e as operações executadas por ramificações XA frouxamente acopladas são isoladas uma da outra.  
  
     O hotfix fornecido em [MSDTC e transações firmemente acopladas](http://support.microsoft.com/kb/938653) habilita o suporte a ramificações XA firmemente acopladas em que várias ramificações XA com a mesma transação global ID (GTRID) são mapeadas para uma única ID de transação de MS DTC. Esse suporte permite que várias ramificações XA firmemente acopladas vejam as alterações uma da outra no Gerenciador de recursos, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Um [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) sinalizador permite que os aplicativos usem transações XA firmemente acopladas que têm a transação de ramificação XA IDs (bQual) diferentes, mas a mesma transação global (GTRID) de ID e ID de formato (FormatID). Para usar esse recurso, você deve definir o [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) no parâmetro de sinalizadores do método XAResource.start:  
  
    ```  
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>Instruções de configuração  
 As etapas a seguir serão necessárias se você desejar usar fontes de dados XA junto com o MS DTC para tratar de transações distribuídas.  
  
> [!NOTE]  
>  Os componentes de transações distribuídas do JDBC são incluídos no diretório xa da instalação do driver JDBC. Esses componentes incluem os arquivos xa_install.sql e sqljdbc_xa.dll.  
  
### <a name="running-the-ms-dtc-service"></a>Executando o serviço MS DTC  
 O serviço MS DTC deve ser marcado como **automático** no Service Manager para certificar-se de que ele está em execução quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] serviço foi iniciado. Para habilitar o MS DTC para transações XA, você deve seguir estas etapas:  
  
 No Windows Vista e versão posterior:  
  
1.  Clique o **iniciar** botão, digite **dcomcnfg** no início **pesquisa** caixa e, em seguida, pressione ENTER para abrir **serviços de componentes**. Você também pode digitar %windir%\system32\comexp.msc no **Iniciarpesquisa** caixa para abrir **serviços de componentes**.  
  
2.  Expanda Serviços de Componentes, Computadores, Meu Computador e Coordenador de Transações Distribuídas.  
  
3.  Clique com botão direito **DTC Local** e, em seguida, selecione **propriedades**.  
  
4.  Clique o **segurança** guia o **propriedades de DTC Local** caixa de diálogo.  
  
5.  Selecione o **habilitar transações XA** caixa de seleção e, em seguida, clique em **Okey**. Isso causará a reinicialização do serviço MS DTC.  
  
6.  Clique em **OK** novamente para fechar a caixa de diálogo **Propriedades** e, em seguida, feche **Serviços de Componentes**.  
  
7.  Pare e reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para certificar-se de que ele fique sincronizado com as alterações do MS DTC.  
  
### <a name="configuring-the-jdbc-distributed-transaction-components"></a>Configurando os componentes de transações distribuídas do JDBC  
 Você pode configurar os componentes de transações distribuídas do driver JDBC seguindo estas etapas:  
  
1.  Copie o novo arquivo sqljdbc_xa.dll do diretório de instalação do driver JDBC para o diretório Binn de cada [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] transações distribuídas do computador que participará.  
  
    > [!NOTE]  
    >  Se você estiver usando transações XA com 32 bits [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], use o arquivo sqljdbc_xa.dll no x86 pasta, mesmo se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está instalado em um x64 processador. Se você estiver usando transações XA com 64 bits [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] em x64 processador, use o arquivo sqljdbc_xa.dll no x64 pasta.  
  
2.  Execute o banco de dados script xa_install.sql em cada [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] transações distribuídas de instância que participará. Esse script instala os procedimentos armazenados estendidos que são chamados por sqljdbc_xa.dll. Esses procedimentos armazenados estendidos implementam transações distribuídas e XA suporte para o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Você precisará executar o script como um administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instância.  
  
3.  Para conceder permissões para um usuário específico participar de transações distribuídas com o driver JDBC, adicione o usuário à função SqlJDBCXAUser.  
  
 Você pode configurar apenas uma versão do assembly sqljdbc_xa.dll de cada [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instância por vez. Talvez seja necessário usar versões diferentes do driver JDBC para se conectar à mesma aplicativos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instância usando a conexão XA. Nesse caso, o arquivo sqljdbc_xa.dll, que é fornecido com o driver JDBC mais recente, deve ser instalado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instância.  
  
 Há três maneiras de verificar a versão de sqljdbc_xa.dll está instalada no momento a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instância:  
  
1.  Abra o diretório LOG do computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que participará de transações distribuídas. Selecione e abra o arquivo "ERRORLOG" do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Procure a frase "Using 'SQLJDBC_XA.dll' version ..." no arquivo "ERRORLOG".  
  
2.  Abra o diretório Binn do computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que participará de transações distribuídas.  
  
    -   No Windows Vista ou em versões posteriores: clique com o botão direito do mouse em sqljdbc_xa.dll e selecione Propriedades. Em seguida, clique na guia **Detalhes**. O campo **Versão do Arquivo** mostra a versão de sqljdbc_xa.dll que está instalada atualmente na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
3.  Defina a funcionalidade de registro em log conforme mostrado no exemplo de código na próxima seção. Procure a frase "Server XA DLL version:..." no arquivo de log de saída.  
  
###  <a name="BKMK_ServerSide"></a>Configurar as configurações de tempo limite do lado do servidor para reversão automática de transações não preparadas  
  
> [!WARNING]  
>  Essa opção no lado do servidor é nova com o Microsoft JDBC Driver 4.2 (e superior) para o SQL Server. Para obter o comportamento atualizado, verifique se o sqljdbc_xa.dll no servidor está atualizado. Para obter mais detalhes sobre como definir tempos limite do lado do cliente, consulte [Xaresource](http://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html).  
  
 Há duas configurações de Registro (valores DWORD) para controlar o comportamento de tempo limite de transações distribuídas:  
  
-   **XADefaultTimeout** (em segundos): O valor de tempo limite padrão a ser usado quando o usuário não especificar nenhum tempo limite. O padrão é 0.  
  
-   **XAMaxTimeout** (em segundos): O valor máximo de tempo limite que um usuário pode definir. O padrão é 0.  
  
 Essas configurações são específicas da instância do SQL Server e devem ser criadas na seguinte chave do Registro:  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.\<**versão**>.\< *instance_name*> \XATimeout  
  
> [!NOTE]  
>  Para 32 bits do SQL Server em execução em máquinas de 64 bits, as configurações do registro devem ser criadas sob a seguinte chave: HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL\<versão >. < nome_da_instância > \ XATimeout  
  
 Um valor de tempo limite é definido para cada transação iniciada e a transação é revertida pelo SQL Server se o tempo limite expirar. O tempo limite é determinado dependendo dessas definições de Registro e daquelas que o usuário tiver especificado por meio de XAResource.setTransactionTimeout(). A seguir estão alguns exemplos de como esses valores de tempo limite são interpretados:  
  
-   XADefaultTimeout = 0, XAMaxTimeout = 0  
  
     Significa que nenhum tempo limite padrão será usado e nenhum tempo limite máximo será aplicado aos clientes. Nesse caso, as transações terão um tempo limite somente se o cliente definir um tempo limite usando XAResource.setTransactionTimeout.  
  
-   XADefaultTimeout = 60, XAMaxTimeout = 0  
  
     Significa que todas as transações terão o tempo limite de 60 segundos se o cliente não especificar nenhum tempo limite. Se o cliente especificar o tempo limite, esse valor de tempo limite será usado. Nenhum valor máximo para o tempo limite é aplicado.  
  
-   XADefaultTimeout = 30, XAMaxTimeout = 60  
  
     Significa que todas as transações terão o tempo limite de 30 segundos se o cliente não especificar nenhum tempo limite. Se cliente especificar qualquer tempo limite, então o tempo limite do cliente será usado, desde que seja inferior a 60 segundos (valor máximo).  
  
-   XADefaultTimeout = 0, XAMaxTimeout = 30  
  
     Significa que todas as transações terão o tempo limite de 30 segundos (valor máximo) se o cliente não especificar nenhum tempo limite. Se cliente especificar qualquer tempo limite, então o tempo limite do cliente será usado, desde que seja inferior a 30 segundos (valor máximo).  
  
### <a name="upgrading-sqljdbcxadll"></a>Atualizando o sqljdbc_xa.dll  
 Ao instalar uma nova versão do driver JDBC, você também deve usar o arquivo sqljdbc_xa.dll da nova versão para atualizar sqljdbc_xa.dll no servidor.  
  
> [!IMPORTANT]  
>  Você deve atualizar o arquivo sqljdbc_xa.dll durante a janela de manutenção ou quando não houver transações MS DTC em andamento.  
  
1.  Descarregue sqljdbc_xa.dll usando o [!INCLUDE[tsql](../../includes/tsql_md.md)] comando **sqljdbc_xa DBCC (FREE)**.  
  
2.  Copie o novo arquivo sqljdbc_xa.dll do diretório de instalação do driver JDBC para o diretório Binn de cada [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] transações distribuídas do computador que participará.  
  
     A nova DLL será carregada quando um procedimento estendido em sqljdbc_xa.dll for chamado. Você não precisa reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para carregar as novas definições.  
  
### <a name="configuring-the-user-defined-roles"></a>Configurando as funções definidas pelo usuário  
 Para conceder permissões para um usuário específico participar de transações distribuídas com o driver JDBC, adicione o usuário à função SqlJDBCXAUser. Por exemplo, use a seguinte [!INCLUDE[tsql](../../includes/tsql_md.md)] código para adicionar um usuário nomeado 'shelby' (o usuário de logon padrão do SQL chamado 'shelby') à função SqlJDBCXAUser:  
  
```  
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```  
  
 As funções definidas pelo usuário do SQL são definidas por banco de dados. Para criar sua própria função para fins de segurança, você terá que definir a função em cada banco de dados e adicionar os usuários para cada banco de dados. A função SqlJDBCXAUser é definida estritamente no banco de dados mestre porque é usada para conceder acesso aos procedimentos armazenados estendidos do SQL JDBC que residem no mestre. Primeiro, você precisará conceder acessos de usuário individuais ao mestre e, em seguida, conceder a eles acesso à função SqlJDBCXAUser enquanto você estiver conectado ao banco de dados mestre.  
  
## <a name="example"></a>Exemplo  
  
```  
import java.net.Inet4Address;  
import java.sql.*;  
import java.util.Random;  
import javax.transaction.xa.*;  
import javax.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class testXA {  
  
   public static void main(String[] args) throws Exception {  
  
      // Create variables for the connection string.  
      String prefix = "jdbc:sqlserver://";  
      String serverName = "localhost";  
      int portNumber = 1433;  
      String databaseName = "AdventureWorks";   
      String user = "UserName";   
      String password = "*****";  
      String connectionUrl = prefix + serverName + ":" + portNumber  
         + ";databaseName=" + databaseName + ";user=" + user + ";password=" + password;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         Connection con = DriverManager.getConnection(connectionUrl);  
  
         // Create a test table.  
         Statement stmt = con.createStatement();  
         try {  
            stmt.executeUpdate("DROP TABLE XAMin");   
         }  
         catch (Exception e) {  
         }  
         stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");  
         stmt.close();  
         con.close();  
  
         // Create the XA data source and XA ready connection.  
         SQLServerXADataSource ds = new SQLServerXADataSource();  
         ds.setUser(user);  
         ds.setPassword(password);  
         ds.setServerName(serverName);  
         ds.setPortNumber(portNumber);  
         ds.setDatabaseName(databaseName);  
         XAConnection xaCon = ds.getXAConnection();  
         con = xaCon.getConnection();  
  
         // Get a unique Xid object for testing.  
         XAResource xaRes = null;  
         Xid xid = null;  
         xid = XidImpl.getUniqueXid(1);  
  
         // Get the XAResource object and set the timeout value.  
         xaRes = xaCon.getXAResource();  
         xaRes.setTransactionTimeout(0);  
  
         // Perform the XA transaction.  
         System.out.println("Write -> xid = " + xid.toString());  
         xaRes.start(xid,XAResource.TMNOFLAGS);  
         PreparedStatement pstmt =   
         con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");  
         pstmt.setInt(1,1);  
         pstmt.setString(2,xid.toString());  
         pstmt.executeUpdate();  
  
         // Commit the transaction.  
         xaRes.end(xid,XAResource.TMSUCCESS);  
         xaRes.commit(xid,true);  
  
         // Cleanup.  
         con.close();  
         xaCon.close();  
  
         // Open a new connection and read back the record to verify that it worked.  
         con = DriverManager.getConnection(connectionUrl);  
         ResultSet rs = con.createStatement().executeQuery("SELECT * FROM XAMin");  
         rs.next();  
         System.out.println("Read -> xid = " + rs.getString(2));  
         rs.close();  
         con.close();  
      }   
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
  
class XidImpl implements Xid {  
  
   public int formatId;  
   public byte[] gtrid;  
   public byte[] bqual;  
   public byte[] getGlobalTransactionId() {return gtrid;}  
   public byte[] getBranchQualifier() {return bqual;}  
   public int getFormatId() {return formatId;}  
  
   XidImpl(int formatId, byte[] gtrid, byte[] bqual) {  
      this.formatId = formatId;  
      this.gtrid = gtrid;  
      this.bqual = bqual;  
   }  
  
   public String toString() {  
      int hexVal;  
      StringBuffer sb = new StringBuffer(512);  
      sb.append("formatId=" + formatId);  
      sb.append(" gtrid(" + gtrid.length + ")={0x");  
      for (int i=0; i<gtrid.length; i++) {  
         hexVal = gtrid[i]&0xFF;  
         if ( hexVal < 0x10 )  
            sb.append("0" + Integer.toHexString(gtrid[i]&0xFF));  
         else  
            sb.append(Integer.toHexString(gtrid[i]&0xFF));  
         }  
         sb.append("} bqual(" + bqual.length + ")={0x");  
         for (int i=0; i<bqual.length; i++) {  
            hexVal = bqual[i]&0xFF;  
            if ( hexVal < 0x10 )  
               sb.append("0" + Integer.toHexString(bqual[i]&0xFF));  
            else  
               sb.append(Integer.toHexString(bqual[i]&0xFF));  
         }  
         sb.append("}");  
         return sb.toString();  
      }  
  
      // Returns a globally unique transaction id.  
      static byte [] localIP = null;  
      static int txnUniqueID = 0;  
      static Xid getUniqueXid(int tid) {  
  
      Random rnd = new Random(System.currentTimeMillis());  
      txnUniqueID++;  
      int txnUID = txnUniqueID;  
      int tidID = tid;  
      int randID = rnd.nextInt();  
      byte[] gtrid = new byte[64];  
      byte[] bqual = new byte[64];  
      if ( null == localIP) {  
         try {  
            localIP = Inet4Address.getLocalHost().getAddress();  
         }  
         catch ( Exception ex ) {  
            localIP =  new byte[] { 0x01,0x02,0x03,0x04 };  
         }  
      }  
      System.arraycopy(localIP,0,gtrid,0,4);  
      System.arraycopy(localIP,0,bqual,0,4);  
  
      // Bytes 4 -> 7 - unique transaction id.  
      // Bytes 8 ->11 - thread id.  
      // Bytes 12->15 - random number generated by using seed from current time in milliseconds.  
      for (int i=0; i<=3; i++) {  
         gtrid[i+4] = (byte)(txnUID%0x100);  
         bqual[i+4] = (byte)(txnUID%0x100);  
         txnUID >>= 8;  
         gtrid[i+8] = (byte)(tidID%0x100);  
         bqual[i+8] = (byte)(tidID%0x100);  
         tidID >>= 8;  
         gtrid[i+12] = (byte)(randID%0x100);  
         bqual[i+12] = (byte)(randID%0x100);  
         randID >>= 8;  
      }  
      return new XidImpl(0x1234, gtrid, bqual);  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Executando transações com o JDBC Driver](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
