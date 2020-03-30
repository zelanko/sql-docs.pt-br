---
title: Como usar o Always Encrypted com enclaves seguros | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: reneye
ms.author: v-reye
ms.openlocfilehash: 441adf8e3623f06bfa98718ebc6c01c314c94828
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77004705"
---
# <a name="using-always-encrypted-with-the-secure-enclaves"></a>Como usar o Always Encrypted com enclaves seguros
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Esta página fornece informações sobre como desenvolver aplicativos do Java usando o [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md) e o Microsoft JDBC Driver 8.2 (ou superior) para SQL Server.

Os enclaves seguros são uma adição ao recurso existente do [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md). A finalidade dos enclaves seguros é resolver as limitações ao trabalhar usando dados do Always Encrypted. Anteriormente, os usuários podiam executar apenas comparações de igualdade nos dados do Always Encrypted e tinham que recuperar e descriptografar os dados para executar outras operações. Os enclaves seguros solucionam essas limitações, permitindo realizar cálculos em dados de texto não criptografado em um enclave seguro no lado do servidor. Um enclave seguro é uma região protegida de memória dentro do processo do SQL Server e atua como um ambiente de execução confiável para o processamento de dados confidenciais dentro do mecanismo do SQL Server. Um enclave seguro é exibido como uma caixa preta para o restante do SQL Server e outros processos no computador de hospedagem. Não há nenhuma maneira de exibir os dados ou o código dentro do enclave de fora, mesmo com um depurador.

## <a name="prerequisites"></a>Prerequisites
- O Microsoft JDBC Driver 8.2 (ou superior ) para SQL Server deve estar instalado em seu computador de desenvolvimento. 

> [!Note]
> Se estiver usando uma versão anterior do JDK 8, poderá ser necessário baixar e instalar os arquivos de política de jurisdição de força ilimitada do JCE (Java Cryptography Extension). Leia o arquivo Leiame incluído no arquivo zip para instruções de instalação e detalhes relevantes sobre problemas possíveis de importação/exportação.  
>
> Os arquivos de política podem ser baixados em [Download dos arquivos de política de jurisdição de força ilimitada do JCE (Java Cryptography Extension) 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

## <a name="setting-up-secure-enclaves"></a>Como configurar os enclaves seguros
Siga este [tutorial](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md) para começar a usar os enclaves seguros. Para obter mais informações, veja [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="connection-string-properties"></a>Propriedades de cadeia de conexão
**enclaveAttestationUrl:** a URL do ponto de extremidade do serviço de atestado.

**enclaveAttestationProtocol:** o protocolo do serviço de atestado. Atualmente, o único valor compatível é **HGS**(Serviço Guardião de Host).

Os usuários devem habilitar **columnEncryptionSetting** e definir corretamente **ambas** as propriedades da cadeia de conexão acima para habilitar o Always Encrypted com enclaves seguros do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

## <a name="working-with-secure-enclaves"></a>Como trabalhar com enclaves seguros
Quando as propriedades de conexão do enclave forem definidas corretamente, o recurso funcionará de maneira transparente. O driver determinará se a consulta requer o uso de um enclave seguro automaticamente. Veja a seguir exemplos de consultas que disparam cálculos de enclave. Você pode encontrar a configuração de banco de dados e de tabela em [Introdução aos enclaves do Always Encrypted](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md).

As consultas avançadas dispararão cálculos de enclave:
```java
private static final String URL = "jdbc:sqlserver://<server>:<port>;user=<username>;password=<password>;databaseName=ContosoHR;columnEncryptionSetting=enabled;enclaveAttestationUrl=<attestation-url>;enclaveAttestationProtocol=<attestation-protocol>;";
try (Connection c = DriverManager.getConnection(URL)) {
    try (PreparedStatement p = c.prepareStatement("SELECT * FROM Employees WHERE SSN LIKE ?")) {
        p.setString(1, "%6818");
        try (ResultSet rs = p.executeQuery()) {
            while (rs.next()) {
                // Do work with data
            }
        }
    }
    
    try (PreparedStatement p = c.prepareStatement("SELECT * FROM Employees WHERE SALARY > ?")) {
        ((SQLServerPreparedStatement) p).setMoney(1, new BigDecimal(0));
        try (ResultSet rs = p.executeQuery()) {
            while (rs.next()) {
                // Do work with data
            }
        }
    }
}
```

Alternar a criptografia em uma coluna também disparará cálculos de enclave:
```java
private static final String URL = "jdbc:sqlserver://<server>:<port>;user=<username>;password=<password>;databaseName=ContosoHR;columnEncryptionSetting=enabled;enclaveAttestationUrl=<attestation-url>;enclaveAttestationProtocol=<attestation-protocol>;";
try (Connection c = DriverManager.getConnection(URL);Statement s = c.createStatement()) {
    s.executeUpdate("ALTER TABLE Employees ALTER COLUMN SSN CHAR(11) NULL WITH (ONLINE = ON)");
}
```

## <a name="java-8-users"></a>Usuários do Java 8
Esse recurso requer o algoritmo de assinatura RSASSA-PSA. Esse algoritmo foi adicionado ao JDK 11, mas não houve back-port para o JDK 8. Os usuários que desejam usar esse recurso com o JDK versão 8 do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] devem carregar o próprio provedor, que é compatível com o algoritmo de assinatura RSASSA-PSA, ou incluir a dependência opcional BouncyCastleProvider. A dependência será removida em uma data posterior se o JDK 8 fizer back-port do algoritmo de assinatura ou se o ciclo de vida de suporte do JDK 8 terminar.

## <a name="see-also"></a>Confira também
[Como usar Always Encrypted com o JDBC Driver](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  