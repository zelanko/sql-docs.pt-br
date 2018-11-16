---
title: Executar o Script SQL do catálogo de endereços | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c77bece1b2ab67cc361f7445240e1a2b1190587
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51557793"
---
# <a name="running-the-address-book-sql-script"></a>Executar o script SQL do catálogo de endereços
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Você deve usar o utilitário de linha de comando ISQL/Query Analyzer ou o SQL Server Enterprise Manager para executar o script SQL incluído (Sampleemp.sql) que:  
  
-   Cria um novo banco de dados, AddrBookDB, no dispositivo padrão.  
  
-   Conecta-se ao banco de dados, AddrBookDB.  
  
-   Cria uma tabela de funcionários.  
  
-   Preenche a tabela com dados de exemplo.  
  
-   Executa uma instrução SELECT simples para verificar se a população da tabela de banco de dados.  
  
-   Configura uma conta de usuário chamada "adcdemo" com uma senha de "adcdemo".  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Para executar o script de Sampleemp.sql no Microsoft SQL Server 6.5  
  
1.  Clique em **inicie**, aponte para **programas**e, em seguida, aponte para **Microsoft SQL Server 6.5**. Clique em **SQL Enterprise Manager**.  
  
2.  Dos **ferramentas** menu, clique em **ferramenta de consulta SQL**.  
  
3.  Clique em **carga SQL Script** e navegue até c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
4.  Selecione o arquivo Sampleemp.sql. Clique em **Abrir**.  
  
5.  Clique o **executar consulta** botão (a seta verde na barra de ferramentas).  
  
6.  Depois de sua execução, feche o **consulta** e **Enterprise Manager** windows.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Para executar o script de Sampleemp.sql no Microsoft SQL Server 7.0  
  
1.  Clique em **inicie**, aponte para **programas**e, em seguida, aponte para **Microsoft SQL Server 7.0**. Clique em **Enterprise Manager**.  
  
2.  Certifique-se de que o SQL Server que você deseja usar está selecionado na lista de servidores registrados no Enterprise Manager.  
  
3.  Dos **ferramentas** menu, clique em **SQL Server Query Analyzer**.  
  
4.  Clique o **carga SQL Script** botão (a pasta aberta na barra de ferramentas) e navegue até c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
5.  Selecione o arquivo Sampleemp.sql. Clique em **Abrir**.  
  
6.  Clique o **executar consulta** botão (a seta verde na barra de ferramentas) ou **F5**.  
  
7.  Depois de sua execução, feche o **consulta**, **analisador de consultas**, e **Enterprise Manager** windows.  
  
## <a name="see-also"></a>Consulte também  
 [Executando o aplicativo de exemplo do catálogo de endereços](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


