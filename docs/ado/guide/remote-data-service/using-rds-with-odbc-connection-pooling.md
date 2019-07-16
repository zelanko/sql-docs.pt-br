---
title: Usando RDS com Conexão de ODBC Pooling | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921933"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>Usar RDS com pool de conexões ODBC
Se você estiver usando uma fonte de dados ODBC, você pode usar a opção no Internet Information Services (IIS) do pool de conexão para alcançar a manipulação de alto desempenho de carga do cliente. Pooling de Conexão é um Gerenciador de recursos para conexões, mantendo o estado aberto em conexões usadas com frequência.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Para habilitar o pooling de conexão, consulte a documentação de serviços de informações da Internet.  
  
 Observe que habilitar o pooling de conexão pode sujeitar o servidor Web para outras restrições, conforme indicado na documentação do Microsoft Internet Information Services.  
  
 Para garantir que o pooling de conexão é estável e fornece ganhos de desempenho adicionais, você deve configurar o Microsoft SQL Server para usar a biblioteca de rede de soquete TCP/IP.  
  
 Para fazer isso, você precisa:  
  
-   Configure o computador do SQL Server para usar soquetes TCP/IP.  
  
-   Configure o servidor Web para usar soquetes TCP/IP.  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>Configurando o computador do SQL Server para usar soquetes TCP/IP  
 No computador do SQL Server, execute o programa de instalação do SQL Server para que as interações com a fonte de dados usam a biblioteca de rede de soquete TCP/IP.  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>Para especificar a biblioteca de rede de soquete TCP/IP no computador do SQL Server  
  
### <a name="in-microsoft-sql-server-65"></a>No Microsoft SQL Server 6.5:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 6.5 e, em seguida, clique em instalação do SQL.  
  
2.  Clique duas vezes em continuar.  
  
3.  No Microsoft SQL Server-caixa de diálogo de opções, selecione o suporte de rede de alteração e, em seguida, clique em continuar.  
  
4.  Verifique se que a caixa de seleção de soquetes TCP/IP está selecionada e clique em Okey.  
  
5.  Clique em Continuar para concluir e sair da instalação.  
  
### <a name="in-microsoft-sql-server-70"></a>In Microsoft SQL Server 7.0:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 7.0 e, em seguida, clique em utilitário de rede do servidor.  
  
2.  Na guia geral da caixa de diálogo, clique em Adicionar.  
  
3.  Na caixa de diálogo Adicionar configuração da biblioteca de rede, clique em TCP/IP.  
  
4.  Nas caixas de endereço de Proxy e número da porta, digite o endereço de número e o proxy de porta fornecido pelo seu administrador de rede.  
  
5.  Clique em Okey para concluir e sair da instalação.  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>Configurando o servidor Web para usar soquetes TCP/IP  
 Há duas opções para configurar o servidor Web para usar soquetes TCP/IP. O que fazer depende se todos os servidores SQL são acessados a partir do servidor Web ou apenas um servidor específico do SQL é acessado do servidor Web.  
  
 Se todos os servidores SQL são acessados do servidor Web, você precisará executar o utilitário de configuração de cliente do SQL Server no computador do servidor Web. As etapas a seguir alteram a biblioteca de rede padrão para todas as conexões do SQL Server feitas nesse servidor Web do IIS para usar a biblioteca de rede de soquetes TCP/IP.  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>Para configurar o servidor Web (todos os servidores SQL)  
  
### <a name="for-microsoft-sql-server-65"></a>Para o Microsoft SQL Server 6.5:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 6.5 e, em seguida, clique em SQL Client Configuration Utility.  
  
2.  Clique na guia biblioteca de rede.  
  
3.  Na caixa de rede padrão, selecione soquetes TCP/IP.  
  
4.  Clique em concluído para salvar as alterações e sair do utilitário.  
  
### <a name="for-microsoft-sql-server-70"></a>Para o Microsoft SQL Server 7.0:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 7.0 e, em seguida, clique em utilitário de rede do cliente.  
  
2.  Clique na guia Geral.  
  
3.  Na caixa de biblioteca de rede padrão, clique em TCP/IP.  
  
4.  Clique em Okey para salvar as alterações e sair do utilitário.  
  
 Se um servidor específico do SQL é acessado de um servidor Web, você precisa executar o utilitário de configuração de cliente do SQL Server no computador do servidor Web. Para alterar a biblioteca de rede para uma conexão específica do SQL Server, configure o software cliente do SQL Server no computador do servidor Web, da seguinte maneira.  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>Para configurar o servidor Web (um servidor específico do SQL)  
  
### <a name="for-microsoft-sql-server-65"></a>Para o Microsoft SQL Server 6.5:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 6.5 e, em seguida, clique em SQL Client Configuration Utility.  
  
2.  Clique na guia Avançado.  
  
3.  Na caixa do servidor, digite o nome do servidor para conectar-se ao uso de soquetes TCP/IP.  
  
4.  Na caixa Nome da DLL, selecione soquetes TCP/IP.  
  
5.  Clique em Adicionar/modificar. Todas as fontes de dados que aponta para esse servidor passará a usar soquetes TCP/IP.  
  
6.  Clique em concluído.  
  
### <a name="for-microsoft-sql-server-70"></a>Para o Microsoft SQL Server 7.0:  
  
1.  No menu Iniciar, aponte para programas, aponte para Microsoft SQL Server 7.0 e, em seguida, clique em utilitário de configuração do cliente.  
  
2.  Clique na guia Geral.  
  
3.  Clique em Adicionar.  
  
4.  Insira o alias do servidor na caixa de alias do servidor. Na caixa de bibliotecas de rede, clique em TCP/IP. Na caixa Nome do computador, insira o nome do computador do computador que escuta para clientes de soquetes TCP/IP. Na caixa de número de porta, insira a porta na qual o SQL Server escuta.  
  
5.  Clique em Okey e Okey novamente para sair do utilitário.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)






















