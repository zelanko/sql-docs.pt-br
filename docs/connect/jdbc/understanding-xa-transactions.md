---
title: Noções básicas sobre transações XA | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e249bb515ca0a8b579e923e7d289fccd80ce6ef
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286510"
---
# <a name="understanding-xa-transactions"></a>Noções básicas sobre transações XA

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte a transações distribuídas opcionais para Plataforma Java, Enterprise Edition/JDBC 2.0. Conexões JDBC obtidas da classe [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) podem participar de ambientes de processamento de transações distribuídas padrão como os servidores de aplicativos da Plataforma Java, Java EE (Enterprise Edition).  

Neste artigo, o XA significa arquitetura estendida.

> [!WARNING]  
> O Microsoft JDBC Driver 4.2 (e superiores) for SQL inclui novas opções de tempo limite para o recurso existente para reversão automática de transações não preparadas. Confira [Configuração das definições de tempo limite do servidor para reversão automática de transações não preparadas](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide) posteriormente neste tópico para encontrar mais detalhes.  

## <a name="remarks"></a>Comentários

As classes para a implementação das transações distribuídas são as seguintes:  
  
| Classe                                              | Implementa                      | Descrição                                       |
| -------------------------------------------------- | ------------------------------- | ------------------------------------------------- |
| com.microsoft.sqlserver.jdbc.SQLServerXADataSource | javax.sql.XADataSource          | A fábrica de classes para conexões distribuídas.    |
| com.microsoft.sqlserver.jdbc.SQLServerXAResource   | javax.transaction.xa.XAResource | O adaptador de recursos para o gerenciador de transações. |
  
> [!NOTE]  
> As conexões de transações distribuídas XA usam como padrão o nível de isolamento Leitura Confirmada.  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>Diretrizes e limitações ao usar transações XA  

As diretrizes adicionais a seguir se aplicam a transações firmemente acopladas:  

- Ao usar transações XA junto com o Coordenador de Transações Distribuídas (MS DTC), talvez você observe que a versão atual do MS DTC não oferece suporte ao comportamento de ramificações XA firmemente acopladas. Por exemplo, o MS DTC tem um mapeamento um-para-um entre uma ID de transação de ramificação XA (XID) e uma ID de transação do MS DTC, e as operações executadas por ramificações XA frouxamente acopladas são isoladas uma da outra.  
  
- O MS DTC também é compatível com branches XA bem acoplados em que vários branches XA com a mesma GTRID (ID de transação global) são mapeados para uma ID de transação do MS DTC. Esse suporte permite que vários branches XA bem acoplados reconheçam as alterações feitas no gerenciador de recursos, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
- Um sinalizador [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) permite que os aplicativos usem as transações XA bem acopladas com IDs de transação de branch XA (BQUAL) diferentes, mas a mesma GTRID (ID de transação global) e a mesma FormatID (ID de formato). Para usar esse recurso, você deve definir o [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) no parâmetro de sinalizadores do método XAResource.start:
  
    ```java
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>Instruções de configuração

As etapas a seguir serão necessárias se você desejar usar fontes de dados XA junto com o MS DTC para tratar de transações distribuídas.  

> [!NOTE]  
> Os componentes de transações distribuídas do JDBC são incluídos no diretório xa da instalação do driver JDBC. Esses componentes incluem os arquivos xa_install.sql e sqljdbc_xa.dll.  

> [!NOTE]  
> Começando com o CTP 2.0 da versão prévia pública do SQL Server 2019, os componentes da transação distribuída do JDBC XA estão incluídos no mecanismo do SQL Server e podem ser habilitados ou desabilitados com um procedimento armazenado do sistema.
> Para habilitar os componentes necessários para executar transações distribuídas XA usando o driver JDBC, execute o procedimento armazenado a seguir.
>
> EXEC sp_sqljdbc_xa_install
>
> Para desabilitar os componentes instalados anteriormente, execute o procedimento armazenado a seguir.
>
> EXEC sp_sqljdbc_xa_uninstall

### <a name="running-the-ms-dtc-service"></a>Executando o serviço MS DTC

O serviço MS DTC deve ser marcado como **Automático** no Service Manager para garantir que ele esteja em execução quando o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for iniciado. Para habilitar o MS DTC para transações XA, você deve seguir estas etapas:  
  
No Windows Vista e versão posterior:  
  
1. Clique no botão **Iniciar**, digite **dcomcnfg** na caixa Iniciar **Pesquisa** e pressione ENTER para abrir **Serviços de Componentes**. Você também pode digitar %windir%\system32\comexp.msc na caixa **StartSearch** para abrir **Serviços de Componentes**.  
  
2. Expanda Serviços de Componentes, Computadores, Meu Computador e Coordenador de Transações Distribuídas.  
  
3. Clique com o botão direito do mouse em **DTC Local** e selecione **Propriedades**.  
  
4. Clique na guia **Segurança** na caixa de diálogo **Propriedades de DTC Local**.  
  
5. Marque a caixa de seleção **Habilitar Transações XA** e clique em **OK**. Isso causará uma reinicialização do serviço MS DTC.
  
6. Clique em **OK** novamente para fechar a caixa de diálogo **Propriedades** e feche **Serviços de Componentes**.  
  
7. Pare e reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para assegurar que ele esteja sincronizado com as alterações do MS DTC.  

### <a name="configuring-the-jdbc-distributed-transaction-components"></a>Configurando os componentes de transações distribuídas do JDBC  

Você pode configurar os componentes de transações distribuídas do driver JDBC seguindo estas etapas:  
  
1. Copie o novo sqljdbc_xa.dll do diretório de instalação do driver JDBC para o diretório Binn de cada computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que participará de transações distribuídas.  
  
    > [!NOTE]  
    > Se você estiver usando transações XA com um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits, use o arquivo sqljdbc_xa.dll na pasta x86, mesmo que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esteja instalado em um processador x64. Se estiver usando transações XA com um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits no processador x64, use o arquivo sqljdbc_xa.dll na pasta x64.  
  
2. Execute o script do banco de dados xa_install.sql em cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que participará de transações distribuídas. Esse script instala os procedimentos armazenados estendidos que são chamados por sqljdbc_xa.dll. Esses procedimentos armazenados estendidos implementam o suporte a transações distribuídas e XA para o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Você precisará executar o script como administrador da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3. Para conceder permissões para um usuário específico participar de transações distribuídas com o driver JDBC, adicione o usuário à função SqlJDBCXAUser.  
  
Só é possível configurar uma versão do assembly sqljdbc_xa.dll de cada vez em cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Talvez os aplicativos precisem usar versões diferentes do driver JDBC para conectarem-se à mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a conexão XA. Nesse caso, o arquivo sqljdbc_xa.dll, que vem com o driver JDBC mais recente, deve ser instalado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Há três maneiras de verificar qual versão do sqljdbc_xa.dll está instalada no momento na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:
  
1. Abra o diretório LOG do computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que participará de transações distribuídas. Selecione e abra o arquivo "ERRORLOG" do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Procure a frase "Using 'SQLJDBC_XA.dll' version ..." no arquivo "ERRORLOG".  
  
2. Abra o diretório Binn do computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que participará de transações distribuídas. Selecione o assembly sqljdbc_xa.dll.

    - No Windows Vista ou posterior: Clique com o botão direito do mouse em sqljdbc_xa.dll e selecione Propriedades. Em seguida, clique na guia **Detalhes**. O campo **Versão do Arquivo** mostra a versão de sqljdbc_xa.dll que está instalada no momento na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3. Defina a funcionalidade de registro em log conforme mostrado no exemplo de código na próxima seção. Procure a frase "Server XA DLL version:..." no arquivo de log de saída.  

### <a name="configuring-server-side-timeout-settings-for-automatic-rollback-of-unprepared-transactions"></a><a name="BKMK_ServerSide"></a> Configurando as definições de tempo limite do servidor para reversão automática de transações não preparadas  

> [!WARNING]  
> Essa opção do servidor é nova no Microsoft JDBC Driver 4.2 (e superiores) para SQL Server. Para obter o comportamento atualizado, verifique se o arquivo sqljdbc_xa.dll no servidor foi atualizado. Para saber mais sobre como configurar o tempo limite no cliente, veja [XAResource.setTransactionTimeout()](https://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html).  

Há duas configurações de Registro (valores DWORD) para controlar o comportamento de tempo limite de transações distribuídas:  
  
- **XADefaultTimeout** (em segundos): O valor de tempo limite padrão a ser usado quando o usuário não especifica nenhum tempo limite. O padrão é 0.  
  
- **XAMaxTimeout** (em segundos): O valor máximo do tempo limite que um usuário pode definir. O padrão é 0.  
  
Essas configurações são específicas da instância do SQL Server e devem ser criadas na seguinte chave do Registro:  

```bash
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout  
```

> [!NOTE]  
> Para o SQL Server de 32 bits em execução em máquinas de 64 bits, as configurações de Registro devem ser criadas na seguinte chave: `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout`
  
Um valor de tempo limite é definido para cada transação iniciada e a transação é revertida pelo SQL Server se o tempo limite expirar. O tempo limite é determinado dependendo dessas definições de Registro e daquelas que o usuário tiver especificado por meio de XAResource.setTransactionTimeout(). A seguir estão alguns exemplos de como esses valores de tempo limite são interpretados:  
  
- `XADefaultTimeout = 0`, `XAMaxTimeout = 0`
  
     Significa que nenhum tempo limite padrão será usado e nenhum tempo limite máximo será aplicado aos clientes. Nesse caso, as transações terão um tempo limite somente se o cliente definir um tempo limite usando XAResource.setTransactionTimeout.  
  
- `XADefaultTimeout = 60`, `XAMaxTimeout = 0`
  
     Significa que todas as transações terão o tempo limite de 60 segundos se o cliente não especificar nenhum tempo limite. Se o cliente especificar o tempo limite, esse valor de tempo limite será usado. Nenhum valor máximo para o tempo limite é aplicado.  
  
- `XADefaultTimeout = 30`, `XAMaxTimeout = 60`
  
     Significa que todas as transações terão o tempo limite de 30 segundos se o cliente não especificar nenhum tempo limite. Se o cliente especificar um tempo limite, ele será usado desde que seja inferior a 60 segundos (o valor máximo).  
  
- `XADefaultTimeout = 0`, `XAMaxTimeout = 30`
  
     Significa que todas as transações terão o tempo limite de 30 segundos (valor máximo) se o cliente não especificar nenhum tempo limite. Se o cliente especificar um tempo limite, ele será usado desde que seja inferior a 30 segundos (o valor máximo).  
  
### <a name="upgrading-sqljdbc_xadll"></a>Atualizando o sqljdbc_xa.dll

Ao instalar uma nova versão do driver JDBC, você também deve usar o arquivo sqljdbc_xa.dll da nova versão para atualizar sqljdbc_xa.dll no servidor.  
  
> [!IMPORTANT]  
> Você deve atualizar o sqljdbc_xa.dll durante a janela de manutenção ou quando não houver nenhuma transação do MS DTC em andamento.
  
1. Descarregue o sqljdbc_xa.dll usando o comando [!INCLUDE[tsql](../../includes/tsql-md.md)] **DBCC sqljdbc_xa (FREE)** .  
  
2. Copie o novo sqljdbc_xa.dll do diretório de instalação do driver JDBC para o diretório Binn de cada computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que participará de transações distribuídas.  
  
    A nova DLL será carregada quando um procedimento estendido em sqljdbc_xa.dll for chamado. Você não precisa reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para carregar as novas definições.  
  
### <a name="configuring-the-user-defined-roles"></a>Configurando as funções definidas pelo usuário

Para conceder permissões para um usuário específico participar de transações distribuídas com o driver JDBC, adicione o usuário à função SqlJDBCXAUser. Por exemplo, use o código [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir para adicionar um usuário nomeado 'shelby' (usuário com logon padrão do SQL chamado 'shelby') à função SqlJDBCXAUser:  

```sql
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```

As funções definidas pelo usuário do SQL são definidas por banco de dados. Para criar sua própria função para fins de segurança, você terá que definir a função em cada banco de dados e adicionar os usuários para cada banco de dados. A função SqlJDBCXAUser é definida estritamente no banco de dados mestre porque é usada para conceder acesso aos procedimentos armazenados estendidos do SQL JDBC que residem no mestre. Primeiro, você precisará conceder acessos de usuário individuais ao mestre e, em seguida, conceder a eles acesso à função SqlJDBCXAUser enquanto você estiver conectado ao banco de dados mestre.  

## <a name="example"></a>Exemplo  

```java
import java.net.Inet4Address;
import java.sql.*;
import java.util.Random;
import javax.sql.XAConnection;
import javax.transaction.xa.*;
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

        String connectionUrl = prefix + serverName + ":" + portNumber + ";databaseName=" + databaseName + ";user="
                + user + ";password=" + password;

        Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement()) {
            stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");

        }
        // Create the XA data source and XA ready connection.
        SQLServerXADataSource ds = new SQLServerXADataSource();
        ds.setUser(user);
        ds.setPassword(password);
        ds.setServerName(serverName);
        ds.setPortNumber(portNumber);
        ds.setDatabaseName(databaseName);

        XAConnection xaCon = ds.getXAConnection();
        try (Connection con = xaCon.getConnection()) {

            // Get a unique Xid object for testing.
            XAResource xaRes = null;
            Xid xid = null;
            xid = XidImpl.getUniqueXid(1);

            // Get the XAResource object and set the timeout value.
            xaRes = xaCon.getXAResource();
            xaRes.setTransactionTimeout(0);

            // Perform the XA transaction.
            System.out.println("Write -> xid = " + xid.toString());
            xaRes.start(xid, XAResource.TMNOFLAGS);
            PreparedStatement pstmt = con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");
            pstmt.setInt(1, 1);
            pstmt.setString(2, xid.toString());
            pstmt.executeUpdate();

            // Commit the transaction.
            xaRes.end(xid, XAResource.TMSUCCESS);
            xaRes.commit(xid, true);
        }
        xaCon.close();

        // Open a new connection and read back the record to verify that it worked.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT * FROM XAMin")) {
            rs.next();
            System.out.println("Read -> xid = " + rs.getString(2));
            stmt.executeUpdate("DROP TABLE XAMin");
        }
    }
}


class XidImpl implements Xid {

    public int formatId;
    public byte[] gtrid;
    public byte[] bqual;

    public byte[] getGlobalTransactionId() {
        return gtrid;
    }

    public byte[] getBranchQualifier() {
        return bqual;
    }

    public int getFormatId() {
        return formatId;
    }

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
        for (int i = 0; i < gtrid.length; i++) {
            hexVal = gtrid[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(gtrid[i] & 0xFF));
            else
                sb.append(Integer.toHexString(gtrid[i] & 0xFF));
        }
        sb.append("} bqual(" + bqual.length + ")={0x");
        for (int i = 0; i < bqual.length; i++) {
            hexVal = bqual[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(bqual[i] & 0xFF));
            else
                sb.append(Integer.toHexString(bqual[i] & 0xFF));
        }
        sb.append("}");
        return sb.toString();
    }

    // Returns a globally unique transaction id.
    static byte[] localIP = null;
    static int txnUniqueID = 0;

    static Xid getUniqueXid(int tid) {

        Random rnd = new Random(System.currentTimeMillis());
        txnUniqueID++;
        int txnUID = txnUniqueID;
        int tidID = tid;
        int randID = rnd.nextInt();
        byte[] gtrid = new byte[64];
        byte[] bqual = new byte[64];
        if (null == localIP) {
            try {
                localIP = Inet4Address.getLocalHost().getAddress();
            } catch (Exception ex) {
                localIP = new byte[] {0x01, 0x02, 0x03, 0x04};
            }
        }
        System.arraycopy(localIP, 0, gtrid, 0, 4);
        System.arraycopy(localIP, 0, bqual, 0, 4);

        // Bytes 4 -> 7 - unique transaction id.
        // Bytes 8 ->11 - thread id.
        // Bytes 12->15 - random number generated by using seed from current time in milliseconds.
        for (int i = 0; i <= 3; i++) {
            gtrid[i + 4] = (byte) (txnUID % 0x100);
            bqual[i + 4] = (byte) (txnUID % 0x100);
            txnUID >>= 8;
            gtrid[i + 8] = (byte) (tidID % 0x100);
            bqual[i + 8] = (byte) (tidID % 0x100);
            tidID >>= 8;
            gtrid[i + 12] = (byte) (randID % 0x100);
            bqual[i + 12] = (byte) (randID % 0x100);
            randID >>= 8;
        }
        return new XidImpl(0x1234, gtrid, bqual);
    }
}

```

## <a name="see-also"></a>Confira também  

[Executando transações com o JDBC Driver](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
