---
title: "A execução do Script SQL do catálogo de endereço | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4751361a50f4fe594ad4ffc9d4233b41a4918361
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="running-the-address-book-sql-script"></a>A execução do Script SQL do catálogo de endereço
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Você deve usar o utilitário de linha de comando ISQL/Query Analyzer ou o SQL Server Enterprise Manager para executar o script SQL incluído (Sampleemp.sql) que:  
  
-   Cria um novo banco de dados, AddrBookDB, no dispositivo padrão.  
  
-   Conecta-se ao banco de dados, AddrBookDB.  
  
-   Cria uma tabela de funcionários.  
  
-   Preenche a tabela com dados de exemplo.  
  
-   Executa uma instrução SELECT simples para verificar se a população da tabela de banco de dados.  
  
-   Configura uma conta de usuário chamada "adcdemo" com a senha "adcdemo".  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Para executar o script de Sampleemp.sql no Microsoft SQL Server 6.5  
  
1.  Clique em **iniciar**, aponte para **programas**e, em seguida, aponte para **Microsoft SQL Server 6.5**. Clique em **SQL Enterprise Manager**.  
  
2.  Do **ferramentas** menu, clique em **ferramenta de consulta do SQL**.  
  
3.  Clique em **carga SQL Script** e navegue até c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
4.  Selecione o arquivo Sampleemp.sql. Clique em **Abrir**.  
  
5.  Clique o **executar consulta** botão (a seta verde na barra de ferramentas).  
  
6.  Depois que ele é executado, feche o **consulta** e **Enterprise Manager** windows.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Para executar o script de Sampleemp.sql no Microsoft SQL Server 7.0  
  
1.  Clique em **iniciar**, aponte para **programas**e, em seguida, aponte para **Microsoft SQL Server 7.0**. Clique em **Enterprise Manager**.  
  
2.  Certifique-se de que o SQL Server que você deseja usar está selecionado na lista de servidores registrados no Enterprise Manager.  
  
3.  Do **ferramentas** menu, clique em **SQL Server Query Analyzer**.  
  
4.  Clique o **carga SQL Script** botão (a pasta aberta na barra de ferramentas) e navegue para c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
5.  Selecione o arquivo Sampleemp.sql. Clique em **Abrir**.  
  
6.  Clique o **executar consulta** botão (a seta verde na barra de ferramentas) ou **F5**.  
  
7.  Depois que ele é executado, feche o **consulta**, **Query Analyzer**, e **Enterprise Manager** windows.  
  
## <a name="see-also"></a>Consulte também  
 [Executando o aplicativo de exemplo do catálogo de endereços](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)



