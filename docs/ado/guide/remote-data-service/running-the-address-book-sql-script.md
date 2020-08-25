---
description: Executar o script SQL do catálogo de endereços
title: Executando o script SQL do catálogo de endereços | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c8c47f4e5cd5235ee0289df27d31193db8a2e1d
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759306"
---
# <a name="running-the-address-book-sql-script"></a>Executar o script SQL do catálogo de endereços
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Você deve usar o utilitário de linha de comando ISQL/Query Analyzer ou o Gerenciador de SQL Server Enterprise para executar o script SQL incluído (Sampleemp. Sql) que:  
  
-   Cria um novo banco de dados, AddrBookDB, no dispositivo padrão.  
  
-   Conecta-se ao banco de dados, AddrBookDB.  
  
-   Cria uma tabela Employee.  
  
-   Popula a tabela com dados de exemplo.  
  
-   Executa uma instrução SELECT simples para verificar a população da tabela de banco de dados.  
  
-   Configura uma conta de usuário chamada "adcdemo" com a senha "adcdemo".  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Para executar o script Sampleemp. SQL no Microsoft SQL Server 6,5  
  
1.  Clique em **Iniciar**, aponte para **programas**e, em seguida, aponte para **Microsoft SQL Server 6,5**. Clique em **SQL Enterprise Manager**.  
  
2.  No menu **ferramentas** , clique em **ferramenta de consulta SQL**.  
  
3.  Clique em **carregar script SQL** e navegue até c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
4.  Selecione o arquivo Sampleemp. Sql. Clique em **Abrir**.  
  
5.  Clique no botão **Executar consulta** (a seta verde na barra de ferramentas).  
  
6.  Após a execução, feche a **consulta** e as janelas do **Enterprise Manager** .  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Para executar o script Sampleemp. SQL no Microsoft SQL Server 7,0  
  
1.  Clique em **Iniciar**, aponte para **programas**e, em seguida, aponte para **Microsoft SQL Server 7,0**. Clique em **Enterprise Manager**.  
  
2.  Certifique-se de que o SQL Server que você deseja usar esteja selecionado na lista de servidores registrados no Enterprise Manager.  
  
3.  No menu **ferramentas** , clique em **SQL Server Query Analyzer**.  
  
4.  Clique no botão **carregar script SQL** (a pasta abrir na barra de ferramentas) e navegue até c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
5.  Selecione o arquivo Sampleemp. Sql. Clique em **Abrir**.  
  
6.  Clique no botão **Executar consulta** (a seta verde na barra de ferramentas) ou **F5**.  
  
7.  Após a execução, feche a **consulta**, o **Query Analyzer**e o Windows **Enterprise Manager** .  
  
## <a name="see-also"></a>Consulte Também  
 [Executar o aplicativo de exemplo do catálogo de endereços](./running-the-address-book-sample-application.md)