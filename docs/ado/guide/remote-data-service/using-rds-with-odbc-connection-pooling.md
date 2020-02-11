---
title: Usando o RDS com o ODBC Connection Pooling | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling in RDS [ADO]
ms.assetid: e8b912c1-da5b-4e85-a000-1e6648a94237
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2ffcc64cb9d0e45d371e927cd1c15be51cd917c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921933"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>Usar RDS com pool de conexões ODBC
Se você estiver usando uma fonte de dados ODBC, poderá usar a opção de pooling de conexão no Serviços de Informações da Internet (IIS) para obter o tratamento de alto desempenho da carga do cliente. O pool de conexões é um Gerenciador de recursos para conexões, mantendo o estado aberto em conexões usadas com frequência.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Para habilitar o pool de conexões, consulte a documentação do Serviços de Informações da Internet.  
  
 Observe que habilitar o pool de conexões pode sujeitar o servidor Web a outras restrições, conforme observado na documentação do Microsoft Serviços de Informações da Internet.  
  
 Para garantir que o pool de conexões seja estável e forneça ganhos de desempenho adicionais, você deve configurar o Microsoft SQL Server para usar a biblioteca de rede de soquete TCP/IP.  
  
 Para fazer isso, você precisa:  
  
-   Configure o computador SQL Server para usar soquetes TCP/IP.  
  
-   Configure o servidor Web para usar soquetes TCP/IP.  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>Configurando o computador SQL Server para usar soquetes TCP/IP  
 No computador SQL Server, execute o programa de instalação do SQL Server para que as interações com a fonte de dados usem a biblioteca de rede de soquete TCP/IP.  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>Para especificar a biblioteca de rede de soquete TCP/IP no computador SQL Server  
  
### <a name="in-microsoft-sql-server-65"></a>No Microsoft SQL Server 6,5:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 6,5 e clique em configuração do SQL.  
  
2.  Clique em continuar duas vezes.  
  
3.  Na caixa de diálogo Microsoft SQL Server-opções, selecione Alterar suporte de rede e clique em continuar.  
  
4.  Verifique se a caixa de seleção Soquetes TCP/IP está marcada e clique em OK.  
  
5.  Clique em continuar para concluir e saia da instalação.  
  
### <a name="in-microsoft-sql-server-70"></a>No Microsoft SQL Server 7,0:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 7,0 e clique em utilitário de rede do servidor.  
  
2.  Na guia Geral da caixa de diálogo, clique em Adicionar.  
  
3.  Na caixa de diálogo Adicionar configuração da biblioteca de rede, clique em TCP/IP.  
  
4.  Nas caixas número da porta e endereço proxy, insira o número da porta e o endereço do proxy fornecidos pelo administrador da rede.  
  
5.  Clique em OK para concluir e saia da instalação.  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>Configurando o servidor Web para usar soquetes TCP/IP  
 Há duas opções para configurar o servidor Web para usar soquetes TCP/IP. O que você faz depende se todos os SQL Servers são acessados do servidor Web ou apenas um SQL Server específico é acessado do servidor Web.  
  
 Se todos os SQL Servers forem acessados do servidor Web, você precisará executar o utilitário de configuração do cliente SQL Server no computador do servidor Web. As etapas a seguir alteram a biblioteca de rede padrão para todas as conexões SQL Server feitas desse servidor Web do IIS para usar a biblioteca de rede de soquetes TCP/IP.  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>Para configurar o servidor Web (todos os SQL Servers)  
  
### <a name="for-microsoft-sql-server-65"></a>Para Microsoft SQL Server 6,5:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 6,5 e clique em utilitário de configuração do cliente SQL.  
  
2.  Clique na guia NET Library.  
  
3.  Na caixa rede padrão, selecione Soquetes TCP/IP.  
  
4.  Clique em concluído para salvar as alterações e sair do utilitário.  
  
### <a name="for-microsoft-sql-server-70"></a>Para Microsoft SQL Server 7,0:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 7,0 e clique em utilitário de rede do cliente.  
  
2.  Clique na guia Geral.  
  
3.  Na caixa biblioteca de rede padrão, clique em TCP/IP.  
  
4.  Clique em OK para salvar as alterações e sair do utilitário.  
  
 Se um SQL Server específico for acessado de um servidor Web, você precisará executar o utilitário de configuração do cliente SQL Server no computador do servidor Web. Para alterar a biblioteca de rede para uma conexão de SQL Server específica, configure o software cliente do SQL Server no computador do servidor Web da seguinte maneira.  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>Para configurar o servidor Web (um SQL Server específico)  
  
### <a name="for-microsoft-sql-server-65"></a>Para Microsoft SQL Server 6,5:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 6,5 e clique em utilitário de configuração do cliente SQL.  
  
2.  Clique na guia Avançado.  
  
3.  Na caixa servidor, digite o nome do servidor com o qual se conectar usando soquetes TCP/IP.  
  
4.  Na caixa nome da DLL, selecione Soquetes TCP/IP.  
  
5.  Clique em Adicionar/modificar. Todas as fontes de dados que apontam para este servidor agora usarão Soquetes TCP/IP.  
  
6.  Clique em Concluído.  
  
### <a name="for-microsoft-sql-server-70"></a>Para Microsoft SQL Server 7,0:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 7,0 e clique em utilitário de configuração do cliente.  
  
2.  Clique na guia Geral.  
  
3.  Clique em Adicionar.  
  
4.  Insira o alias do servidor na caixa alias do servidor. Na caixa bibliotecas de rede, clique em TCP/IP. Na caixa nome do computador, digite o nome do computador que escuta os clientes de soquetes TCP/IP. Na caixa número da porta, insira a porta na qual o SQL Server escuta.  
  
5.  Clique em OK e em OK novamente para sair do utilitário.  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)






















