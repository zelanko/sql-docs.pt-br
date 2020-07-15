---
title: Espelhamento de Banco de Dados – usar certificados para conexões de saída | Microsoft Docs
description: Saiba como configurar instâncias de servidor para usar certificados para autenticar conexões de entrada para espelhamento de banco de dados, depois de configurar as conexões de saída.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- certificates [SQL Server], database mirroring
- outbound connections [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 464c9096-10d6-4c5e-8bb1-19acba27ad9e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2837bcba7069f3259b23446137aa6162b2443189
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754682"
---
# <a name="database-mirroring---use-certificates-for-outbound-connections"></a>Espelhamento de Banco de Dados – usar certificados para conexões de saída
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve os passos para configurar instâncias de servidor para usar certificados para autenticar conexões de saída para espelhamento de banco de dados. A configuração de conexão de saída deve ser feita antes que você possa configurar conexões de entrada.  
  
> [!NOTE]  
>  Todas as conexões de espelhamento em uma instância do servidor usam um único ponto de extremidade de espelhamento do banco de dados e você deve especificar o método de autenticação da instância do servidor quando criar o ponto de extremidade.  
  
 O processo de configurar conexões de saída envolve os seguintes passos gerais:  
  
1.  No banco de dados **mestre** , crie um banco de dados chave mestre.  
  
2.  No banco de dados **mestre** , crie um certificado criptografado na instância de servidor.  
  
3.  Crie um ponto de extremidade para a instância do servidor que usa seu certificado.  
  
4.  Faça o backup do certificado em um arquivo e o copie-o com segurança para outro sistema ou sistemas.  
  
 Você deve completar essas etapas para cada parceiro e para a testemunha, se houver.  
  
 O procedimento a seguir descreve em detalhes essas etapas. Para cada etapa, o processo fornece um exemplo para configurar a instância do servidor em um sistema chamado de HOST_A. A seção de exemplo mostra as mesmas etapas para uma outra instância do servidor em um sistema chamado de HOST_B.  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="to-configure-server-instances-for-outbound-mirroring-connections-on-host_a"></a>Para configurar as instâncias de servidor para espelhamento de conexões de saída (No HOST_A)  
  
1.  No banco de dados **mestre** , crie o banco de dados chave mestre, se nenhum existir. Para exibir as chaves existentes para um banco de dados, use a exibição do catálogo [sys.symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md) .  
  
     Para criar o banco de dados chave mestre, use o seguinte comando [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<1_Strong_Password!>';  
    GO  
    ```  
  
     Use uma senha exclusiva forte e a registre em um lugar seguro.  
  
     Para obter mais informações, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) e [Criar uma chave mestra de banco de dados](../../relational-databases/security/encryption/create-a-database-master-key.md).  
  
2.  No banco de dados **master** , crie um certificado criptografado na instância de servidor a ser usado nas suas conexões de saída para espelhamento de banco de dados.  
  
     Por exemplo, para criar um certificado para o sistema HOST_A.  
  
    > [!IMPORTANT]  
    >  Se você pretende usar o certificado por mais de um ano, especifique a data de expiração em hora UTC usando a opção EXPIRY_DATE em sua instrução CREATE CERTIFICATE. Além disso, é recomendável que você use o SQL Server Management Studio para criar uma regra de gerenciamento baseado em políticas para alertá-lo quando seus certificados estiverem expirando. Usando a caixa de diálogo **Criar Condição** do Gerenciamento de Política, crie essa regra no campo **\@ExpirationDate** da faceta **Certificado**. Para obter mais informações, veja [Administrar servidores usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md) e [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md).  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_A_cert   
       WITH SUBJECT = 'HOST_A certificate for database mirroring',   
       EXPIRY_DATE = '11/30/2013';  
    GO  
    ```  
  
     Para obter mais informações, consulte [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md).  
  
     Para exibir os certificados no banco de dados **mestre** , você pode usar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] seguintes:  
  
    ```  
    USE master;  
    SELECT * FROM sys.certificates;  
    ```  
  
     Para obter mais informações, veja [sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md).  
  
3.  Assegure que o ponto de extremidade do espelhamento de banco de dados exista em cada uma das instâncias de servidor.  
  
     Se um ponto de extremidade do espelhamento de banco de dados já existir para a instância de servidor, você deveria usar de novo aquele ponto de extremidade para qualquer outra sessão que você estabeleça na instância de servidor. Para determinar se um ponto de extremidade do espelhamento de banco de dados existe em uma instância de servidor e exibir sua configuração, use a instrução seguinte:  
  
    ```  
    SELECT name, role_desc, state_desc, connection_auth_desc, encryption_algorithm_desc   
       FROM sys.database_mirroring_endpoints;  
    ```  
  
     Se nenhum ponto de extremidade existir, crie um ponto de extremidade que usa este certificado para conexões de saída e que usa as credenciais do certificado para verificação no outro sistema. Este é um ponto de extremidade em todo servidor que é usado por todas as sessões de espelhamento nas quais a instância de servidor participa.  
  
     Por exemplo, para criar um espelhamento de ponto de extremidade para a instância de servidor de exemplo em HOST_A.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
       STATE = STARTED  
       AS TCP (  
          LISTENER_PORT=7024  
          , LISTENER_IP = ALL  
       )   
       FOR DATABASE_MIRRORING (   
          AUTHENTICATION = CERTIFICATE HOST_A_cert  
          , ENCRYPTION = REQUIRED ALGORITHM AES  
          , ROLE = ALL  
       );  
    GO  
    ```  
  
     Para obter mais informações, veja [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
4.  Faça o backup do certificado e o copie ao outro sistema ou sistemas. Isto é necessário para configurar as conexões de entrada no outro sistema.  
  
    ```  
    BACKUP CERTIFICATE HOST_A_cert TO FILE = 'C:\HOST_A_cert.cer';  
    GO  
    ```  
  
     Para obter mais informações, veja [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md).  
  
     Copie este certificado usando qualquer método seguro de sua escolha. Seja extremamente cauteloso para manter todos os seus certificados em segurança.  
  
 O código de exemplo nos passos precedentes configura conexões de saída no HOST_A.  
  
 Você precisa realizar os passos de saída equivalentes para o HOST_B. Esses passos estão ilustrados na seguinte seção de exemplo.  
  
## <a name="example"></a>Exemplo  
 O exemplo seguinte demonstra como configurar o HOST_B para conexões de saída.  
  
```  
USE master;  
--Create the database Master Key, if needed.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<Strong_Password_#2>';  
GO  
-- Make a certifcate on HOST_B server instance.  
CREATE CERTIFICATE HOST_B_cert   
   WITH SUBJECT = 'HOST_B certificate for database mirroring',   
   EXPIRY_DATE = '11/30/2013';  
GO  
--Create a mirroring endpoint for the server instance on HOST_B.  
CREATE ENDPOINT Endpoint_Mirroring  
   STATE = STARTED  
   AS TCP (  
      LISTENER_PORT=7024  
      , LISTENER_IP = ALL  
   )   
   FOR DATABASE_MIRRORING (   
      AUTHENTICATION = CERTIFICATE HOST_B_cert  
      , ENCRYPTION = REQUIRED ALGORITHM AES  
      , ROLE = ALL  
   );  
GO  
--Backup HOST_B certificate.  
BACKUP CERTIFICATE HOST_B_cert TO FILE = 'C:\HOST_B_cert.cer';  
GO   
--Using any secure copy method, copy C:\HOST_B_cert.cer to HOST_A.  
```  
  
 Copie o certificado ao outro sistema usando qualquer método seguro de sua escolha. Seja extremamente cauteloso para manter todos os seus certificados em segurança.  
  
> [!IMPORTANT]  
>  Depois que você tiver configurado as conexões de saída, você deve configurar as conexões de entrada em cada instância de servidor para a outra instância ou instâncias de servidor. Para obter mais informações, consulte [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md).  
  
 Para obter informações sobre como criar um banco de dados espelho, incluindo um exemplo de Transact-SQL, veja [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
 Para obter um exemplo de Transact-SQL para estabelecer uma sessão de modo de alto desempenho, confira [Exemplo: Configurar o espelhamento de banco de dados usando certificados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md).  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 A menos que você possa garantir que sua rede está segura, recomendamos o uso de criptografia para conexões de espelhamento de banco de dados.  
  
 Ao copiar um certificado para outro sistema, use um método de cópia seguro.  
  
## <a name="see-also"></a>Consulte Também  
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [Exemplo: Configurar o espelhamento de banco de dados usando certificados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)   
 [Configurar um banco de dados espelho criptografado](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
  
