---
title: "Definir um idioma de sess&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erros [SQL Server], considerações internacionais"
  - "globalização [SQL Server], sessões"
  - "tempo [SQL Server]"
  - "sessões [SQL Server], idiomas"
  - "considerações internacionais [SQL Server], sessões"
  - "datas [SQL Server], idiomas de sessão"
  - "considerações globais [SQL Server], sessões"
  - "idioma da sessão do lado do cliente"
  - "horas [SQL Server], idiomas de sessão"
  - "mensagens [SQL Server], considerações internacionais"
  - "idioma da sessão do lado do servidor"
ms.assetid: de7f2c90-8f4f-4cfc-94cc-4933a7fd2bde
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Definir um idioma de sess&#227;o
  O idioma da sessão pode ser usado para definir como os seguintes elementos são exibidos no servidor com base na preferência cultural e de idioma:  
  
-   O idioma que será usado para erros e outras mensagens do sistema. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a várias cópias de todas as cadeias de caracteres de erros e de mensagens do sistema em todos os idiomas nos quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponível. Essas mensagens podem ser exibidas na exibição de catálogo [sys.messages](../Topic/sys.messages%20\(Transact-SQL\).md). Quando uma versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalada, essas mensagens do sistema são traduzidas para a versão do idioma instalado. Por padrão, você também obtém o conjunto dessas mensagens em inglês (EUA). Além disso, é possível adicionar mensagens definidas pelo usuário em um idioma específico usando [sp_addmessage](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
  
-   O formato de dados de data e hora.  
  
-   Os nomes de dias e meses, inclusive abreviações.  
  
-   O primeiro dia da semana.  
  
-   Dados de moeda.  
  
 Há 33 idiomas disponíveis para uso como configurações de sessão. Para obter uma lista de idiomas, consulte [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).  
  
## Definindo o idioma da sessão no servidor  
 Para definir o idioma da sessão do lado de servidor, use [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md).  
  
## Definindo o idioma da sessão no cliente  
 O idioma da sessão pode ser definido no lado do cliente usando o OLE DB, ODBC ou ADO.NET. Para OLE DB, use a propriedade SSPROP_INIT_CURRENTLANGUAGE. Para obter mais informações, consulte [Propriedades de inicialização e autorização](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
 Para ODBC, use a palavra-chave Idioma. Para obter mais informações, consulte [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md).  
  
 Para ADO.NET, use o parâmetro **Idioma Atual** do objeto **ConnectionString**. Para obter mais informações, consulte a documentação do SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access Components (MDAC).  
  
  