---
title: "Preparar SQL Server para CDC | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "prepSqlSrv"
ms.assetid: 20b51dbf-a545-4234-87ae-4228268a0fb2
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Preparar SQL Server para CDC
  O serviço Oracle CDC exige que todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino contenham o banco de dados MSXDBCDC. Você cria este banco de dados usando a ação Preparar ação do SQL Server no Console de Configuração do Serviço CDC. Isto cria um script especial que é executado para criar as tabelas exigidas, os procedimentos armazenados e outros artefatos necessários para este banco de dados. Esta tarefa só é feita uma vez para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 Para obter mais informações sobre o banco de dados MSXDBCDC, consulte O banco de dados MSXDBCDC.  
  
 No Console de Configuração do Serviço CDC, clique em **Preparar SQL Server**. Se esta opção não estiver disponível, verifique se a opção **Serviços Locais CDC** está marcada no painel esquerdo do console.  
  
## Opções  
  
### Nome do servidor  
 Digite o nome do servidor em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está localizado.  
  
### Autenticação  
 Selecione uma destas opções:  
  
-   **Autenticação do Windows**  
  
-   **Autenticação do SQL Server**: se você selecionar esta opção, deverá digitar o **Nome de Usuário** e a **Senha** para o usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual você está se conectando.  
  
 Para preparar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Oracle CDC, o logon deve ter permissão de gravação no banco de dados MSXDBCDC. Insira as credenciais para um logon que tem permissão de gravação no banco de dados MSXDBCDC, como um membro da função `sysasmin` .  
  
### Opções  
 Clique na seta para exibir opções disponíveis a serem configuradas. Você pode escolher deixar estas opções com o valor padrão. As opções disponíveis são:  
  
-   **Tempo limite de conexão**: digite o tempo (em segundos) que o Serviço CDC para Oracle aguarda uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de exceder o tempo limite. O valor padrão é **15**.  
  
-   **Tempo limite de execução**: digite o tempo (em segundos) que o Serviço Windows do Oracle CDC aguarda até que um comando seja executado antes de exceder o tempo limite. O valor padrão é **30**.  
  
-   **Criptografar Conexão**: selecione **Criptografar Conexão** para a comunicação entre o Serviço Oracle CDC e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino usando uma conexão criptografada.  
  
-   **Avançado**: digite as propriedades de conexão adicionais, se necessário.  
  
### Exibir script  
 Clique em **Exibir Script** para exibir uma versão somente leitura do script de instalação. Um administrador do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode copiar este script no Console de Gerenciamento do SQL Server para editá-lo, se for necessário. Para obter mais informações sobre o Script Preparar SQL Server, consulte [Script de visualização Preparar SQL Server para Oracle CDC](../../integration-services/change-data-capture/prepare-sql-server-for-oracle-cdc-view-script.md).  
  
## Consulte também  
 [Como trabalhar com os serviços CDC](../../integration-services/change-data-capture/how-to-work-with-cdc-services.md)   
 [Como Preparar o SQL Server para CDC](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
  