---
title: "Utilit&#225;rio SqlLocalDB | Microsoft Docs"
ms.custom: ""
ms.date: "08/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Utilitário SqlLocalDB [SQL Server]"
  - "utilitário tempo de execução de banco de dados local"
  - "LocalDB, utilitário SqlLocalDB"
ms.assetid: d785cdb7-1ea0-4871-bde9-1ae7881190f5
caps.latest.revision: 19
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 19
---
# Utilit&#225;rio SqlLocalDB
  Use o utilitário **SqlLocalDB** para criar uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssExpCurrent](../includes/ssexpcurrent-md.md)]**LocalDB**. O utilitário **SqlLocalDB** (SqlLocalDB.exe) é uma ferramenta de linha de comando simples para permitir que usuários e desenvolvedores criem e gerenciem uma instância do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. Para obter informações sobre como usar o **LocalDB**, consulte [SQL Server 2016 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md).  
  
## Sintaxe  
  
```  
SqlLocalDB.exe   
{  
      [ create   | c ] <instance-name>  <instance-version> [-s ]  
    | [ delete   | d ] <instance-name>  
    | [ start    | s ] <instance-name>  
    | [ stop     | p ] <instance-name>  [ -i ] [ -k ]  
    | [ share    | h ] [" <user_SID> " | " <user_account> " ] " <private-name> " " <shared-name> "  
    | [ unshare  | u ] " <shared-name> "  
    | [ info     | i ] <instance-name>  
    | [ versions | v ]  
    | [ trace    | t ] [ on | off ]  
    | [ help     | -? ]  
}  
```  
  
## Argumentos  
 [ **create** | **c** ] *\<instance-name>* *\<instance-version>* [**-s** ]  
 Cria uma nova instância do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. O **SqlLocalDB** usa a versão de binários [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] especificada pelo argumento *\<instance-version>*. O número da versão é especificado em formato numérico com pelo menos um decimal. Os números de versões secundárias (pacotes de serviço) são opcionais. Por exemplo, os dois números de versão seguintes são aceitáveis: 11.0 ou 11.0.1186. A versão especificada deve ser estalada no computador. Se não especificado, o número da versão será padronizado como a versão do utilitário **SqlLocalDB** . A adição de **–s** inicia a nova instância do **LocalDB**.  
  
 [ **share** | **h** ]  
 Compartilha a instância privada especificada do **LocalDB** que usa o nome compartilhado especificado. Se a SID ou o nome de conta do usuário for omitido, o valor padrão será o usuário atual.  
  
 [ **unshared** | **u** ]  
 Interrompe o compartilhamento da instância especificada compartilhada do **LocalDB**.  
  
 [ **delete** | **d** ] *\<instance-name>*  
 Exclui a instância especificada do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**.  
  
 [ **start** | **s** ] "*\<instance-name>*"  
 Inicia a instância especificada do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. Quando tem êxito, a instrução retorna o endereço de pipe nomeado do **LocalDB**.  
  
 [ **stop** | **p** ] *\<instance-name>* [**-i** ] [**-k** ]  
 Interrompe a instância especificada do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. A adição de **–i** solicita o desligamento da instância com a opção **NOWAIT** . A adição de **–k** elimina o processo da instância sem contatá-la.  
  
 [ **info** | **i** ] [ *\<instance-name>* ]  
 Lista todas as instâncias do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** de propriedade do usuário atual.  
  
 *\<instance-name>* retorna o nome, a versão, o estado (Executando ou Parado), a hora da última inicialização da instância especificada do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** e o nome do pipe local do **LocalDB**.  
  
 [ **trace** | **t** ] **on** | **off**  
 **trace on** habilita rastreamento para as chamadas à API do **SqlLocalDB** para o usuário atual. **trace off** desabilita o rastreamento.  
  
 **-?**  
 Retorna descrições breves de cada opção de **SqlLocalDB** .  
  
## Comentários  
 O argumento *instance name* deve seguir as regras de identificadores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou deve ser colocado entre aspas duplas.  
  
 A execução de SqlLocalDB sem argumentos retorna o texto da ajuda.  
  
 Operações diferentes de iniciar podem ser executados apenas em uma instância que pertence ao usuário conectado no momento. Quando compartilhada, uma instância do SQLLOCALDB só pode ser iniciada e interrompida pelo proprietário da instância.  
  
## Exemplos  
  
### A. Criando uma instância do LocalDB  
 O exemplo a seguir cria uma instância do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** denominada `DEPARTMENT` que usa os binários do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e inicia a instância.  
  
```  
SqlLocalDB.exe create "DEPARTMENT" 12.0 -s  
```  
  
### B. Trabalhando com uma instância compartilhada do LocalDB  
 Abrir um prompt de comando usando privilégios de administrador.  
  
```  
SqlLocalDB.exe create "DeptLocalDB"  
SqlLocalDB.exe share "DeptLocalDB" "DeptSharedLocalDB"  
SqlLocalDB.exe start "DeptLocalDB"  
SqlLocalDB.exe info "DeptLocalDB"  
REM The previous statement outputs the Instance pipe name for the next step  
sqlcmd –S np:\\.\pipe\LOCALDB#<use your pipe name>\tsql\query  
CREATE LOGIN NewLogin WITH PASSWORD = 'Passw0rd!!@52';   
GO  
CREATE USER NewLogin;  
GO  
EXIT  
```  
  
 Execute o código a seguir para conectar-se à instância compartilhada do **LocalDB** usando o logon `NewLogin` .  
  
```  
sqlcmd –S (localdb)\.\DeptSharedLocalDB -U NewLogin -P Passw0rd!!@52  
```  
  
## Consulte também  
 [SQL Server 2016 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
[Ferramenta de gerenciamento da linha de comando: SqlLocalDB.exe](Command-Line%20Management%20Tool:%20SqlLocalDB.exe.md)  
  